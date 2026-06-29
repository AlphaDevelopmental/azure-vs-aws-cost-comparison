# Web Application Specifications — Cost Comparison Baseline

This document defines the fixed specifications used to price the same workload on both AWS and Azure. Keeping these specs identical across both calculators ensures a fair, apples-to-apples cost comparison.

## Scenario

A small SaaS startup running a customer-facing API with a database backend, serving a moderate number of users.

## Compute Requirements

| Spec | Value |
|---|---|
| vCPUs | 2 |
| RAM | 4 GB |
| Operating System (Scenario A) | Linux (Ubuntu) |
| Operating System (Scenario B) | Windows Server (with Hybrid Benefit on Azure) |
| Uptime | 24/7 (730 hours/month) |

## Storage Requirements

| Spec | Value |
|---|---|
| Block/Disk storage | 100 GB SSD, general purpose |
| Object storage (file uploads, backups) | 50 GB |

## Database Requirements

| Spec | Value |
|---|---|
| Type | Managed relational database (SQL) |
| Storage | 20 GB |
| Tier | Basic/General Purpose (smallest production-ready tier) |

## Networking Requirements

| Spec | Value |
|---|---|
| Monthly outbound data transfer (egress) | 500 GB |
| Inter-zone/inter-region transfer | To be evaluated separately in Task 4 |

## Region

US East (N. Virginia on AWS / East US on Azure) — chosen for direct comparability and typically the lowest-cost region on both platforms.
