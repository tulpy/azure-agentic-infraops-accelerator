<!-- markdownlint-disable MD033 MD041 -->

<a id="readme-top"></a>

<div align="center">

![Status](https://img.shields.io/badge/Status-In%20Progress-yellow?style=for-the-badge)
![Step](https://img.shields.io/badge/Step-2%20of%207-blue?style=for-the-badge)

# 🏗️ my-webapp

**Simple web application with App Service, Azure SQL Database, and Key Vault on Azure**

[View Architecture](#-architecture) · [View Artifacts](#-generated-artifacts) · [View Progress](#-workflow-progress)

</div>

---

## 📋 Project Summary

| Property           | Value               |
| ------------------ | ------------------- |
| **Created**        | 2026-03-12          |
| **Last Updated**   | 2026-03-12          |
| **Region**         | swedencentral       |
| **Environment**    | Dev, Production     |
| **Estimated Cost** | ~$117/month (~€108) |
| **IaC Tool**       | Bicep               |

---

## ✅ Workflow Progress

```text
[██░░░░░░░░] 29% Complete
```

| Step | Phase          |                                    Status                                     | Artifact                                                         |
| :--: | -------------- | :---------------------------------------------------------------------------: | ---------------------------------------------------------------- |
|  1   | Requirements   |     ![Done](https://img.shields.io/badge/-Done-success?style=flat-square)     | [01-requirements.md](./01-requirements.md)                       |
|  2   | Architecture   |     ![Done](https://img.shields.io/badge/-Done-success?style=flat-square)     | [02-architecture-assessment.md](./02-architecture-assessment.md) |
|  3   | Design         | ![Pending](https://img.shields.io/badge/-Pending-lightgrey?style=flat-square) | 03-des-\*.md                                                     |
| 3.5  | Governance     | ![Pending](https://img.shields.io/badge/-Pending-lightgrey?style=flat-square) | 04-governance-constraints.md                                     |
|  4   | Planning       | ![Pending](https://img.shields.io/badge/-Pending-lightgrey?style=flat-square) | 04-implementation-plan.md                                        |
|  5   | Implementation | ![Pending](https://img.shields.io/badge/-Pending-lightgrey?style=flat-square) | 05-implementation-reference.md                                   |
|  6   | Deployment     | ![Pending](https://img.shields.io/badge/-Pending-lightgrey?style=flat-square) | 06-deployment-summary.md                                         |
|  7   | Documentation  | ![Pending](https://img.shields.io/badge/-Pending-lightgrey?style=flat-square) | 07-documentation-index.md                                        |

> **Legend**:
> ![Done](https://img.shields.io/badge/-Done-success?style=flat-square) Complete
> | ![WIP](https://img.shields.io/badge/-WIP-yellow?style=flat-square) In Progress
> | ![Pending](https://img.shields.io/badge/-Pending-lightgrey?style=flat-square) Pending
> | ![Skip](https://img.shields.io/badge/-Skipped-blue?style=flat-square) Skipped

---

## 🏛️ Architecture

Architecture diagram will be generated in Step 3 (Design).

### Key Resources

| Resource          | Type             | SKU         | Purpose                 |
| ----------------- | ---------------- | ----------- | ----------------------- |
| app-mywebapp-dev  | App Service      | S1 Standard | Web frontend            |
| sql-mywebapp-dev  | Azure SQL Server | S1 Standard | Relational data storage |
| kv-myweb-dev-\*   | Key Vault        | Standard    | Secrets management      |
| log-mywebapp-dev  | Log Analytics    | Per-GB      | Centralized logging     |
| appi-mywebapp-dev | App Insights     | —           | Application monitoring  |

---

## 📄 Generated Artifacts

<details open>
<summary><strong>📁 Step 1-3: Requirements, Architecture & Design</strong></summary>

| File                                                             | Description                    |                                Status                                 | Created    |
| ---------------------------------------------------------------- | ------------------------------ | :-------------------------------------------------------------------: | ---------- |
| [01-requirements.md](./01-requirements.md)                       | Project requirements with NFRs | ![Done](https://img.shields.io/badge/-Done-success?style=flat-square) | 2026-03-12 |
| [02-architecture-assessment.md](./02-architecture-assessment.md) | WAF assessment + cost estimate | ![Done](https://img.shields.io/badge/-Done-success?style=flat-square) | 2026-03-12 |
| [03-des-cost-estimate.md](./03-des-cost-estimate.md)             | Detailed cost breakdown        | ![Done](https://img.shields.io/badge/-Done-success?style=flat-square) | 2026-03-12 |

</details>

---

## 🔗 Related Resources

| Resource            | Path                                                       |
| ------------------- | ---------------------------------------------------------- |
| **Bicep Templates** | [`infra/bicep/my-webapp/`](../../infra/bicep/my-webapp/)   |
| **Workflow Docs**   | [`docs/workflow.md`](../../docs/workflow.md)               |
| **Troubleshooting** | [`docs/troubleshooting.md`](../../docs/troubleshooting.md) |

---

<div align="center">

**Generated by [Agentic InfraOps](../../README.md)** · [Report Issue](https://github.com/jonathan-vella/azure-agentic-infraops/issues/new)

<a href="#readme-top">⬆️ Back to Top</a>

</div>
