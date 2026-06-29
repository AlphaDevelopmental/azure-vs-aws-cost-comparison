# AWS Cost Report — SaaS Application Workload

## 1. Calculator Metadata

- **Estimate Share Link:** https://calculator.aws/#/estimate?id=ce8ad84b841c0153a49c4d55b113f33553000541
- **Region:** US East (N. Virginia)
- **Currency:** USD ($)
- **Pricing Model:** On-Demand (no commitment discounts applied)
- **Estimate Date:** June 2026

---

## 2. Granular Cost Breakdown

### A. Compute: Amazon EC2

- **Instance Type:** `t4g.medium` (2 vCPU, 4 GiB RAM)
- **Billing Model:** On-Demand, 100% Utilization (730 hours/month)
- **Operating System:** Linux (Ubuntu)
- **Tenancy:** Shared Instances
- **EBS Storage:** 100 GB General Purpose SSD (gp3)
- **Monthly Cost:** $32.53

### B. Managed Database: Amazon RDS for MySQL

- **Deployment Option:** Single-AZ
- **Instance Class:** db.t3.micro
- **Storage:** 20 GB General Purpose SSD (gp2)
- **Utilization:** 730 hours/month (24/7)
- **Billing Model:** On-Demand
- **Monthly Cost:** $92.09

### C. Object Storage: Amazon S3

- **Storage Class:** S3 Standard
- **Capacity:** 50 GB
- **Region:** US East (N. Virginia)
- **Monthly Cost:** $1.15

### D. Networking: AWS Data Transfer

- **Traffic Type:** Outbound to Internet (Egress)
- **Volume:** 500 GB/month
- **Monthly Cost:** $45.00

---

## 3. Total Estimated AWS Cost

| Component | Monthly Cost |
|---|---|
| Amazon EC2 (t4g.medium + 100GB EBS, Linux) | $32.53 |
| Amazon RDS for MySQL (db.t3.micro, 20GB) | $92.09 |
| Amazon S3 (50GB Standard) | $1.15 |
| AWS Data Transfer (500GB egress) | $45.00 |
| **Total Monthly** | **$170.77** |
| **Total Annual** | **$2,049.24** |

---

## 4. Key Cost Observations

The dominant cost driver on AWS is the **managed database tier**, which accounts for 53.9% of the total monthly bill ($92.09 of $170.77). This is a significant finding — even the smallest production-ready RDS instance carries a substantial minimum cost that disproportionately impacts small startup deployments.

The EC2 compute cost ($32.53 including 100GB EBS storage) is competitive and the `t4g.medium` ARM-based instance offers strong price-to-performance value for Linux workloads. The egress pricing ($45.00 for 500GB) follows AWS's standard tiered model at $0.09/GB after the first 100GB free.