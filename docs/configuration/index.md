# Configuration

The Configuration module is the foundation of EPMware administration, providing comprehensive setup and management of all core system components. This module enables administrators to configure infrastructure connections, define applications and dimensions, manage metadata properties, and establish global settings that govern the entire EPMware environment.

## Overview

Configuration establishes the framework for EPMware's master data management capabilities. Proper configuration ensures seamless integration with target EPM systems, accurate metadata management, and efficient workflow processing. The configuration module is organized into logical sections that build upon each other, from infrastructure setup through detailed property definitions.

## Configuration Components

### Infrastructure

Infrastructure configuration establishes the foundational connections and environment structure for EPMware. This includes defining server connections to target applications and setting up multi-environment configurations for development, testing, and production deployments.

**Key Infrastructure Features:**

- **Server Configuration** - Define connection details for target EPM systems (HFM, Planning, Essbase, PBCS, TRCS, OneStream, etc.)
- **Multi-Environment Setup** - Configure deployment paths across development, UAT, and production environments
- **Environment Mapping** - Associate applications with their respective environments
- **Connection Testing** - Validate server connectivity and credentials

[:octicons-arrow-right-24: Configure Infrastructure](infrastructure.md)

---

### Applications

Application configuration links EPMware to target EPM applications, imports metadata hierarchies, and defines deployment settings. Each application in EPMware represents a target system where metadata will be deployed.

**Application Management:**

- **Application Registration** - Create and configure EPMware applications linked to target systems
- **Metadata Import** - Auto-import hierarchies from target applications or manually load from files
- **Application Properties** - Configure target-specific settings for HFM, Planning, Essbase, PBCS, and other applications
- **Deployment Settings** - Define deployment methods (Direct, File, or Interface Table)
- **Import Error Resolution** - Troubleshoot and resolve application import issues

[:octicons-arrow-right-24: Configure Applications](applications.md)

---

### Dimensions

Dimension configuration defines the hierarchical structure of your metadata, including dimension classes, dimension properties, mappings between applications, and hierarchy actions that control metadata operations.

**Dimension Configuration Areas:**

- **Dimension Classes** - Organize dimensions into logical groupings (Account, Entity, Custom, etc.)
- **Dimension Configuration** - Define dimension attributes, security, and behavior
- **Dimension Properties** - Configure dimension-level settings and SQL-based derivations
- **Dimension Mapping** - Link dimensions across applications for synchronized metadata management
- **Hierarchy Actions** - Control available operations (Create Member, Move Member, Delete Member, etc.)

[:octicons-arrow-right-24: Configure Dimensions](dimensions.md)

---

### Member Properties

Member Properties configuration defines the attributes that describe individual metadata members, including property definitions, categories for organization, mappings across applications, validations, and derivations.

**Property Management Features:**

- **Property Configuration** - Define property attributes, display types, and deployment settings
- **Property Categories** - Organize properties into logical groups for user interface display
- **Property Mapping** - Synchronize property values across mapped applications
- **Property Validation** - Apply business rules and data quality checks
- **Property Derivation** - Calculate property values using SQL or custom scripts

[:octicons-arrow-right-24: Configure Member Properties](member-properties.md)

---

### Email Templates

Email Templates enable customized notifications throughout the metadata request lifecycle. Templates support dynamic content through variable tags and can include request details, validation results, and deployment status.

**Email Template Features:**

- **Variable Tags** - Insert dynamic content (Request ID, Requestor, Status, etc.)
- **Custom Tags** - Use Logic Builder to create custom email content
- **Email Body Tables** - Include formatted tables with request details, properties, and results
- **Workflow Integration** - Assign templates to workflow stages for automated notifications

[:octicons-arrow-right-24: Configure Email Templates](email-templates.md)

---

### Global Settings

Global Settings establish system-wide parameters that affect all aspects of EPMware operation, from email configuration to application behavior and user-defined field definitions.

**Settings Categories:**

- **Email Settings** - Configure SMTP servers, sender addresses, and email routing
- **Application Settings** - Set deployment timeouts, file size limits, and system behavior
- **Web Settings** - Configure web application parameters
- **User Defined Settings** - Create custom fields for metadata requests (UD1, UD2, UD3)

[:octicons-arrow-right-24: Configure Global Settings](global-settings.md)

---

### Lookups

Lookups provide predefined value lists used throughout EPMware for dropdown menus, validation lists, and user selections. Administrators can create custom lookups or modify existing ones to match organizational requirements.

**Lookup Management:**

- **Standard Lookups** - System-defined lookups for priorities, statuses, and workflows
- **Custom Lookups** - User-defined value lists for properties and validations
- **Lookup Codes** - Define individual values with codes, meanings, and display sequences
- **Lookup SQL** - Create dynamic lookups using SQL queries

[:octicons-arrow-right-24: Manage Lookups](lookups.md)

---

## Configuration Workflow

Follow this recommended sequence when configuring a new EPMware environment:

### Phase 1: Foundation Setup

1. **Configure Servers** - Set up connections to target EPM systems
2. **Create Applications** - Register target applications in EPMware
3. **Import Metadata** - Load hierarchies from target applications
4. **Configure Application Properties** - Set target-specific deployment parameters

### Phase 2: Structure Definition

5. **Define Dimension Classes** - Organize dimensions into logical categories
6. **Configure Dimensions** - Set up dimension attributes and mappings
7. **Define Member Properties** - Create property definitions for metadata attributes
8. **Organize Property Categories** - Group properties for user interface display

### Phase 3: Business Rules

9. **Create Property Validations** - Establish data quality rules
10. **Configure Property Derivations** - Set up calculated properties
11. **Map Properties and Dimensions** - Link metadata across applications
12. **Define Hierarchy Actions** - Control available metadata operations

### Phase 4: System Settings

13. **Configure Email Templates** - Set up workflow notifications
14. **Establish Global Settings** - Configure system-wide parameters
15. **Create Custom Lookups** - Define organization-specific value lists
16. **Set User Defined Fields** - Configure custom request fields

!!! tip "Configuration Best Practices"
    - Complete infrastructure setup before importing applications
    - Test server connections before proceeding with application import
    - Use security classes to control access at each configuration level
    - Document custom SQL used in derivations and validations
    - Back up configuration before making significant changes

## Configuration Security

Configuration modules should be restricted to administrative users. Use security provisioning to control access:

- **Config Module Access** - Assign the Config module only to administrators
- **Security Classes** - Use security classes to limit access to specific applications or dimensions
- **Audit Trail** - All configuration changes are logged in the audit module

!!! warning "Administrative Access Required"
    Configuration changes can significantly impact EPMware operation and metadata management. Ensure only trained administrators have access to configuration modules.

## Related Topics

- [Security Configuration](../security/index.md) - Set up users, groups, and security provisioning
- [Workflow Builder](../workflow/index.md) - Create workflows using configured applications
- [Deployment Manager](../deployment/index.md) - Deploy metadata to configured target systems
- [Logic Builder](../logic-builder/index.md) - Create custom scripts for validations and derivations

---

## Quick Links

<div class="grid cards" markdown>

-   :material-server:{ .lg .middle } **Infrastructure**

    ---

    Configure servers and multi-environment deployments

    [:octicons-arrow-right-24: Set up infrastructure](infrastructure.md)

-   :material-application:{ .lg .middle } **Applications**

    ---

    Import and configure target EPM applications

    [:octicons-arrow-right-24: Configure applications](applications.md)

-   :material-file-tree:{ .lg .middle } **Dimensions**

    ---

    Define dimension structure and mappings

    [:octicons-arrow-right-24: Set up dimensions](dimensions.md)

-   :material-format-list-bulleted:{ .lg .middle } **Member Properties**

    ---

    Configure metadata properties and categories

    [:octicons-arrow-right-24: Define properties](member-properties.md)

-   :material-email:{ .lg .middle } **Email Templates**

    ---

    Create notification templates for workflows

    [:octicons-arrow-right-24: Design templates](email-templates.md)

-   :material-cog:{ .lg .middle } **Global Settings**

    ---

    Establish system-wide parameters

    [:octicons-arrow-right-24: Configure settings](global-settings.md)

-   :material-format-list-checks:{ .lg .middle } **Lookups**

    ---

    Manage value lists and dropdown options

    [:octicons-arrow-right-24: Manage lookups](lookups.md)

</div>
