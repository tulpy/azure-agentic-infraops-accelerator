# WAF Research Notes (Temporary)

## Service Research Summary

### App Service (S1 Standard)

- PaaS web hosting: .NET, Java, Node.js, Python, PHP on Windows/Linux
- S1: 1 vCPU, 1.75 GB RAM, 50 GB storage, custom domain + SSL, manual scale
- SLA: 99.95% (single instance), 99.99% (zone-redundant)
- VNet integration and private endpoints available (optional)
- Built-in Entra ID authentication, managed identity support
- Auto-instrumentation for Application Insights
- ISO, SOC, PCI certified; GDPR compliant

### Azure SQL Database (Standard S1, DTU)

- S1: 20 DTU, 250 GB max storage
- SLA: 99.99% (all tiers)
- Automated backups: 1-35 day retention (default 7), PITR
- Geo-redundant/LRS/ZRS backup storage options
- Azure AD-only authentication supported
- TDE (Transparent Data Encryption) enabled by default
- Auditing and threat detection available
- DTU model: bundled CPU, memory, IO

### Key Vault (Standard)

- Secrets, keys, certificates management
- Standard: software-protected keys (FIPS 140 Level 1)
- Premium: HSM-protected (FIPS 140-3 Level 3)
- RBAC or access policy authorization
- Soft delete (90 days default), purge protection
- Logging and monitoring via Azure Monitor
- No direct cost for vault; charged per operation + secrets count

### Log Analytics Workspace (Per-GB)

- Centralized log data store for Azure Monitor
- No direct cost for workspace creation
- Charged per GB ingested + retention beyond free tier
- Free tier: 5 GB/day ingestion, 31-day retention
- Data retention: up to 12 years (long-term)
- Supports KQL queries, alerts, workbooks

### Application Insights

- APM feature of Azure Monitor (OpenTelemetry-based)
- Auto-instrumentation for App Service
- Live metrics, application map, failures/performance views
- Linked to Log Analytics workspace for data storage
- Charged via Log Analytics ingestion (Per-GB plan)
- No separate base cost

## WAF Pillar Scores

### Security: 7/10 (Confidence: High)

**Strengths:**

- Managed Identity for service-to-service auth (App Service → SQL, KV)
- Key Vault for centralized secret management
- TLS 1.2+ enforced on all services
- Entra ID for user authentication (SSO)
- Encryption at rest (platform-managed keys) on SQL + KV
- TDE enabled by default on Azure SQL
- RBAC for infrastructure access control

**Gaps:**

- No private endpoints (public endpoints exposed)
- No VNet integration for App Service
- No WAF/Application Gateway
- No network-level isolation between services
- Key Vault using Standard tier (not Premium HSM)

**Recommendations:**

- Consider private endpoints for SQL + KV in production
- Enable VNet integration for App Service in production
- Add Application Gateway with WAF v2 for production scale

### Reliability: 6/10 (Confidence: Medium)

**Strengths:**

- 99.95% App Service SLA, 99.99% SQL Database SLA
- Composite SLA meets 99.9% target (calculation: 0.9995 × 0.9999 × 0.9999 ≈ 99.93%)
- Automated SQL backups with PITR (35-day retention)
- Stateless App Service → easy redeployment from IaC
- Key Vault soft delete for secret recovery

**Gaps:**

- Single region deployment (swedencentral only)
- No failover region configured
- No availability zone redundancy
- No health probes or auto-healing defined
- RTO 4h dependent on manual recovery

**Recommendations:**

- Enable App Service health checks
- Configure SQL backup with geo-redundant storage
- Document manual recovery runbook for RTO 4h
- Consider zone-redundant deployments for production

### Performance Efficiency: 7/10 (Confidence: Medium)

**Strengths:**

- S1 handles 100-1K concurrent users adequately
- Application Insights for real-time performance monitoring
- SQL S1 (20 DTU) sufficient for ~5,000-10,000 daily transactions
- <2s page load achievable with S1 tier

**Gaps:**

- No caching layer (Redis deferred)
- No CDN for static content
- No autoscale configured (S1 manual scale only)
- No connection pooling strategy defined
- <500ms API p95 may require optimization

**Recommendations:**

- Monitor DTU usage, upgrade to S2 if >80% sustained
- Consider Azure CDN for static assets as traffic grows
- Plan Redis Cache addition at 1K+ concurrent users
- Use App Service connection pooling for SQL

### Cost Optimization: 8/10 (Confidence: High)

**Strengths:**

- Standard tiers align with €500-€2K budget
- Consumption-based monitoring (pay per GB ingested)
- No over-provisioned resources
- Clear upgrade path without re-architecture
- Free tier available for Log Analytics (5 GB/day)

**Gaps:**

- No reserved instance planning
- Fixed compute costs (App Service Plan always-on)
- No dev/test pricing consideration
- No auto-shutdown for dev environment

**Recommendations:**

- Use Dev/Test pricing for dev subscription
- Consider B1 tier for dev environment
- Monitor actual usage and right-size after 30 days
- Plan reserved instances at 12-month mark

### Operational Excellence: 7/10 (Confidence: Medium)

**Strengths:**

- Bicep IaC for repeatable deployments
- Application Insights + Log Analytics for monitoring
- Diagnostic settings for all services
- Email alert notifications configured
- Environment separation (Dev + Prod resource groups)

**Gaps:**

- No CI/CD pipeline defined
- No custom dashboards or workbooks
- No runbooks or automated remediation
- No alert severity tiers
- No deployment slots for zero-downtime deploys

**Recommendations:**

- Set up GitHub Actions or Azure DevOps for CI/CD
- Create Azure Monitor workbook for key metrics
- Document operational runbooks
- Use App Service deployment slots for production

## SKU Selection Summary

| Resource             | SKU               | Justification                                                              |
| -------------------- | ----------------- | -------------------------------------------------------------------------- |
| App Service Plan     | S1 Standard       | 1 vCPU, 1.75 GB RAM; fits balanced tier; custom domain + SSL; manual scale |
| Web App              | On S1 plan        | .NET/Node.js/Python; managed identity enabled                              |
| Azure SQL Database   | Standard S1 (DTU) | 20 DTU, 250 GB; 99.99% SLA; automated backups; TDE                         |
| Key Vault            | Standard          | Software-protected keys; RBAC; soft delete; sufficient for non-HSM needs   |
| Log Analytics        | Per-GB plan       | Pay per ingestion; 5 GB/day free; 31-day default retention                 |
| Application Insights | Workspace-based   | Linked to Log Analytics; no separate base cost                             |

## Resource List for Pricing (send to cost-estimate-subagent)

1. App Service Plan S1, swedencentral, 1 instance, Windows
2. Azure SQL Database Standard S1, 20 DTU, swedencentral
3. Key Vault Standard, ~10,000 operations/month
4. Log Analytics workspace, ~5 GB/month ingestion
5. Application Insights, ~5 GB/month (included in Log Analytics)
