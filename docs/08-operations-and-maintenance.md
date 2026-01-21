# Operations and Maintenance

## Purpose

This document describes how the helpdesk environment is **operated, maintained, and sustained over time**.  
The focus is not initial deployment, but **ongoing reliability, security, and recoverability**.

In enterprise environments, systems are judged by how they behave:
- After updates
- During failures
- Under change
- Over time

This lab intentionally includes operational practices to demonstrate long-term ownership, not one-time setup.

## Operational Scope

This environment is treated as a **persistent internal service**, not a disposable test system.

Operational responsibility includes:
- Identity services (Active Directory)
- Authentication mechanisms (LDAP / LDAPS)
- Ticketing platform (osTicket)
- Database integrity and retention
- Workflow enforcement and auditability
- Service availability and failure recovery

All systems are assumed to be in continuous use.

## Operating System Maintenance

### Linux — osTicket Server (Debian)

Operational practices include:
- Regular security and package updates
- Verification of Apache, PHP, and MariaDB services after patching
- Intentional reboot scheduling to avoid surprise downtime
- Log review following updates to detect regressions

The server is treated as a production system where availability matters.

### Windows Server — Domain Controller

Operational practices include:
- Scheduled Patch Tuesday updates
- Reboot coordination to avoid authentication outages
- Post-update verification of:
  - AD DS
  - DNS
  - LDAPS functionality
- Review of system and security event logs after changes

Authentication services are treated as **critical infrastructure**.

## Application Maintenance (osTicket)

### Upgrade Discipline

osTicket updates are handled deliberately:
- Release notes reviewed prior to upgrade
- Configuration and database backups taken beforehand
- Plugin compatibility verified
- Post-upgrade validation performed

Blind updates are avoided to prevent workflow disruption.

### Configuration Drift Awareness

Key configuration areas are monitored for unintended change:
- LDAP authentication settings
- Department and role assignments
- SLA definitions
- Help topics and escalation rules

Changes are documented to preserve operational intent and auditability.

## Identity and Access Maintenance

### Active Directory Hygiene

Ongoing directory maintenance includes:
- Review of disabled or stale accounts
- Group membership audits
- Service account monitoring
- Enforcement of least-privilege access

Identity hygiene is treated as a preventive control, not a cleanup task.

### LDAP / LDAPS Health Validation

Authentication health is monitored through:
- Periodic LDAPS connectivity testing
- Certificate trust validation
- Review of authentication failures
- Detection of anomalous login behavior

Authentication failures are treated as **priority incidents**, not background noise.

## Database Operations

### MariaDB Responsibilities

The database is treated as operational data storage, not disposable logs.

Operational tasks include:
- Regular logical backups
- Disk space monitoring
- Integrity checks
- Review of database service logs

Ticket history and audit trails are preserved intentionally.

## Backup and Recovery Strategy

### Protected Data

Backups include:
- osTicket database
- Application configuration files
- LDAP integration settings
- Knowledge base content

### Recovery Philosophy

Backups are considered successful only if recovery is possible.
The focus is on **restoration capability**, not backup existence.

## Monitoring and Service Visibility

### Current State

Operational visibility currently includes:
- Manual service health checks
- Authentication testing
- Review of system, application, and database logs

This establishes a baseline understanding of normal behavior.

### Integrated Monitoring (Zabbix)

This environment is designed to integrate with centralized monitoring.

Planned and implemented monitoring concepts include:
- Service availability checks
- Authentication service monitoring
- Resource utilization visibility
- Alert-driven incident awareness

Monitoring is treated as an operational multiplier, not an afterthought.

## Incident Handling During Operations

Operational incidents follow established workflows:

1. Issue detected (user report or monitoring)
2. Ticket created or flagged
3. SLA applied
4. Tier 1 validates symptoms
5. Tier 2 performs remediation
6. Root cause documented
7. Knowledge base updated if applicable

Operational incidents feed directly into process improvement.

## Change Management Discipline

All non-trivial changes follow a structured approach:
- Define change scope
- Assess operational impact
- Apply change during appropriate window
- Validate functionality
- Document outcome

Uncontrolled changes are treated as technical debt.

## Documentation as an Operational Asset

Documentation is considered part of the operational system.

Maintained documentation includes:
- Architecture and trust boundaries
- Workflow and escalation logic
- Known issues and resolutions
- Authentication dependencies

This ensures continuity even in single-admin environments.

## Failure Scenarios Considered

This lab explicitly accounts for realistic failure scenarios:
- Domain Controller downtime
- LDAPS authentication failure
- Database corruption or disk exhaustion
- Certificate expiration
- Configuration drift after updates

Planning for failure is treated as a baseline operational skill.

## Why This Matters

Operations and maintenance separate:
- Deployments from systems
- Labs from environments
- Setup knowledge from ownership

This section demonstrates the ability to **keep systems running**, recover them when they fail, and maintain trust over time.

## Future Operational Enhancements

Planned improvements include:
- Automated backup scheduling
- Monitoring-driven ticket creation
- NOC alert workflows
- Scheduled maintenance records
- Post-incident review templates

## Summary

This helpdesk environment is treated as a living system.

It is:
- Maintained deliberately
- Secured intentionally
- Observed continuously
- Designed to fail safely and recover cleanly

Operations and maintenance are not optional.
They are the proof that this environment reflects real enterprise IT.
