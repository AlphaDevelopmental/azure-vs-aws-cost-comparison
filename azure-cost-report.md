# Azure Cost Report — SaaS Application Workload

## 1. Calculator Metadata

- **Estimate Share Link (Linux):** https://azure.com/e/f13f8e56174346b2b890b72982938793
- **Region:** East US
- **Currency:** USD ($)
- **Pricing Model:** Pay-as-you-go (no commitment discounts applied)
- **Estimate Date:** June 2026

---

## 2. Scenario A — Linux (Ubuntu)

### A. Compute: Azure Virtual Machine

- **Instance:** B2als v2 (2 vCPUs, 4 GB RAM)
- **Operating System:** Linux (Ubuntu)
- **Tier:** Standard
- **Pricing Model:** Pay as you go
- **Managed Disk:** S10 Standard HDD (128 GiB)
- **Uptime:** 730 hours/month (24/7)
- **Monthly Cost:** $33.34 (VM $27.45 + Disk $5.89)

### B. Object Storage: Azure Blob Storage

- **Type:** Block Blob Storage, General Purpose V2
- **Redundancy:** LRS (Locally Redundant Storage)
- **Access Tier:** Hot
- **Capacity:** 50 GB
- **Monthly Cost:** $2.08

### C. Managed Database: Azure Database for MySQL

- **Deployment:** Flexible Server
- **Tier:** Burstable (B1MS, 1 vCore)
- **Storage:** 20 GiB
- **Utilization:** 730 hours/month
- **Monthly Cost:** $14.71

### D. Networking: Azure Bandwidth

- **Data Transfer Type:** Internet Egress
- **Source Region:** East US
- **Routing:** Microsoft Global Network
- **Volume:** 500 GB/month
- **Monthly Cost:** $34.80

### Scenario A Total

| Component | Monthly Cost |
|---|---|
| Azure VM B2als v2 + S10 Disk (Linux) | $33.34 |
| Azure Blob Storage (50GB LRS Hot) | $2.08 |
| Azure Database for MySQL Flexible | $14.71 |
| Azure Bandwidth (500GB egress) | $34.80 |
| **Total Monthly** | **$84.93** |
| **Total Annual** | **$1,019.16** |

---

## 3. Scenario B — Windows Server with Azure Hybrid Benefit

Azure Hybrid Benefit (AHB) allows organizations with existing on-premises Windows Server licenses (covered under Software Assurance) to apply those licenses to Azure VMs, effectively eliminating the Windows OS licensing premium.

### VM Cost Breakdown (Windows)

| Pricing Option | Monthly VM Cost |
|---|---|
| Windows Server (License Included) | $34.16 |
| Windows OS Premium | $6.72 |
| **Total VM without Hybrid Benefit** | **$40.88** |
| **With Azure Hybrid Benefit applied** | **$34.16** (OS premium waived) |

### Scenario B Total (with Hybrid Benefit)

| Component | Monthly Cost |
|---|---|
| Azure VM B2als v2 + S10 Disk (Windows + HB) | $40.05 |
| Azure Blob Storage (50GB LRS Hot) | $2.08 |
| Azure Database for MySQL Flexible | $14.71 |
| Azure Bandwidth (500GB egress) | $34.80 |
| **Total Monthly** | **$91.64** |
| **Total Annual** | **$1,099.68** |

### Hybrid Benefit Insight

The Windows Server scenario costs **$6.71 more per month** than Linux when Hybrid Benefit is applied. Without Hybrid Benefit, the Windows VM would cost approximately $40.88/month (adding $6.72 OS premium), making the total **$98.36/month** — a 15.8% premium over the Linux baseline. Organizations already holding Windows Server licenses through Microsoft's Volume Licensing or Software Assurance programs can recover this premium entirely, making Azure Windows deployments cost-neutral compared to Linux.

---

## 4. Key Cost Observations

Azure's most significant cost advantage over AWS lies in its **managed database pricing**. Azure Database for MySQL Flexible Server (Burstable B1MS) costs $14.71/month versus AWS RDS for MySQL at $92.09/month — a **6.3x price difference** for equivalent small-scale database workloads. This alone drives the majority of Azure's cost advantage in this comparison.

Azure's egress pricing ($34.80 for 500GB) is approximately 22.7% cheaper than AWS's equivalent ($45.00), providing additional savings for network-intensive applications. Compute pricing is broadly comparable between providers at this scale.