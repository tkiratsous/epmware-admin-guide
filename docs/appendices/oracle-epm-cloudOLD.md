# Oracle EPM Cloud Configuration Requirements

This appendix provides detailed configuration requirements for linking EPMware to Oracle EPM Cloud applications, enabling hierarchy import and direct metadata deployment.

## Overview

EPMware integrates seamlessly with Oracle EPM Cloud applications through REST APIs, providing automated metadata management across your cloud EPM landscape. This guide covers configuration for PBCS, FCCS, TRCS, ARCS, and PCMCS applications.

## Supported Applications

<div class="grid cards">
  <div class="card">
    <h3>📊 PBCS</h3>
    <p><strong>Planning & Budgeting Cloud Service</strong><br/>
    Full planning application support with dimension management</p>
  </div>
  
  <div class="card">
    <h3>💰 FCCS</h3>
    <p><strong>Financial Consolidation & Close Cloud Service</strong><br/>
    Consolidation hierarchies and close management</p>
  </div>
  
  <div class="card">
    <h3>📋 TRCS</h3>
    <p><strong>Tax Reporting Cloud Service</strong><br/>
    Tax provision and reporting hierarchies</p>
  </div>
  
  <div class="card">
    <h3>✅ ARCS</h3>
    <p><strong>Account Reconciliation Cloud Service</strong><br/>
    Reconciliation profiles and hierarchies</p>
  </div>
  
  <div class="card">
    <h3>📈 PCMCS</h3>
    <p><strong>Profitability & Cost Management Cloud Service</strong><br/>
    Cost allocation and profitability dimensions</p>
  </div>
</div>

---

## Configuration Workflow

```mermaid
graph LR
    A[Oracle EPM Cloud] --> B[Create Snapshots]
    B --> C[Setup Import Jobs]
    C --> D[Configure EPMware]
    D --> E[Test Integration]
    E --> F[Production Ready]
```

---

## Step 1: Configure Metadata Import

### Create LCM Export Snapshot

Enable EPMware to import metadata from your Oracle EPM Cloud application.

#### For PBCS/FCCS/TRCS/ARCS

1. **Access Migration**
   - Log into Oracle EPM Cloud application
   - Navigate to **Tools → Migration**

2. **Select Application Artifacts**
   - Click on your application name
   - Select all artifacts **EXCEPT**:
     - ❌ Essbase Data
     - ❌ Data Management Staging Data
     - ❌ Planning Unit Hierarchy

3. **Create Export**
   - Click **Export** icon
   - Name: `EW_LCM_EXPORT`
   - Click **Export**

!!! important "Snapshot Name"
    The export name **MUST** be `EW_LCM_EXPORT` to match EPMware's default configuration.

#### For PCMCS

1. **Access Application Migration**
   - Navigate to **Applications → Migration**
   - Select your PCMCS application

2. **Export Configuration**
   - Select all artifacts except Essbase Data
   - Export name: `EW_LCM_EXPORT`
   - Create export

### Application Properties Reference

Configure these properties in EPMware under **Configuration → Applications → Properties**:

| Property | Default Value | Description |
|----------|---------------|-------------|
| `PBCS_LCM_SNAPSHOT_NAME` | EW_LCM_EXPORT | Snapshot name for import |
| `PBCS_LCM_EXPORT_URL` | Auto-generated | REST API endpoint for export |
| `PBCS_APP_VERSION` | 11.1.2.3.600 | API version (do not modify) |

---

## Step 2: Configure Metadata Deployment

### Create Import Jobs

Set up import jobs for each dimension managed by EPMware.

#### Job Creation Process

1. **Access Dimensions**
   - Navigate to **Application → Overview → Dimensions**
   - Click **Import** icon

2. **Configure Import Settings**
   
   | Setting | Value | Required |
   |---------|-------|----------|
   | **Location** | Inbox | ✅ |
   | **Clear Members** | Checked | ✅ |
   | **Import File** | See naming convention | ✅ |
   | **Refresh Database** | Checked | ✅ |

3. **File Naming Convention**

   ```
   Dimensions: EW_IMPORT_<DIMENSION_NAME>.csv
   UDAs:       EW_IMPORT_UDA_<DIMENSION_NAME>.csv
   ```

   !!! warning "Case Sensitivity"
       File names are **case-sensitive**. Use UPPERCASE except for the `.csv` extension.

4. **Save as Job**
   - Job Name: `EW_IMPORT_<DIMENSION_NAME>`
   - Enable "Refresh Database if Import Metadata is successful"
   - Save

### Example Import Jobs

Create separate jobs for each dimension:

| Dimension | Import File | Job Name |
|-----------|------------|----------|
| Account | EW_IMPORT_ACCOUNT.csv | EW_IMPORT_ACCOUNT |
| Entity | EW_IMPORT_ENTITY.csv | EW_IMPORT_ENTITY |
| Product | EW_IMPORT_PRODUCT.csv | EW_IMPORT_PRODUCT |
| Account UDA | EW_IMPORT_UDA_ACCOUNT.csv | EW_IMPORT_UDA_ACCOUNT |

---

## Step 3: EPMware Configuration

### Application Setup

1. **Create Application**
   ```
   Configuration → Applications → Configuration
   - Application Type: Select cloud EPM type
   - Target Application: Cloud app name
   - Deployment: Direct
   ```

2. **Configure Properties**
   
   Essential properties for cloud integration:

   | Property Category | Properties |
   |-------------------|------------|
   | **Connection** | PBCS_SERVER_URL, PBCS_TENANT_NAME, PBCS_DATA_CENTER |
   | **Application** | PBCS_APP_NAME, PBCS_SERVICE_NAME |
   | **Import/Export** | PBCS_LCM_SNAPSHOT_NAME, PBCS_LCM_EXPORT_URL |
   | **Deployment** | PBCS_DEPLOY_JOB_NAME, PBCS_DEPLOY_JOB_FILE_NAME |

### URL Configuration

#### Server URL Format
```
https://<SERVICE_NAME>-<TENANT_NAME>.pbcs.<DATA_CENTER>.oraclecloud.com
```

#### Example URLs

| Service | URL Pattern |
|---------|-------------|
| **PBCS** | `https://planning-test-abc123.pbcs.us2.oraclecloud.com` |
| **FCCS** | `https://consolidation-abc123.fccs.us6.oraclecloud.com` |
| **TRCS** | `https://tax-abc123.trcs.us2.oraclecloud.com` |

### Data Center Codes

| Region | Code | Description |
|--------|------|-------------|
| US Commercial | us2, us6 | North America |
| EU Frankfurt | em2 | Europe |
| EU Amsterdam | em3 | Europe |
| APAC Sydney | ap1 | Asia Pacific |

---

## Testing & Validation

### Connection Testing

1. **Test Server Connection**
   ```
   Configuration → Infrastructure → Servers
   - Select cloud server
   - Click "Test Connection"
   - Verify success message
   ```

2. **Import Test**
   - Use Application Import with Auto Import
   - Verify hierarchies load correctly
   - Check import status and logs

3. **Deployment Test**
   - Create test request with minimal changes
   - Deploy through workflow
   - Verify in target application

### Validation Checklist

- [ ] Server connection successful
- [ ] LCM snapshot accessible
- [ ] Import jobs created for all dimensions
- [ ] Application properties configured
- [ ] Test import completes successfully
- [ ] Test deployment updates target
- [ ] Audit logs capture activities

---

## Application-Specific Configuration

### FCCS Special Configuration

Additional properties for HFM to FCCS migrations:

| Property | Description | Example |
|----------|-------------|---------|
| `HFM_LEGACY_DIM_MAP_ACCOUNT` | HFM Account dimension name | Account |
| `HFM_LEGACY_DIM_MAP_ENTITY` | HFM Entity dimension name | Entity |
| `HFM_LEGACY_DIM_MAP_CUSTOM1` | HFM Custom1 dimension name | Product |
| `HFM_LEGACY_TOP_NODE_PREFIX` | Prefix for legacy nodes | HFM_Legacy_ |

### PCMCS Configuration

!!! note "PCMCS Deployment"
    PCMCS deployments are handled through the EPMware Agent. No import job configuration is required in PCMCS.

Key differences:
- No import job setup needed
- Agent-based deployment
- Supports POV-specific deployments

---

## Troubleshooting

### Common Issues & Solutions

| Issue | Error Message | Solution |
|-------|---------------|----------|
| **Connection Failed** | HTTP 401 Unauthorized | Verify username/password and user permissions |
| **Bad Request** | HTTP 400 Bad Request | Check application name, data center, and URL format |
| **Forbidden** | HTTP 403 Forbidden | User lacks required application role |
| **Import Timeout** | Timeout exceeded | Increase timeout in Global Settings |
| **Job Not Found** | Import job not found | Verify job name matches exactly (case-sensitive) |

### Debug Checklist

1. **Verify Credentials**
   - Test login directly in Oracle EPM Cloud
   - Confirm user has Service Administrator role
   - Check password for special characters

2. **Validate URLs**
   - Confirm data center code
   - Verify tenant name
   - Check service name

3. **Review Job Configuration**
   - Confirm file names are uppercase
   - Verify .csv extension is lowercase
   - Check "Clear Members" is enabled

---

## Best Practices

### Security
- ✅ Use dedicated service account
- ✅ Apply principle of least privilege
- ✅ Rotate passwords regularly
- ✅ Enable audit logging

### Performance
- ✅ Schedule imports during off-peak hours
- ✅ Batch deployments when possible
- ✅ Monitor API rate limits
- ✅ Optimize dimension sizes

### Maintenance
- ✅ Document all configurations
- ✅ Test after Oracle monthly updates
- ✅ Keep EPMware updated
- ✅ Regular backup of configurations

---

## Quick Reference

### REST API Endpoints

| Operation | Endpoint Pattern |
|-----------|-----------------|
| **LCM Export** | `/interop/rest/{version}/applicationsnapshots/{snapshot}/migration?q={type:export}` |
| **Job Execution** | `/HyperionPlanning/rest/v3/applications/{app}/jobs` |
| **Job Status** | `/HyperionPlanning/rest/v3/applications/{app}/jobs/{jobId}` |

### Required Oracle Roles

| Role | Required For |
|------|--------------|
| Service Administrator | Full integration |
| Power User | Limited deployment |
| User | Read-only access |

---

## Additional Resources

### Related Topics
- [Application Configuration](../configuration/applications.md)
- [Application Properties](../configuration/applications.md#application-properties)
- [Deployment Configuration](../deployment/index.md)

### Oracle Documentation
- [Oracle EPM Cloud REST API Guide](https://docs.oracle.com/en/cloud/saas/enterprise-performance-management-common/prest/)
- [EPM Automate Utility](https://docs.oracle.com/en/cloud/saas/enterprise-performance-management-common/cepma/)
- [Migration Best Practices](https://docs.oracle.com/en/cloud/saas/enterprise-performance-management-common/epmss/)

---

## Support

For Oracle EPM Cloud integration assistance:

📧 **EPMware Support**: support@epmware.com  
📞 **Phone**: 408-614-0442  
🌐 **Oracle Support**: [support.oracle.com](https://support.oracle.com)

!!! tip "Monthly Updates"
    Oracle EPM Cloud receives monthly updates. Test your integration after each update cycle to ensure compatibility.