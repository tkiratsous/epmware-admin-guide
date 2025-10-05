# OneStream Configuration

This appendix provides detailed configuration requirements for linking EPMware to OneStream XF applications, enabling hierarchy import and direct metadata deployment through REST APIs.

![OneStream Integration Overview](../assets/images/appendices/onestream-integration-overview.png)
*OneStream XF integration architecture with EPMware*

## Overview

EPMware integrates with OneStream XF through REST APIs and custom business rules, providing automated metadata management and deployment capabilities. This guide covers the complete configuration process from initial setup to production deployment.

## Prerequisites

Before beginning configuration, ensure you have:

- ✅ OneStream XF 5.0 or later
- ✅ Administrative access to OneStream
- ✅ EPMware application access
- ✅ EPMWARE.dll file (provided by EPMware)
- ✅ Okta or OIS authentication configured

---

## Part 1: Import OneStream Application

### Required Extract Files

To import a OneStream application into EPMware, extract the following artifacts:

1. **Application Properties** - `ApplicationProperties.xml`
2. **Workflow Channels** - `WorkflowChannels.xml` 
3. **Metadata** - `<AppName>_Metadata.xml`
4. **Security Groups** - `Security_Groups.xml`

### Extract Application Artifacts

#### Step 1: Access Application Tools

1. Login to OneStream application
2. Select **Application** tab
3. Navigate to **Tools → Load/Extract**

![OneStream Application Tab](../assets/images/appendices/onestream-application-tab.png)
*OneStream application tab with Load/Extract tools*

#### Step 2: Extract Application Properties

1. Select **Application Properties** from dropdown
2. Click **Extract** icon
3. Save as `ApplicationProperties.xml`

![Extract Application Properties](../assets/images/appendices/onestream-extract-app-properties.png)
*Extracting Application Properties to XML file*

#### Step 3: Extract Metadata

1. Select **Metadata** from dropdown
2. Expand and select:
   - ✅ Business Rules
   - ✅ Dimensions
3. Click **Extract** icon
4. Save as `<AppName>_Metadata.xml`

![Extract Metadata Selection](../assets/images/appendices/onestream-extract-metadata.png)
*Metadata extraction with Business Rules and Dimensions selected*

#### Step 4: Extract Workflow Channels

1. Select **Workflow Channels** from dropdown
2. Click **Extract** icon
3. Save as `WorkflowChannels.xml`

### Extract Security Artifacts

1. Select **Security** tab
2. Navigate to **Tools → Load/Extract**
3. Select **Security** from dropdown
4. Choose **Security Groups**
5. Extract as `Security_Groups.xml`

![Security Groups Extraction](../assets/images/appendices/onestream-extract-security-groups.png)
*Security Load/Extract screen with Security Groups selected*

### Create Import ZIP File

Package all extracted files:

```
onestream_import.zip
├── ApplicationProperties.xml
├── WorkflowChannels.xml
├── GolfStream_Metadata.xml
└── Security_Groups.xml
```

![ZIP File Structure](../assets/images/appendices/onestream-zip-structure.png)
*Required file structure for EPMware import*

---

## Part 2: Configure OneStream for Deployment

### Create Business Rule

#### Step 1: Access Business Rules

1. Navigate to **Application → Tools → Business Rules**
2. Click **New Business Rule** icon
3. Select **Extender** type
4. Name: `EPMWARE_DataMgmt`

![Create Business Rule](../assets/images/appendices/onestream-create-business-rule.png)
*Creating new Extender business rule for EPMware*

#### Step 2: Configure Properties

1. Select **Properties** tab
2. Add Referenced Assembly: `XF\EPMWARE.dll`
3. Save configuration

![Business Rule Properties](../assets/images/appendices/onestream-business-rule-properties.png)
*Business Rule Properties with EPMWARE.dll reference*

#### Step 3: Add Formula Code

1. Select **Formula** tab
2. Copy the provided VB.NET code
3. Paste into formula editor
4. Save business rule

![Business Rule Formula](../assets/images/appendices/onestream-business-rule-formula.png)
*EPMWARE_DataMgmt business rule formula editor*

<details>
<summary>Click to view complete business rule code</summary>

```vbnet
Imports System
Imports System.Data
Imports System.Collections.Generic
Imports OneStream.Shared.Common
Imports OneStream.Finance.Engine
Imports OneStream.BusinessRule.Extender.EPMWARE_DLL

Namespace OneStream.BusinessRule.Extender.EPMWARE_DataMgmt
    Public Class MainClass
        Public Function Main(ByVal si As SessionInfo, _
                           ByVal globals As BRGlobals, _
                           ByVal api As Object, _
                           ByVal args As ExtenderArgs) As Object
            Try
                Dim MainClass As New EWMainClass()
                Return MainClass.Main(si, globals, api, args)
            Catch ex As Exception
                Throw ErrorHandler.LogWrite(si, New XFException(si, ex))
            End Try
        End Function
    End Class
End Namespace
```

</details>

!!! warning "Code Formatting"
    Remove any page numbers if they appear when copying from documentation.

---

### Create Data Management Configuration

#### Step 1: Create Data Management Group

1. Navigate to **Application → Tools → Data Management**
2. Click **New Data Management Group** icon
3. Name: `EPMWARE Metadata Adapter`
4. Save

![Create Data Management Group](../assets/images/appendices/onestream-create-dm-group.png)
*Creating EPMWARE Metadata Adapter data management group*

#### Step 2: Create Sequence

1. Select **EPMWARE Metadata Adapter** group
2. Click **Create Sequence** icon
3. Name: `Deploy Metadata`
4. Save

![Create Deploy Sequence](../assets/images/appendices/onestream-create-sequence.png)
*Creating Deploy Metadata sequence*

#### Step 3: Create and Configure Step

1. Click **Step** icon
2. Select **Execute Business Rule**
3. Language: Visual Basic (VB)
4. Name: `Deploy Metadata`
5. Assign business rule: `EPMWARE_DataMgmt`

![Create Deployment Step](../assets/images/appendices/onestream-create-step.png)
*Execute Business Rule step configuration dialog*

![Assign Business Rule to Step](../assets/images/appendices/onestream-assign-business-rule.png)
*Assigning EPMWARE_DataMgmt business rule to step*

#### Step 4: Assign Step to Sequence

1. Select **Deploy Metadata** sequence
2. Navigate to **Sequence Steps** tab
3. Click **+** to add step
4. Select **Deploy Metadata** step
5. Save

![Assign Step to Sequence](../assets/images/appendices/onestream-assign-step-sequence.png)
*Assigning Deploy Metadata step to sequence*

---

## Part 3: Configure Authentication

### Create REST API User

1. Navigate to **System → Administration → Security**
2. Click **New User** icon
3. Configure user:
   - Name: `REST API`
   - Add to **Administrators** group
   - External Auth Provider: **Okta**
   - Internal Password: Set secure password

![Create REST API User](../assets/images/appendices/onestream-create-api-user.png)
*Creating REST API user with administrator privileges*

### Authentication Options

#### Option 1: Okta Configuration

Configure these properties in EPMware:

| Property | Description | Source |
|----------|-------------|--------|
| `OS_REST_API_CLIENT_ID` | Okta M2M Client ID | Okta Admin |
| `OS_REST_API_CLIENT_SECRET_KEY` | Okta M2M Secret Key | Okta Admin |
| `OS_REST_API_SCOPE` | Okta Scope Name | Okta Admin |
| `OS_REST_API_URL` | Okta URL with Auth Server | Okta Admin |
| `OS_REST_API_USERNAME` | REST API user name | OneStream |

#### Option 2: OIS Configuration

For OneStream Identity Server:

| Property | Description | Source |
|----------|-------------|--------|
| `OS_REST_API_TOKEN` | Personal Access Token | OneStream Help Desk |
| `OS_REST_API_USERNAME` | REST API user name | OneStream |

---

## Part 4: EPMware Configuration

### Application Setup

1. Navigate to **Configuration → Applications → Configuration**
2. Create new application:
   - Type: **OneStream**
   - Target Application: OneStream app name
   - Deployment: **Direct**

![EPMware OneStream Application](../assets/images/appendices/epmware-onestream-app-config.png)
*EPMware application configuration for OneStream*

### Configure Application Properties

Navigate to **Properties** tab and configure:

![OneStream Properties Configuration](../assets/images/appendices/epmware-onestream-properties.png)
*OneStream application properties in EPMware*

#### REST API Properties

![REST API Properties](../assets/images/appendices/onestream-rest-api-properties.png)
*REST API authentication properties configuration*

| Property | Description | Example |
|----------|-------------|---------|
| `OS_REST_API_CLIENT_ID` | Okta Client ID | abc123def456 |
| `OS_REST_API_CLIENT_SECRET_KEY` | Okta Secret | ********* |
| `OS_REST_API_URL` | Authentication endpoint | https://epmware.okta.com/oauth2/[serverID]/v1/token |
| `OS_REST_API_USERNAME` | API User | REST API |

#### Deployment Properties

| Property | Description | Default |
|----------|-------------|---------|
| `OS_DEPLOY_DM_SEQUENCE` | DM Sequence name | Deploy Metadata |
| `OS_DEPLOY_DM_STEP` | DM Step name | Deploy Metadata |
| `OS_APPLICATION_NAME` | OneStream app name | GolfStream |

### Import Application Metadata

1. Click **Import** icon for OneStream application
2. Select **Manual Import**
3. Browse to ZIP file
4. Click **Import**

![OneStream Import Dialog](../assets/images/appendices/onestream-import-dialog.png)
*Manual import dialog for OneStream application*

---

## Part 5: Server Configuration

### Install EPMWARE.dll

1. Login to OneStream application server
2. Navigate to **BusinessRuleAssemblyFolder**
   - Location specified in server config file
3. Copy `EPMWARE.dll` to folder
4. Restart OneStream services if required

![DLL Installation Path](../assets/images/appendices/onestream-dll-path.png)
*BusinessRuleAssemblyFolder location for EPMWARE.dll*

!!! note "DLL File"
    The EPMWARE.dll file is provided by EPMware support. Contact support@epmware.com to obtain the file.

### Configure Whitelisting

For cloud deployments:
1. Request whitelisting from support@epmware.com
2. Provide OneStream public IP
3. EPMware provides IP for OneStream whitelist
4. OneStream support completes configuration

!!! info "Network Requirements"
    VPN tunnel is NOT required. Whitelisting uses public IP addresses only.

---

## Testing & Validation

### Connection Test

1. **EPMware Server Test**
   ```
   Configuration → Infrastructure → Servers
   - Select OneStream server
   - Test Connection
   ```

![Test Connection Success](../assets/images/appendices/onestream-test-connection.png)
*Successful connection test to OneStream*

### Import Validation

1. Review import status
2. Verify dimension count
3. Check hierarchy structures
4. Validate properties

![Import Status Report](../assets/images/appendices/onestream-import-status.png)
*Application import status showing successful completion*

### Deployment Test

1. Create test request
2. Make minimal change
3. Deploy through workflow
4. Verify in OneStream

---

## Troubleshooting

### Common Issues

| Issue | Cause | Solution |
|-------|-------|----------|
| **Authentication Failed** | Invalid credentials | Verify Okta/OIS configuration |
| **Business Rule Error** | Missing DLL | Install EPMWARE.dll |
| **Import Timeout** | Large metadata | Increase timeout settings |
| **Deployment Failed** | Sequence not found | Verify DM configuration |

### Debug Checklist

- [ ] EPMWARE.dll installed correctly
- [ ] Business rule compiled without errors
- [ ] REST API user has admin rights
- [ ] Authentication properties configured
- [ ] Data Management sequence created
- [ ] Whitelisting completed (if cloud)

### Log Locations

| Component | Log Location |
|-----------|--------------|
| **OneStream** | Application Event Log |
| **Business Rule** | BRApi.ErrorLog entries |
| **EPMware** | Administration → Services → Logs |

---

## Best Practices

### Security
- 🔐 Use dedicated service account
- 🔑 Rotate API credentials regularly
- 📝 Enable comprehensive audit logging
- 🛡️ Apply least privilege principle

### Performance
- ⚡ Schedule deployments off-peak
- 📦 Batch metadata changes
- 🎯 Target specific dimensions
- 📊 Monitor execution times

### Maintenance
- 📋 Document configuration
- 🔄 Test after OneStream updates
- 💾 Backup business rules
- 📚 Keep DLL versions current

---

## Quick Reference

### OneStream Properties

| Property Category | Properties |
|-------------------|------------|
| **Authentication** | OS_REST_API_CLIENT_ID, OS_REST_API_TOKEN |
| **Deployment** | OS_DEPLOY_DM_SEQUENCE, OS_DEPLOY_DM_STEP |
| **Application** | OS_APPLICATION_NAME, OS_APPLICATION_TYPE |
| **Connection** | OS_REST_API_URL, OS_REST_API_USERNAME |

### Required Files

| File | Purpose | Source |
|------|---------|--------|
| `ApplicationProperties.xml` | Application settings | OneStream Extract |
| `WorkflowChannels.xml` | Workflow configuration | OneStream Extract |
| `*_Metadata.xml` | Dimensions & rules | OneStream Extract |
| `Security_Groups.xml` | Security configuration | OneStream Extract |
| `EPMWARE.dll` | Integration library | EPMware Support |

---

## Support Resources

### EPMware Support
📧 **Email**: support@epmware.com  
📞 **Phone**: 408-614-0442  

### OneStream Resources
- OneStream Community Portal
- XF MarketPlace
- OneStream Support

### Related Documentation
- [Application Configuration](../configuration/applications.md)
- [Server Configuration](../configuration/infrastructure.md)
- [Deployment Management](../deployment/index.md)

!!! tip "Integration Tip"
    Always test the integration in a OneStream development environment before configuring production. Create a backup of your OneStream business rules before making changes.