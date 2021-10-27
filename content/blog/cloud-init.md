---
title: "Cloud-Init"
date: 2021-10-27T11:27:17+02:00
draft: true
---

Aurreko atalean aipatu bezala, automatizazio tresna ezberdinak erabili nahiko nituzke makina birtualen sorrera eta kudeaketa ahalik eta modu txukunenean egiteko.

## Cloud-Init buruz
Honetarako [Cloud-Init](https://cloud-init.io/) oso ondo datorkit. Makina birtual baten hasieratzea kudeatzeko tresna da. Birtualizazio eta Cloud hornitzaile gehienek onartzen duten estandarra bihurtu da. Sistema eragilearen oinarrizko txantiloi bat izanda, hainbat konfigurazio ezarri daitezke aldiz aurretik (erabiltzaileak, sare konfigurazioa etab.).

Linux distribuzio ezagunenek _Cloud-Init_ soportea eskeintzen dute, cloud inguruneentzako espreski prestatutako irudi-txantiloiak eskeiniz. Adibidez, hemen Ubuntu eta Debianek eskeinitako irudiak:

- [Ubuntu Cloud irudiak](http://cloud-images.ubuntu.com/releases/)
- [Debian Cloud irudiak](https://cloud.debian.org/images/cloud/)

Irudi hauek erabiliz, _User-Data_ delako aukera pertsonalizatuak txertatu izango dizkiogu instantziei hauek guk nahi ditugun konfigurazioak izateko.


## Cloud-Init eta ProxmoxVE
Cloud hornitzaileetaz gain, guk geuk ere erabili ditzazkegu irudi hauek _Proxmox_ bezalako plataforma batean. Egin beharreko lehen urratsa Proxmox _template_ edo txantiloi bat egitea da, kasu honetan Ubuntu Cloud irudia oinarri gisa erabiliz:

### 1- Deskargatu oinarrizko Ubuntu irudia

Hurrengo urrats hauek gure ordenagailuan egin ditzazkegu:
```
# Download Ubuntu Server 20.04 LTS Cloud irudia
wget wget https://cloud-images.ubuntu.com/focal/current/focal-server-cloudimg-amd64.img
```

### 2- Gehitu qemu-guest-agent

Irudi hau ProxmoxVEn modu egokian erabili ahal izateko, `qemu-guest-agent` paketea gehitu beharko diogu. Horretarako *virt-customize* izeneko aplikazioa erabili dezakegu:

```
sudo apt update -y && sudo apt install libguestfs-tools -y
sudo virt-customize -a focal-server-cloudimg-amd64.img --install qemu-guest-agent
```

Orain moldatutako irudi hau ProxmoxVE zerbitzarira pasatzeko unea da. Hurrengo aginduak Proxmox zerbitzarian bertan egin beharrekoak dira.

### 3- Sortu Proxmox txantiloia
Hurrengo agindu hauen bidez, VM berri bat sortuko dugu lehendabizi, eta gero txantiloi bihurtuko dugu.

```
# Create VM
qm create 9000 --name "ubuntu-2004-cloudinit-template" --memory 2048 --cores 2 --net0 virtio,bridge=vmbr0
qm importdisk 9000 focal-server-cloudimg-amd64.img ceph-rbd
qm set 9000 --scsihw virtio-scsi-pci --scsi0 ceph-rbd:vm-9000-disk-0
qm set 9000 --boot c --bootdisk scsi0
qm set 9000 --ide2 ceph-rbd:cloudinit
qm set 9000 --serial0 socket --vga serial0
qm set 9000 --agent 1

# Generate Proxmox template
qm template 9000
```

Hainbat ohar aurreko aginduen inguruan:
- VMaren diskoa gordetzeko biltegiratze gisa _"ceph-rbd"_ izeneko bolumena erabili dut nire kasuan. Zure kasuan seguraski *local* edo *local-lvm* erabili nahiko duzu.
- Ikusi dudanaren arabera, vmid 9000 jartzen zaio normalean horrelako txantiloi bati, baina nahi duzuna jar dezakezu (beti ere libre badago)

Behin aurreko urratsak jarraituta, txantiloia ikusiko dugu zerbitzarian (VM id 9000). Txantiloi honek ez du inolako pertsonalizazio berezirik momentuz, sartu diogun (moldatutako) irudia izan ezik. Izan ere, aukera pertsonalizatu horiek VMak sortu edo klonatzean gehituko dizkiogu makinei.

### 4- Sortu txantiloian oinarritutako VMak (eta gehitu aukera pertsonalizatuak)

Egin berri dugun txantiloia erabiltzeko adibide soil bat ikusiko dugu jarraian. Pixka bat "artesanala" izango da momentuz, script bat erabiliz. Aurrerago prozesu hau *Terraform* bidez beste modu batera egin daitekeela ikusiko dugu.

```
#/bin/sh

VMID=$(pvesh get /cluster/nextid)
VMNAME=nire-makina
IPADDRESS=192.168.1.34
IPPREFIX=24
GATEWAY=192.168.1.1
VLAN=10
DNS1=1.1.1.1
GHUSERNAME=xezpeleta

echo Deploying VM with ID $VMID and name $VMNAME

qm clone 9000 $VMID --name $VMNAME

# Download and include ssh pubkey
curl -o /tmp/id_rsa.pub https://github.com/$GHUSERNAME.keys \
        && qm set $VMID --sshkey /tmp/id_rsa.pub \
        && rm /tmp/id_rsa.pub

# SET Vlan
pvesh set /nodes/nireproxmoxnodoa/qemu/$VMID/config --net0 virtio,bridge=vmbr0,tag=$VLAN

# Configure IP address
qm set $VMID --ipconfig0 ip=$IPADDRESS/$IPPREFIX,gw=$GATEWAY --nameserver $DNS1

# Start the VM
qm start $VMID
```

Script honek VM berri bat sortuko digu Proxmox-en. Cloud-Init esker aurretik nahi genituen hainbat konfigurazio ezarriko dizkio (IP helbidea, SSH giltza publikoa, etab). Eta ez hori bakarrik: Proxmox web UIaren bidez ere, VM horretara sartzean Cloud-Init atalean datu minimo hauek aldatzeko aukera eskeiniko digu orain.

Hurrengo atalean gaur sortutako txantiloia erabiliko dugu **Terraform** bidez behar ditugun makinak sortzeko.


## Erreferentziak

- [How to create a Proxmox Ubuntu cloud-init image](https://austinsnerdythings.com/2021/08/30/how-to-create-a-proxmox-ubuntu-cloud-init-image/)

