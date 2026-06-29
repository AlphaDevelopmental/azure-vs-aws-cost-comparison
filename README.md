# AWS vs Azure Cost Comparison — SaaS Application Workload

This repository contains a comprehensive cloud cost comparison between Amazon Web Services (AWS) and Microsoft Azure for hosting a small SaaS application. The analysis covers compute, storage, database, and networking costs across both platforms, including discount mechanisms and inter-zone transfer pricing.

## Scenario

A small SaaS startup running a customer-facing API with a managed MySQL database backend, evaluated across two business contexts: a Linux-based startup and a Microsoft-centric enterprise with existing Windows Server licenses.

## Infrastructure Specifications

| Component | Specification |
|---|---|
| Compute | 2 vCPU, 4 GB RAM, 24/7 uptime (730 hrs/month) |
| Block Storage | 100 GB SSD (General Purpose) |
| Database | Managed MySQL, 20 GB, smallest production tier |
| Object Storage | 50 GB |
| Network Egress | 500 GB/month outbound |
| Region | US East (N. Virginia / East US) |

## Cost Summary

| Provider | Scenario | Monthly Cost | Annual Cost |
|---|---|---|---|
| AWS | Linux, On-Demand | $170.77 | $2,049.24 |
| Azure | Linux, Pay-as-you-go | $84.93 | $1,019.16 |
| Azure | Windows + Hybrid Benefit | $91.64 | $1,099.68 |

**Azure saves $85.84/month ($1,030.08/year) over AWS on the Linux baseline.**

## Repository Structure

| File | Description |
|---|---|
| `app-specs.md` | Fixed infrastructure specifications used as the comparison baseline |
| `aws-cost-report.md` | Detailed AWS cost breakdown with share link |
| `azure-cost-report.md` | Detailed Azure cost breakdown — Linux and Windows scenarios |
| `comparison-report.md` | Full comparison including inter-zone transfer (Task 4) and discount mechanisms (Task 5) |
| `business-justification.md` | ~400 word provider justification for startup and enterprise contexts |
| `screenshots/` | Calculator configuration screenshots for both providers |

## Calculator Links

- **AWS Estimate:** https://calculator.aws/#/estimate?id=ce8ad84b841c0153a49c4d55b113f33553000541
- **Azure Estimate (Linux):** https://azure.com/e/f13f8e56174346b2b890b72982938793

## Key Findings

The dominant cost driver difference between providers is the **managed database tier**. AWS RDS for MySQL costs $92.09/month versus Azure MySQL Flexible Server at $14.71/month — a 6.3x price difference that accounts for the majority of Azure's overall cost advantage. Azure also provides cheaper network egress at $34.80 versus AWS's $45.00 for 500 GB.

For both a Linux startup and a Microsoft-centric enterprise, Azure is the recommended platform based on this workload profile and region selection.

---

**Author:** Taiwo Ajani
**Platform comparison:** Amazon Web Services vs Microsoft Azure
**Tooling:** AWS Pricing Calculator, Azure Pricing Calculator
## Regional Analysis
See `regional-price-analysis.md` for full cost comparison across US East, Europe (London), and Asia Pacific (Singapore).
