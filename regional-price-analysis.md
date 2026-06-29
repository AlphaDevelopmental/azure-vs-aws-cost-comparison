# Regional Price Analysis — AWS vs Azure

## Overview

This document extends the baseline US East cost comparison across two additional global regions: **Europe (London / West Europe)** and **Asia Pacific (Singapore / Southeast Asia)**. All estimates use identical specifications — 2 vCPU, 4 GB RAM, 100 GB block storage, 20 GB managed MySQL, 50 GB object storage, and 500 GB monthly egress — priced on both AWS and Azure pricing calculators.

---

## Regional Cost Matrix — Linux (Pay-as-you-go / On-Demand)

| Region | AWS Monthly | Azure Monthly | Azure Saving | Azure Saving % |
|---|---|---|---|---|
| US East (N. Virginia / East US) | $170.77 | $84.93 | $85.84 | **50.3%** |
| Europe (London / West Europe) | $161.51 | $91.60 | $69.91 | **43.3%** |
| Asia Pacific (Singapore / Southeast Asia) | $199.34 | $112.13 | $87.21 | **43.8%** |

## Regional Cost Matrix — Windows Server

| Region | AWS Monthly | Azure (with Hybrid Benefit) | Azure Saving | Azure Saving % |
|---|---|---|---|---|
| US East | $170.77 | $91.64 | $79.13 | **46.3%** |
| Europe (London / West Europe) | $184.14 | $98.31 | $85.83 | **46.6%** |
| Asia Pacific (Singapore) | $201.02 | $118.84 | $82.18 | **40.9%** |

---

## Service-Level Regional Breakdown

### Compute (EC2 / Azure VM)

| Region | AWS EC2 (Linux) | Azure VM (Linux) | Difference |
|---|---|---|---|
| US East | $32.53 | $27.45 | Azure cheaper by $5.08 |
| Europe (London) | ~$36.73 | $31.54 | Azure cheaper by $5.19 |
| Singapore | ~$14.93 | $34.46 | AWS cheaper by $19.53 |

> **Insight:** Singapore is the one region where AWS compute is cheaper than Azure. AWS uses ARM-based t4g instances at very competitive rates in Asia Pacific, while Azure's B2als v2 pricing is less aggressive in that region.

### Database (RDS / Azure MySQL Flexible Server)

| Region | AWS RDS MySQL | Azure MySQL Flexible | Difference |
|---|---|---|---|
| US East | $92.09 | $14.71 | Azure cheaper by $77.38 |
| Europe (London) | $101.21 | $17.27 | Azure cheaper by $83.94 |
| Singapore | $123.21 | $21.74 | Azure cheaper by $101.47 |

> **Critical Insight:** The database cost gap between AWS and Azure **widens in Asia Pacific**. AWS RDS in Singapore is 5.7x more expensive than Azure MySQL Flexible Server. This is the single largest contributor to AWS's cost disadvantage across all regions.

### Network Egress (500 GB outbound)

| Region | AWS Data Transfer | Azure Bandwidth | Difference |
|---|---|---|---|
| US East | $45.00 | $34.80 | Azure cheaper by $10.20 |
| Europe (London) | $45.00 | $34.80 | Azure cheaper by $10.20 |
| Singapore | $60.00 | $48.00 | Azure cheaper by $12.00 |

> **Insight:** Both providers charge more for egress from Asia Pacific. AWS charges $0.12/GB from Singapore versus $0.09/GB from the US — a 33% premium. Azure charges $0.096/GB from Southeast Asia versus $0.0696/GB from US East — a 38% premium. Both providers penalise Asian egress similarly.

### Object Storage (50 GB S3 / Blob)

| Region | AWS S3 | Azure Blob | Difference |
|---|---|---|---|
| US East | $1.15 | $2.08 | AWS cheaper |
| Europe | $1.20 | $2.11 | AWS cheaper |
| Singapore | $1.20 | $2.04 | AWS cheaper |

> **Insight:** AWS S3 is consistently cheaper than Azure Blob Storage across all regions. However the difference is small ($0.84–$0.93/month) and does not materially affect the overall comparison.

---

## Regional Variation Summary

### Price Stability

Azure pricing is **more stable across regions** than AWS. Azure's total cost increases by 32.0% moving from US East to Southeast Asia ($84.93 → $112.13). AWS increases by 16.7% from US East to Europe ($170.77 → $161.51 — actually cheaper in Europe) and 16.7% from US East to Singapore ($170.77 → $199.34).

### Where AWS is Cheapest

AWS's most competitive region in this comparison is **Europe (London)** at $161.51/month — actually $9.26 cheaper than US East ($170.77). This is driven by lower EC2 compute pricing in eu-west-2 for t4g ARM instances.

### Where Azure is Cheapest

Azure's lowest cost region is **US East** at $84.93/month. Both European and Asian regions are more expensive, primarily because the MySQL Flexible Server compute rate is slightly higher outside the US.

### Architecture Recommendation by Region

| If users are primarily in... | Recommended Provider | Reason |
|---|---|---|
| North America | Azure | 50.3% cheaper, strong database savings |
| Europe | Azure | 43.3% cheaper, database savings outweigh compute premium |
| Asia Pacific | Azure | 43.8% cheaper despite higher egress, database savings dominant |
| Multi-region global | Azure | Consistent savings across all three regions tested |

---

## Key Takeaways

1. **Azure wins in all three regions tested.** The cost advantage ranges from 43.3% (Europe) to 50.3% (US East).

2. **The database tier drives everything.** AWS RDS MySQL is 5.7x–6.3x more expensive than Azure MySQL Flexible Server regardless of region. Any architecture that includes a managed relational database will strongly favour Azure on cost.

3. **Egress is the most volatile cost driver.** Both providers charge significantly more for Asia Pacific outbound traffic. Teams serving Asian users should factor egress into total cost of ownership modelling.

4. **US East remains the cheapest region on both platforms.** Deploying in US East and using a CDN for global content delivery is the most cost-efficient architecture for globally distributed SaaS applications.

5. **Windows licensing premium is consistent globally.** Azure Hybrid Benefit saves approximately $6.72/month on VM compute across all regions — a fixed saving regardless of geography.