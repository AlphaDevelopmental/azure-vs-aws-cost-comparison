# Business Justification — Cloud Provider Selection

## Scenario Context

This justification evaluates two distinct business contexts for the same SaaS infrastructure: a Linux-based startup and a Microsoft-centric enterprise. Both contexts use identical technical specifications — 2 vCPU compute, 4 GB RAM, managed MySQL database (20 GB), object storage (50 GB), and 500 GB monthly egress — priced against AWS and Azure in the US East region.

---

## Context 1: Linux-Based Startup

For a bootstrapping SaaS startup operating on open-source tooling and a lean engineering team, **Microsoft Azure is the recommended platform**, delivering a 50.3% reduction in monthly infrastructure overhead compared to AWS ($84.93 vs $170.77).

The defining cost differential is the managed database tier. AWS RDS for MySQL charges $92.09 per month for its smallest viable production configuration — representing 53.9% of the total AWS bill. Azure's equivalent offering, the MySQL Flexible Server on the Burstable tier, delivers comparable reliability and managed patching for just $14.71 per month. For a startup where every dollar of infrastructure spend is a dollar not invested in product and growth, this $77.38 monthly difference is material.

Azure's network egress pricing also favours startups with API-heavy traffic patterns. At $34.80 for 500 GB versus AWS's $45.00, Azure provides 22.7% cheaper data distribution costs — savings that compound as user volume grows.

Finally, Azure's generous free tier (12 months of free VM usage, always-free services, and $200 credit) gives early-stage teams room to prototype without premature infrastructure commitment.

**Recommended platform: Azure. Estimated annual saving over AWS: $1,030.08.**

---

## Context 2: Microsoft-Centric Enterprise

For an enterprise organization already standardized on the Microsoft technology stack — including Windows Server, Active Directory, Microsoft 365, and existing Volume Licensing agreements — **Azure delivers compounding advantages that extend well beyond raw compute pricing**.

The Azure Hybrid Benefit program allows organizations covered under Software Assurance to apply their existing Windows Server licenses directly to Azure VMs, eliminating the $6.72/month OS licensing premium per instance. At scale, across dozens or hundreds of VMs, this benefit alone can generate six-figure annual savings.

Integration depth is equally important. Azure Active Directory (now Microsoft Entra ID) provides native single sign-on across Azure resources, Microsoft 365, and third-party SaaS applications — eliminating the federation complexity and additional tooling costs that would be required to achieve the same on AWS. For enterprises running hybrid environments with on-premises datacenters, Azure Arc and Azure ExpressRoute provide seamless connectivity options with pricing structures designed for enterprise volume.

Consolidated billing through Microsoft's Enterprise Agreement also enables predictable, negotiated pricing across Azure, Microsoft 365, and Dynamics 365 — simplifying procurement, audit compliance, and budget forecasting.

**Recommended platform: Azure. Primary drivers: Hybrid Benefit licensing savings, native Microsoft ecosystem integration, and Enterprise Agreement consolidation.**

---

## Summary

In both business contexts evaluated, Azure presents a stronger financial and operational case than AWS for this workload profile. The cost advantage is largest for startups (50.3% saving), while enterprises gain additional strategic value through licensing synergies and deep Microsoft ecosystem integration.