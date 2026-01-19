# Operations and Maintenance

## Purpose

This section documents how the helpdesk environment is **operated, maintained, and kept reliable over time**.

In real organizations, systems do not exist to be “set up once.”
They exist to be:
- Patched
- Monitored
- Audited
- Backed up
- Maintained with minimal disruption

This lab intentionally includes operational practices to demonstrate production awareness beyond initial deployment.

## Operational Scope

This environment is treated as a **long-running internal service**, not a disposable test VM.

Operational responsibility includes:
- Identity services (Active Directory)
- Ticketing platform (osTicket)
- Authentication mechanisms (LDAP / LDAPS)
- Database integrity
- Service availability
- Security posture

## System Maintenance Strategy

### Operating System Maintenance

**Debian (osTicket Server)**
- Regular package updates via `apt`
- Security patches prioritized
- Apache, PHP, and MariaDB services monitored after updates
- Reboots scheduled intentionally, not randomly

**Windows Server (Domain Controller)**
- Patch Tuesday updates applied
- Reboots coordinated to avoid authentication outages
- Event logs reviewed post-update

Maintenance windows are assumed, even in a lab environment.

## Application Maintenance (osTicket)

### Upgrade Strategy
- Minor version updates applied after review
- Configuration backups taken prior to upgrades
- Plugin compatibility verified before deployment

The goal is to simulate **change management discipline**, not blind updating.

### Configuration Drift Management
Key configuration areas monitored:
- LDAP authentication settings
- Department and role mappings
- SLA definitions
- Help topics and workflows

Changes are documented to prevent silent drift over time.

## Identity and Access Maintenance

### Active Directory Hygiene
- Disabled accounts reviewed periodically
- Group memberships audited
- Service accounts monitored for password expiration
- Least-privilege principles enforced

### LDAP / LDAPS Validation
- Certificate trust verified
- Bind account permissions reviewed
- Authentication logs monitored for anomalies

Authentication failures are treated as **priority incidents**, not nuisances.

## Database Maintenance

**MariaDB Responsibilities**
- Regular logical backups
- Integrity checks
- Monitoring for failed writes or corruption
- Disk space monitoring

Ticket history is treated as **operational data**, not expendable logs.

## Backup Strategy

### What Is Backed Up
- osTicket database
- osTicket configuration files
- LDAP integration settings
- Knowledge Base content

### Why It Matters
Ticket history, escalation records, and audit trails are critical in real environments.
This lab treats them the same way.

## Monitoring and Health Checks

### Current State
Manual monitoring includes:
- Service availability checks
- Authentication testing
- Log review (Apache, MariaDB, system logs)

### Planned Enhancements
- Automated monitoring (Zabbix / Prometheus)
- Service health dashboards
- Alert-driven ticket creation
- NOC visibility

This environment is designed to **grow into monitoring**, not pretend it already has it.

## Incident Handling During Operations

When operational issues occur:
1. Ticket is created or flagged
2. SLA is applied
3. Tier 1 validates symptoms
4. Tier 2 performs remediation
5. Root cause documented
6. Knowledge Base updated if applicable

Operational incidents feed directly into process improvement.

## Change Management Discipline

All significant changes follow a simple but realistic flow:
- Identify change scope
- Assess impact
- Apply change
- Validate functionality
- Document outcome

Even in a lab, uncontrolled changes are treated as technical debt.

## Documentation as an Operational Tool

Documentation is considered part of operations, not an afterthought.

Maintained documentation includes:
- Architecture diagrams
- Escalation logic
- Known issues and resolutions
- Authentication dependencies

This ensures continuity and knowledge transfer, even in a single-admin environment.

## Failure Scenarios Considered

This lab explicitly accounts for:
- Domain Controller downtime
- LDAP authentication failure
- Database corruption
- Certificate expiration
- Misconfiguration during updates

Planning for failure is considered a **baseline competency**, not pessimism.

## Why This Matters

Operations and maintenance are what separate:
- Demos from systems
- Labs from environments
- Setup knowledge from operational competence

This section demonstrates the ability to **keep systems running**, not just deploy them once.

## Future Enhancements

Planned operational improvements include:
- Automated backups
- Monitoring-driven incident creation
- NOC alert workflows
- Scheduled maintenance documentation
- Post-incident review templates

## Summary

This helpdesk environment is treated as a living system.

It is:
- Maintained deliberately
- Secured intentionally
- Documented continuously
- Designed for failure and recovery

Operations and maintenance are not optional.
They are the proof that this lab mirrors real enterprise IT.
