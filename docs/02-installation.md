# Installation & Deployment (Phase 1)

## Purpose
This document outlines the installation and initial deployment of **osTicket** on **Debian 12 (Bookworm)** as part of Phase 1 of the helpdesk home lab. The goal of this phase was to deploy a stable, standalone ticketing system while following realistic system administration and security practices.

Active Directory integration and external service dependencies are intentionally excluded from this phase and will be addressed in Phase 2.

## Operating System Selection

**Debian GNU/Linux 12 (Bookworm)** was selected for this deployment based on the following considerations:
- Long-term stability and predictable package availability
- Native support for PHP 8.2, which is compatible with osTicket
- Availability of required PHP extensions (including IMAP)
- Common usage in server environments

Earlier testing on newer Debian releases revealed dependency availability issues, reinforcing the importance of selecting a stable, supported platform for production-style deployments.

## Base System Preparation

The operating system was installed with a minimal configuration to reduce attack surface and unnecessary resource usage.

Key decisions:
- No desktop environment required for server operation
- SSH enabled for remote administration
- System packages updated immediately after installation

Post-installation updates were applied to ensure all packages were current before application deployment.

## Web and Application Stack Installation

The following components were installed to support the osTicket application:

- **Apache 2** as the web server
- **PHP 8.2** as the application runtime
- Required PHP extensions for osTicket functionality
- **MariaDB** as the backend database

All services were enabled and configured to start automatically to ensure persistence across reboots.

## Database Configuration

MariaDB was secured using vendor-recommended hardening procedures to reduce default attack vectors.

A dedicated database and database user were created for osTicket:
- Application-specific database isolation
- Least-privilege access model
- Credentials restricted to local access only

Database access was verified prior to application installation to prevent runtime authentication failures.

## osTicket Deployment

The osTicket application was deployed manually to ensure transparency and control over file placement and permissions.

Deployment steps included:
- Downloading the official osTicket release
- Extracting application files into the Apache web root
- Assigning proper ownership to the web service account
- Configuring file permissions required for installation

A writable configuration file was prepared exclusively for the duration of the installer process.

## Web-Based Installer

The osTicket web installer was completed using a browser-based interface.

Configuration steps included:
- Defining helpdesk identity and system settings
- Creating the initial administrative account
- Connecting the application to the MariaDB backend

![Web-Based Installer](../screenshots/install-osticket.png)

Installer execution was monitored using Apache error logs to diagnose and resolve runtime issues.

## Post-Installation Hardening

After successful installation, the following security steps were performed:

- Removal of the osTicket setup directory
- Restriction of configuration file permissions to read-only
- Verification of service stability after restart

These steps ensure the application cannot be reconfigured or reinstalled without explicit administrative action.

## Validation

The deployment was validated through functional testing:
- Access to the user ticket submission portal
- Access to the agent and admin control panel
- Successful creation and resolution of test tickets
- Verification of application stability across service restarts

![Validation](../screenshots/install-final.png)

Successful validation confirmed the system was ready for operational use.

## Phase 1 Completion

At the conclusion of Phase 1, the environment met the following criteria:
- Fully functional osTicket deployment
- Stable application and database services
- Secure baseline configuration
- Documented installation process

The system was snapshotted to preserve a known-good state prior to Phase 2 enhancements.

## Next Phase

Phase 2 will focus on:
- Active Directory / LDAP authentication
- Centralized identity integration
- External service dependencies (SMTP, TLS)
- Expanded security and operational features

Phase 1 documentation will remain unchanged to preserve baseline integrity.
