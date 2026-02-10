---
title: "TrikuSec"
date: 2026-02-10
draft: false
tags: ["security", "lynis", "linux", "audit", "open-source", "docker"]
cover:
    image: "/images/trikusec-cover.png"
    alt: "TrikuSec Cover"
    caption: "TrikuSec Cover"
---

[Lynis](https://cisofy.com/lynis/) is an open-source security auditing tool for Linux systems. It scans file permissions, kernel parameters, installed packages, running services, and more. It's read-only — it never changes anything on the system, just reports what it finds.

The problem comes when managing multiple servers. Running Lynis on each one, collecting the reports, and tracking changes over time becomes tedious quickly.

## A centralized dashboard for Lynis

![TrikuSec Devices Dashboard](https://raw.githubusercontent.com/trikusec/trikusec/main/docs/assets/img/trikusec-devices.png)

I built **TrikuSec** to solve this. It's a centralized platform that collects Lynis audit reports from multiple servers and presents them in a single web dashboard.

How it works:

1. Deploy TrikuSec with Docker (`docker compose up -d`)
2. Configure each server to send Lynis reports via a cron job
3. View all results from the dashboard

Like Lynis itself, TrikuSec follows a **read-only** model. Servers send data to TrikuSec, but TrikuSec never sends commands back.

## Main features

- **Device Management**: All servers in one place, with metadata like hostname, OS, and distribution
- **Compliance Policies**: Define rules (e.g. "SSH root login must be disabled") and check all servers against them automatically

![TrikuSec Policies](https://raw.githubusercontent.com/trikusec/trikusec/main/docs/assets/img/trikusec-policies.png)

- **Change Tracking**: Diff reports between audits to see exactly what changed
- **PDF Reports**: Export compliance status for documentation or audits

## What's next

Some ideas for future versions: interactive charts and trend analysis, an alerting system (Slack, email, webhooks) for compliance changes, and possibly Windows support through similar auditing tools.

## Try it

TrikuSec is open-source under GPL-3.0.

- Source code: [github.com/trikusec/trikusec](https://github.com/trikusec/trikusec)
- Documentation: [trikusec.github.io/trikusec](https://trikusec.github.io/trikusec/)

```bash
docker compose up -d
```

**Important**: TrikuSec is not a professional product. It's an open-source project in active development. If you need enterprise support and SLAs, consider [Lynis Enterprise](https://cisofy.com/pricing/) by CISOfy.

> Note: I have no affiliation with CISOfy or the Lynis project.
