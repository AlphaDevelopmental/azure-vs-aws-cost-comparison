# Cross-Cloud Cost Comparison Report
## AWS vs Microsoft Azure — SaaS Application Workload

---

## 1. Executive Summary

This report presents a direct cost comparison between Amazon Web Services (AWS) and Microsoft Azure for hosting a small SaaS application requiring 2 vCPU compute, 4 GB RAM, 100 GB block storage, 20 GB managed MySQL database, 50 GB object storage, and 500 GB monthly egress — all provisioned in the US East region on both platforms.

**Verdict: Azure is 50.3% cheaper than AWS for this workload on a Linux baseline.**

| Provider | Monthly Cost | Annual Cost |
|---|---|---|
| AWS (Linux, On-Demand) | $170.77 | $2,049.24 |
| Azure (Linux, Pay-as-you-go) | $84.93 | $1,019.16 |
| Azure (Windows + Hybrid Benefit) | $91.64 | $1,099.68 |
| **Monthly savings (Azure vs AWS)** | **$85.84** | **$1,030.08** |

---

## 2. Direct Cost Matrix

| Infrastructure Component | AWS | Azure (Linux) | Azure (Windows + HB) | Key Driver |
|---|---|---|---|---|
| Compute (2 vCPU / 4 GB RAM) | $24.53 | $27.45 | $34.16 | AWS ARM instance cheaper; Azure adds Windows premium |
| Block Storage (100 GB SSD) | $8.00 | $5.89 | $5.89 | Azure S10 disk slightly cheaper |
| Managed MySQL Database (20 GB) | $92.09 | $14.71 | $14.71 | Azure Flexible Server dramatically cheaper |
| Object Storage (50 GB) | $1.15 | $2.08 | $2.08 | AWS S3 slightly cheaper |
| Network Egress (500 GB) | $45.00 | $34.80 | $34.80 | Azure Global Network 22.7% cheaper |
| **Total Monthly** | **$170.77** | **$84.93** | **$91.64** | |

---

## 3. Task 4 — Inter-Zone Data Transfer Cost Comparison

Inter-zone data transfer refers to data moving between Availability Zones (AWS) or Availability Zones (Azure) within the same region. This is a hidden cost that many teams overlook during initial architecture planning.

### AWS Inter-Zone Transfer Pricing

- **Cost:** $0.01 per GB in each direction (inbound and outbound)
- **Example:** Moving 100 GB of data between two Availability Zones in US East costs $1.00 inbound + $1.00 outbound = **$2.00**
- **Impact:** For a multi-AZ deployment with heavy cross-zone traffic (e.g., database replicas, load-balanced services), this can add $10–$50/month to a small deployment
- **Free tier:** No free inter-zone transfer on AWS

### Azure Inter-Zone Transfer Pricing

- **Cost:** $0.01 per GB for data transfer between Availability Zones within the same region
- **Example:** Moving 100 GB between zones costs **$1.00** (one direction only; Azure bills only the outbound direction)
- **Impact:** Slightly more favorable than AWS as Azure typically bills one-directional transfer; AWS bills both directions
- **Free tier:** First 100 GB of inter-zone transfer per month is free on Azure

### Comparison Summary

| Metric | AWS | Azure |
|---|---|---|
| Inter-AZ transfer rate | $0.01/GB each direction | $0.01/GB outbound only |
| Billing direction | Both inbound + outbound | Outbound only |
| Free allowance | None | 100 GB/month free |
| 100 GB transfer cost | $2.00 | $1.00 |
| 500 GB transfer cost | $10.00 | $4.00 |

**Winner: Azure** — for architectures with significant cross-zone traffic, Azure's one-directional billing and free allowance provide meaningful savings over AWS's bi-directional model.

---

## 4. Task 5 — Discount Mechanisms

Both providers offer commitment-based discounts that can significantly reduce costs compared to the on-demand/pay-as-you-go baselines used in this comparison.

### AWS Savings Plans

AWS Savings Plans are a flexible pricing model offering lower prices in exchange for a consistent usage commitment (measured in $/hour) over a 1 or 3-year term.

| Plan Type | Description | Max Discount |
|---|---|---|
| Compute Savings Plans | Applies automatically to any EC2, Fargate, or Lambda usage | Up to 66% |
| EC2 Instance Savings Plans | Specific to one instance family in one region | Up to 72% |
| SageMaker Savings Plans | Specific to SageMaker usage | Up to 64% |

**Key characteristics:**
- No upfront commitment required (no-upfront option available)
- Discount applies automatically to matching usage
- Unused commitment is forfeited — no rollover
- 1-year term: ~30-40% discount; 3-year term: ~50-66% discount
- Applied to this estimate: EC2 cost would drop from $24.53 to ~$9.08/month (3-year, no upfront)

### Azure Reserved Instances

Azure Reserved Instances (also called Azure Reservations) provide discounted rates in exchange for committing to a specific VM size, region, and term.

| Term | Typical Discount |
|---|---|
| 1-year reservation | ~41% off pay-as-you-go |
| 3-year reservation | ~62% off pay-as-you-go |

**Key characteristics:**
- Can be paid fully upfront, partially upfront, or monthly
- Reservations are exchangeable and partially refundable (cancellation fee applies)
- Scope can be set to single subscription or shared across subscriptions
- Azure Hybrid Benefit can be combined with reservations for maximum savings
- Applied to this estimate: VM cost would drop from $27.45 to ~$10.44/month (3-year reservation)

### Combined Savings Potential

| Provider | On-Demand Total | 3-Year Committed Total | Annual Saving |
|---|---|---|---|
| AWS | $170.77/month | ~$108.00/month | ~$756/year |
| Azure (Linux) | $84.93/month | ~$55.00/month | ~$359/year |

Even with commitment discounts applied, Azure maintains its cost advantage — the absolute dollar savings are larger on AWS simply because the baseline is higher.

---

## 5. Scenario Analysis

### Scenario A: Linux-Based Startup

For a bootstrapping startup running open-source workloads on Linux, **Azure is the clear winner**. The $85.84/month saving ($1,030/year) represents significant runway capital for an early-stage company. Azure's MySQL Flexible Server pricing particularly benefits startups that need a reliable managed database without enterprise-scale overhead.

### Scenario B: Microsoft-Centric Enterprise

For an enterprise already invested in the Microsoft ecosystem (Active Directory, Windows Server licenses, Microsoft 365), **Azure delivers compounding advantages** beyond raw compute pricing. Azure Hybrid Benefit eliminates the Windows OS licensing premium, Active Directory integration is native, and consolidated billing through Microsoft's Enterprise Agreement can further reduce costs. The Windows + Hybrid Benefit scenario at $91.64/month is still 46.3% cheaper than AWS.

---

## 6. Two Cost-Optimization Strategies

### Strategy 1: Adopt Commitment-Based Pricing After 3 Months of Stable Usage

Neither reserved instances nor savings plans should be purchased immediately — spend the first 3 months on pay-as-you-go to establish real usage patterns. Once patterns stabilize, commit to 1-year reserved/savings plan pricing. On Azure, this would reduce the $84.93/month baseline to approximately $55–60/month, saving an additional $25–30/month on top of the already-significant AWS savings.

### Strategy 2: Right-Size the Database Tier

The database tier is the single largest cost driver in this comparison — 53.9% of the AWS total ($92.09) and 17.3% of the Azure total ($14.71). Both providers offer smaller database tiers than what was used in this estimate. For a startup in early growth phase (fewer than 1,000 concurrent users), consider:

- **AWS:** Use Aurora Serverless v2 which scales from 0.5 ACUs and charges per second — at low traffic, total database cost could drop to $15–20/month
- **Azure:** The Flexible Server Burstable tier already represents good value; further savings come from disabling ZRS redundancy in favour of LRS during development, reducing the cost to approximately $10/month

---

## 7. Final Recommendation

| Business Type | Recommended Provider | Reason |
|---|---|---|
| Linux startup, cost-sensitive | **Azure** | 50.3% cheaper baseline, far lower database costs |
| Microsoft enterprise | **Azure** | Hybrid Benefit + native AD integration + consolidated billing |
| AWS-heavy existing infrastructure | **AWS** | Migration cost outweighs pricing difference at scale |
| Heavy machine learning workloads | **AWS** | Broader ML/AI service catalog and maturity |

For the scenario defined in this project, **Azure is recommended for both the startup and enterprise contexts**.