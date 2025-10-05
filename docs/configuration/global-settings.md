# Global Settings

Global Settings configure system-wide parameters for the entire EPMware application. These settings control email services, application behavior, web interface options, and user-defined fields that affect all modules and users.

![Global Settings Overview](../assets/images/configuration/global-settings-overview.png)<br/>
*Global Settings module with configuration tabs*

## Overview

Navigate to **Configuration → Misc → Global Settings** to configure system-wide settings organized into four main categories:

- **[Email Settings](#email-settings)** - Configure email service and notification parameters
- **[Application Settings](#application-settings)** - System behavior, performance, and integration options
- **[Web Settings](#web-settings)** - User interface and web application configuration
- **[User Defined Settings](#user-defined-settings)** - Custom fields for request management

## Quick Links

<div class="grid cards">
  <div class="card">
    <h3>📧 Email Configuration</h3>
    <p>Set up email service, addresses, and AWS SES integration</p>
    <a href="#email-settings" class="md-button">Configure Email →</a>
  </div>
  
  <div class="card">
    <h3>⚙️ System Settings</h3>
    <p>Application behavior, timeouts, and performance tuning</p>
    <a href="#application-settings" class="md-button">Manage System →</a>
  </div>
  
  <div class="card">
    <h3>🌐 Web Interface</h3>
    <p>UI preferences and display options</p>
    <a href="#web-settings" class="md-button">Configure UI →</a>
  </div>
  
  <div class="card">
    <h3>📝 Custom Fields</h3>
    <p>Define up to 3 user-defined fields for requests</p>
    <a href="#user-defined-settings" class="md-button">Add Fields →</a>
  </div>
</div>

---

## Email Settings

Email Settings control all global email configuration for workflow notifications and system communications.

![Email Settings Tab](../assets/images/configuration/email-settings-tab.png)<br/>
*Email Settings configuration tab*

### Configuration Options

| Setting | Description | Required | Example |
|---------|-------------|----------|---------|
| **From Email Address** | Sender address for all workflow emails | Yes | admin@epmware.com |
| **Override Email Address** | Redirect all emails to single address (testing) | No | test@company.com |
| **Failed Email Forwarding Address** | Receive notifications for failed emails | No | it-support@company.com |
| **Append Fixed value for Email Subject (Prefix)** | Environment identifier prefix | No | [TEST] or [PROD] |

### Email Service Configuration

EPMware supports two email service options:

#### Option 1: AWS SES (Simple Email Service)

**Configuration Steps:**

1. Determine sender email address (e.g., `finance@company.com`)
2. Contact EPMware support to initiate AWS verification
3. AWS sends verification email to the address
4. Complete verification process
5. Set verified address in "From Email Address"

!!! info "AWS SES Documentation"
    For security team inquiries, refer to: [AWS SES FAQs](https://aws.amazon.com/ses/faqs/)

#### Option 2: Client SMTP Server

**Required Information:**
- SMTP Server Name
- SMTP Port
- SMTP Username  
- SMTP Password

### Configuration Example

![Email Settings Example](../assets/images/configuration/email-settings-example.png)<br/>
*Example email configuration for production environment*

**Best Practices:**

1. **Environment Prefixes** - Use clear identifiers:
   - `[PROD]` for production
   - `[UAT]` for user acceptance testing
   - `[DEV]` for development

2. **Override Address** - Only use in non-production environments

3. **Failed Email Monitoring** - Always configure for production

### Editing Email Settings

1. Double-click the **Value** field to enter edit mode
2. Enter or modify the setting value
3. Update the **Description** if needed
4. Click **Save** icon to apply changes

---

## Application Settings

Application Settings control system behavior, performance parameters, and operational configurations.

![Application Settings Tab](../assets/images/configuration/application-settings-tab.png)<br/>
*Application Settings with system configuration options*

### Critical System Settings

#### Performance & Timeout Settings

| Setting | Default | Description | Impact |
|---------|---------|-------------|--------|
| **Application Import - Total Interval in Seconds before TimeOut** | 3000 | Maximum import duration | Prevents hanging imports |
| **Application Import - sleep interval in Seconds** | 10 | Polling interval during import | System responsiveness |
| **Auto Refresh Interval (Seconds)** | 60 | Dashboard/monitor refresh rate | Real-time updates |
| **Maximum # of Minutes for Deployment Task** | 180 | Deployment timeout | Large deployment handling |
| **Maximum # of Minutes for ERP Import Task** | 180 | ERP import timeout | Data volume capacity |
| **Maximum # of Minutes for Export Task** | 180 | Export timeout | Report generation |

#### File Size Limits

| Setting | Default (MB) | Use Case |
|---------|--------------|----------|
| **Maximum file size for All Modules** | 300 | General file operations |
| **Maximum file size for ERP Import** | 50 | ERP data files |
| **Maximum file size for Migration Import** | 200 | Application migrations |
| **Maximum file size for Request Attachments** | 20 | User document uploads |

#### Security & Access Settings

| Setting | Default | Description |
|---------|---------|-------------|
| **Enable Workflow based Security for Requests Dashboard** | Y | Restrict dashboard visibility |
| **User Authentication Directory Type** | LDAP | LDAP or MSAD |
| **User Authentication Directory Type option enabled** | Y | Enable directory integration |
| **Allow Delete/Cancel of Related Request Lines** | N | Cascade deletion control |

#### Service Configuration

| Setting | Default | Description |
|---------|---------|-------------|
| **Deployment Service Sleep Interval** | 5 | Seconds between deployment checks |
| **ERP Import Service Sleep Interval** | 5 | Seconds between import checks |
| **Workflow Service Sleep Interval** | 5 | Seconds between workflow checks |
| **SSH port for Agent Service** | 22 | Agent communication port |

### Organization Branding

Configure company logo for emails and reports:

![Organization Logo Settings](../assets/images/configuration/organization-logo-settings.png)<br/>
*Logo configuration for branding*

| Setting | Example | Notes |
|---------|---------|-------|
| **Organization Name** | EPMware Inc. | Company name |
| **Organization Logo URL** | https://company.com/logo.png | Public URL required |
| **Organization Logo Width (Pixels)** | 172 | Recommended width |
| **Organization Logo Height (Pixels)** | 25 | Recommended height |

### Debug & Monitoring Settings

| Setting | Default | Purpose |
|---------|---------|---------|
| **Debug Level** | 3 | 1=Error only, 2=Warning, 3=All |
| **Debug Purge Days** | 30 | Retention period for debug logs |
| **Turn on/off debug messages** | Y | Master debug switch |
| **Turn on/off debug messages to table** | Y | Database logging |
| **Database Trace identifier** | ew_trace | Trace session identifier |
| **Specify prefix for Debug Files** | ew_debug | Debug file naming |

### System Directories

| Setting | Default | Description |
|---------|---------|-------------|
| **Stage DB Directory** | EW003_STAGE_DB_DIR | Deployment staging |
| **Temp DB Directory** | EW003_TEMP_DB_DIR | Temporary files |
| **File Archives DB Directory** | EW003_ARCHIVE_DB_DIR | File archival |

### Display Configuration

| Setting | Default | Impact |
|---------|---------|--------|
| **Date Format** | MM/DD/RRRR | Global date display |
| **Show # of nodes per page in Hierarchies** | 100 | Pagination size |
| **Show Member Description by default** | Y | Hierarchy display |
| **Show Descendants of parent member for shared instances** | Y | Shared member handling |
| **Show or Hide System Generated Request lines** | Y | Request visibility |

### Advanced Settings

![Application Settings Advanced](../assets/images/configuration/application-settings-advanced.png)<br/>
*Advanced application configuration options*

| Setting | Default | Use Case |
|---------|---------|----------|
| **Disable All Logic Builder Scripts** | N | Emergency script disable |
| **Oracle Character Set** | AL32UTF8 | AL32UTF8 or WE8ISO8859P1 |
| **EPMware Application URL** | https://demo.epmwarecloud.com | System base URL |
| **Unzip - Sleep Interval in Seconds** | 20 | Archive processing |
| **Unzip - Total Interval before TimeOut** | 1200 | Large archive handling |

### Editing Application Settings

1. Double-click the **Value** or **Description** field
2. Modify the setting as required
3. Click **Save** icon to apply changes

!!! warning "Service Restart"
    Some settings may require service restart to take effect. Check with EPMware support before modifying critical system parameters.

---

## Web Settings

Web Settings configure user interface behavior and display preferences for the web application.

![Web Settings Tab](../assets/images/configuration/web-settings-tab.png)<br/>
*Web Settings configuration options*

### Available Settings

| Setting | Description | Default | Options |
|---------|-------------|---------|---------|
| **Theme** | UI color scheme | Light | Light/Dark |
| **Navigation Style** | Menu layout | Side | Side/Top |
| **Grid Lines Per Page** | Default pagination | 25 | 10/25/50/100 |
| **Enable Tooltips** | Show help tooltips | Y | Y/N |
| **Animation Speed** | UI transition speed | Normal | Slow/Normal/Fast |
| **Session Timeout Warning** | Minutes before warning | 5 | 1-30 |

### Editing Web Settings

1. Double-click the **Value** field to enter edit mode
2. Select or enter new value
3. Update **Description** if applicable
4. Click **Save** icon to commit changes

---

## User Defined Settings

User Defined Settings create up to three custom fields (UDF1, UDF2, UDF3) for the Request page, capturing additional business-specific information.

![User Defined Fields Settings](../assets/images/configuration/udf-settings-tab.png)<br/>
*User Defined Field configuration*

### Field Configuration Options

| Property | Description | Options |
|----------|-------------|---------|
| **Enabled** | Activate the field | On/Off |
| **Required** | Make field mandatory | On/Off |
| **Data Type** | Field data type | String/Numeric/Date |
| **Display Type** | Input method | Input/Lookup |
| **Display Label** | Field label on request | Custom text |
| **Lookup** | Reference lookup table | Lookup name |
| **LOV SQL** | Dynamic list of values | SQL query |
| **Description** | Field help text | Custom text |

### Configuration Examples

#### Example 1: Request Type Field (UDF1)

```
Enabled: On
Required: On
Data Type: String
Display Type: Lookup
Display Label: Request Type
Lookup: REQUEST_TYPES
Description: Select the type of metadata request
```

#### Example 2: Cost Center Field (UDF2)

```
Enabled: On
Required: Off
Data Type: String
Display Type: Input
Display Label: Cost Center
Description: Enter cost center code
```

#### Example 3: Effective Date Field (UDF3)

```
Enabled: On
Required: On
Data Type: Date
Display Type: Input
Display Label: Effective Date
Description: Date when changes should take effect
```

### Dynamic List of Values (LOV SQL)

Instead of static lookups, use SQL to generate dynamic dropdown values:

![UDF LOV SQL Configuration](../assets/images/configuration/udf-lov-sql.png)<br/>
*LOV SQL configuration for dynamic dropdowns*

#### SQL Requirements

LOV SQL must return four columns:
1. **lookup_code** - Stored value
2. **meaning** - Display value
3. **description** - Optional tooltip
4. **seq_num** - Sort order

#### Example 1: Security Groups with Filter

```sql
-- Show security groups containing 'APPR'
SELECT name lookup_code, 
       name meaning, 
       description description,
       rownum seq_num
FROM ew_groups
WHERE name LIKE '%APPR%'
ORDER BY name
```

#### Example 2: Requestor's Groups

```sql
-- Show groups for current requestor
SELECT REPLACE(rg.group_name,'REQUESTORS - ','') lookup_code,
       REPLACE(rg.group_name,'REQUESTORS - ','') meaning,
       rg.group_name description,
       rownum seq_num
FROM ew_user_groups_v rg,
     ew_request_headers h
WHERE h.request_id = :request_id  -- Bind variable
  AND rg.user_id = h.requested_by
  AND rg.group_name LIKE 'REQUESTORS - %'
```

!!! note "Bind Variable"
    The `:request_id` bind variable is automatically available in UDF LOV SQL queries.

### Editing User Defined Settings

1. Double-click field in column to enter edit mode
2. Configure field properties
3. Test LOV SQL if applicable
4. Click **Save** icon to apply changes

### Use Cases for UDFs

| Field | Common Uses | Example Values |
|-------|-------------|----------------|
| **UDF1** | Request categorization | New/Change/Delete |
| **UDF2** | Business context | Project codes, regions |
| **UDF3** | Tracking references | Ticket numbers, dates |

---

## Best Practices

### 1. Email Configuration

- **Verify Sender Address** - Complete AWS SES verification
- **Use Environment Prefixes** - Clear identification
- **Monitor Failed Emails** - Configure forwarding address
- **Test in Non-Production** - Use override address

### 2. Performance Tuning

- **Adjust Timeouts** - Based on data volumes
- **Optimize Intervals** - Balance performance vs. load
- **Set File Limits** - Prevent system overload
- **Monitor Services** - Check service intervals

### 3. Security Settings

- **Enable Workflow Security** - Restrict dashboard access
- **Configure Authentication** - LDAP/MSAD properly
- **Audit Debug Settings** - Control logging levels
- **Regular Purging** - Maintain debug retention

### 4. User Experience

- **Consistent Date Format** - Organization-wide standard
- **Appropriate Pagination** - Based on data volumes
- **Clear UDF Labels** - Business-friendly names
- **Helpful Descriptions** - Guide users

---

## Troubleshooting

### Common Issues

| Issue | Setting to Check | Solution |
|-------|-----------------|----------|
| Emails not sending | From Email Address | Verify AWS SES verification |
| Import timeouts | Application Import TimeOut | Increase timeout value |
| Slow dashboard | Auto Refresh Interval | Increase interval |
| Large file failures | Maximum file size settings | Adjust limits |
| Missing debug logs | Debug Level, Turn on debug | Enable debugging |
| Authentication issues | User Authentication Directory Type | Verify LDAP/MSAD settings |

### Critical Settings Reference

!!! danger "High Impact Settings"
    These settings significantly affect system behavior:
    
    - **Disable All Logic Builder Scripts** - Stops all automation
    - **Database Trace** - Performance impact when enabled
    - **Service Sleep Intervals** - Affects responsiveness
    - **File Size Limits** - Can block operations

### Getting Help

When contacting support, provide:
- Current setting values (screenshot)
- Error messages
- Debug log excerpts
- System behavior description

---

## Migration Considerations

When migrating between environments:

### Settings to Update

1. **Email Settings**
   - From Email Address (environment-specific)
   - Override Email (remove in production)
   - Subject Prefix (change per environment)

2. **Application Settings**
   - EPMware Application URL
   - Organization Logo URL
   - Debug Level (reduce in production)

3. **Directory Paths**
   - Stage DB Directory
   - Temp DB Directory
   - Archive DB Directory

### Settings to Preserve

- File size limits
- Timeout values
- Service intervals
- User Defined Fields
- Date formats

!!! tip "Configuration Backup"
    Export Global Settings before major changes using the Migration module.

---

## Related Topics

- [Email Templates](../email-templates/index.md) - Use email settings in templates
- [Workflow Configuration](../workflow/index.md) - Workflow security settings
- [Logic Builder](../logic-builder/index.md) - Script debugging settings
- [Request Management](../requests/index.md) - User defined fields in requests
- [Migration Module](../administration/migration.md) - Export/import settings
