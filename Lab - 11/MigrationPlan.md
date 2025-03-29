**Tailwind OpenCare - Patient Self-Booking System Migration PLan to Microsoft Azure**
## 1. Discovery and Tooling Setup
### Tools for Discovery 
- Using **Azure migrate** for Discovery and Assessment tool.
- Using the **Azure Migrate appliance**(agentless or agent-based) for on-prem servers initial discovery.
- Using **Service Map** for understanding the service connectivity and **Dependency Visualization** with Azure Migrate.

### Data to be Collected
- Operating System details (Ubuntu versions)
- Listing all the installed software for example Node.js, NGINX, PostgreSQL, HAProxy, Redis etc.
- Utilizing the network and memory, CPU and Disk I/O.
- Frontend-to-backend, backend-to-cache/database inter-server dependencies
- Backup configurations

### Secure Credentials and Permissions Management
- In Azure Key Vault storing securely the SSH Keys, credentials and secrets.
- Based on **RBAC (Role-Based Access Control)** restriction to access of migration utilities and resources.
- Activating the **Multi-Factor Authentication (MFA)** for all sign-in accounts that are authenticated to Azure portal.

## 2. Planning for Assessment

### Azure Migrate Assessment Settings
- **Collection of performance history**: 30 days to ensure correct sizing.
- **Sizing**: Based on performance, not simply current VM size.
- **Costing**: Based on chosen Azure region and offer type (e.g., pay-as-you-go or reserved instances).

### Target Azure Setup
- **Azure Region**: Canada Central (to satisfy local compliance and latency needs)
- **Compute Type**: Azure Virtual Machines (D-series VMs for app servers, E-series for PostgreSQL)
- **Storage Type**:
  - **Premium SSD** for PostgreSQL and Redis
  - **Standard SSD** for Node.js and NGINX
  - **Standard HDD** for backup archive storage

### Stakeholder Validation
- Present assessment reports to app owners and infrastructure leads.
- Verify recommended sizing, estimated budgets, and schedules.
- Confirm SLAs and target performance limits.

## 3. Dependency Analysis and Optimization

### Dependency Mapping
- Use **agentless discovery** for low-impact mapping, and utilize **Service Map** to see connections.
- For deeper analysis, install **Log Analytics agent** on mission-critical servers for agent-based mapping.

### Cleaning Dependency Data
- Eliminate system-level dependencies (e.g., NTP, SSH).
- Focus on app-specific flows (NGINX → Node.js → PostgreSQL/Redis).

### Key Metrics
- **Criticality**: All servers are production-critical.
- **User Base**: Patients and administrative staff in North America.
- **SLA**: 99.95% uptime, < 2 hours downtime during migration.
- **Backup Requirements**:
  - Daily snapshot backups for DB and Redis.
  - Long-term backup storage (30-day retention).

## 4. Server Grouping and Migration Waves
### Logical Server Groupings
- **Frontend Group**: NGINX web servers
- **Backend Group**: Node.js API servers
- **Data Group**: PostgreSQL and Redis
- **Load Balancer Group**: HAProxy

### Migration Waves
- **Wave 1**: Redis + PostgreSQL (migrate and test backend connectivity)
- **Wave 2**: Node.js API servers (point to new Redis and DB)
- **Wave 3**: NGINX frontends (final user-facing migration)
- **Wave 4**: HAProxy (replaced with Azure Load Balancer or Application Gateway)

### Firewall, LB, IP Considerations
- Ensure firewall rules permit communication in the new VNet.
- Map existing static IPs to Azure private IPs or use DNS-based redirection.
- Reconfigure HAProxy or replace with **Azure Application Gateway with WAF**.

## 5. Migration Plan Documentation

### Step-by-Step Migration Plan

1. **Pre-Migration**
   - Install Azure Migrate appliance and collect assessment data.
   - Confirm app dependencies and segment servers.
   - Provision VMs and managed services (Azure DB for PostgreSQL, Azure Cache for Redis).
   - Configure Azure Backup and Key Vault.
   - Install Azure Application Gateway or Load Balancer.

2. **Data Replication**
- Using **Azure Database Migration Service (DMS)** to replicate PostgreSQL data.
   - Redis data migration using **redis-cli --rdb**.
   - Sync application data and test connectivity.

3. **DNS and IP Transition**
   - Update DNS entries to point to Azure frontends.
   - Use short TTL during migration for quick DNS propagation.

4. **Cutover**
- Schedule 2-hour migration window (off-peak).
   - Disable HAProxy routing to old infra.
   - Validate functionality in Azure environment.
   - Switch DNS and confirm minimal downtime.

5. **Post-Migration**
   - Run integration and load testing.
   - Monitor performance via **Azure Monitor** and **Log Analytics**.
   - Enable daily automated backups.
   - Decommission old on-prem systems.

### Application Owner Role
- Validate applications before and after migration.
- Perform smoke testing and user acceptance testing.
- Sign-off before decommissioning.

