# EPMware Administrator's Guide

Welcome to the EPMware Administrator's Guide. This comprehensive guide provides detailed instructions for configuring, maintaining, and administering your EPMware master data management and workflow environment.

## About This Guide

EPMWARE is a master data management and workflow tool that manages master data and enforces your organization's workflow around the everyday processes that surround your metadata changes. This guide is designed for system administrators, implementation specialists, and power users responsible for:

- Configuring and maintaining EPMware applications
- Managing security and user access
- Building and maintaining workflows
- Monitoring metadata deployments
- Integrating with target EPM systems


## Key Topics

### Configuration
Configure the core components of your EPMware environment, including infrastructure, applications, dimensions, properties, and global settings.

**Key Configuration Areas:**

- **Infrastructure** - Server configuration and multi-environment setup
- **Applications** - Application import, properties, and deployment settings
- **Dimensions** - Dimension classes, mapping, and hierarchy actions
- **Member Properties** - Property configuration, categories, and derivations
- **Email Templates** - Notification templates with custom tags
- **Global Settings** - System-wide email, application, and web settings

### Security
Implement comprehensive security controls including user management, role-based access, security classes, and SSO integration.

**Security Components:**

- **Security Model** - Understanding roles, modules, and security classes
- **Users & Groups** - User provisioning and group management
- **Security Provisioning** - Assigning access rights
- **SSO Configuration** - SAML and LDAP integration

### Workflow
Design, build, and maintain workflows that enforce your organization's business processes for metadata management.

**Workflow Features:**

- **Workflow Tasks** - Configurable review, approval, validation, and deployment tasks
- **Workflow Builder** - Visual workflow design with stages and branching
- **Custom Scripts** - Logic Builder integration for advanced workflows

### Deployment
Manage metadata deployments to target applications with scheduling, monitoring, and error handling capabilities.

**Deployment Management:**

- **Deployment Manager** - Configure deployment jobs by application, workflow, or request
- **Deployment Monitor** - Real-time monitoring of deployment status
- **Deployment Schedule** - Automated deployment scheduling

### Advanced Administration
Access advanced features including metadata export, Logic Builder scripting, application migration, and ERP integration.

**Advanced Features:**

- **Export Metadata** - Extract metadata for reporting and analysis
- **Logic Builder** - Create custom validations and automation scripts
- **Application Migration** - Move configurations between environments
- **ERP Import** - Import metadata from ERP systems

## Prerequisites

Before using this guide, ensure you have:

- Administrative access to your EPMware environment
- Understanding of your target EPM applications (HFM, Planning, Essbase, PBCS, etc.)
- Familiarity with metadata management concepts
- Basic knowledge of SQL and scripting (for advanced features)

!!! note
    For end-user documentation on creating and managing metadata requests, refer to the [EPMware User Guide](../user-guide/).

## Quick Start

New to EPMware administration? Follow these steps to get started:

1. **[Configure Infrastructure](configuration/infrastructure.md)** - Set up servers and environments
2. **[Import Applications](configuration/applications.md#application-create-and-import)** - Connect target EPM applications
3. **[Set Up Security](security/)** - Create users, groups, and security classes
4. **[Build Workflows](workflow/)** - Design approval workflows
5. **[Configure Deployment](deployment/)** - Set up deployment jobs

## Support & Resources

- **Technical Support**: support@epmware.com
- **Phone**: 408-614-0442
- **Website**: [www.epmware.com](https://www.epmware.com)

---

## Documentation Sections

Explore the complete administrator documentation:

<div class="grid cards" markdown>

-   :material-cog:{ .lg .middle } **Configuration**

    ---

    Configure infrastructure, applications, dimensions, properties, and system settings

    [:octicons-arrow-right-24: Get started](configuration/)

-   :material-shield-account:{ .lg .middle } **Security**

    ---

    Manage users, groups, security classes, and SSO integration

    [:octicons-arrow-right-24: Learn more](security/)

-   :material-sitemap:{ .lg .middle } **Workflow**

    ---

    Build and maintain metadata approval workflows

    [:octicons-arrow-right-24: View workflows](workflow/)

-   :material-rocket-launch:{ .lg .middle } **Deployment**

    ---

    Deploy metadata to target applications with scheduling and monitoring

    [:octicons-arrow-right-24: Explore deployment](deployment/)

-   :material-database-export:{ .lg .middle } **Export Metadata**

    ---

    Extract metadata for reporting and analysis

    [:octicons-arrow-right-24: Export data](export/)

-   :material-code-braces:{ .lg .middle } **Logic Builder**

    ---

    Create custom scripts and automations

    [:octicons-arrow-right-24: Build logic](logic-builder/)

-   :material-swap-horizontal:{ .lg .middle } **Administration**

    ---

    Application migration, ERP import, and system services

    [:octicons-arrow-right-24: Admin tools](administration/)

-   :material-book-open-variant:{ .lg .middle } **Appendices**

    ---

    Target application configurations and integration guides

    [:octicons-arrow-right-24: Reference](appendices/)

</div>
