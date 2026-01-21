# Troubleshooting and Incident Resolution

## Purpose

This document describes **realistic failure scenarios, troubleshooting methodology, and incident resolution practices** used within the helpdesk environment.

The objective is not to suggest that failures are rare.  
The objective is to demonstrate that failures are:
- Detected deliberately
- Diagnosed methodically
- Resolved safely
- Documented clearly
- Used to improve operations

In enterprise IT, troubleshooting competence matters more than initial setup.

## Troubleshooting Methodology

All incidents follow a structured troubleshooting framework:

1. Identify reported symptoms
2. Confirm scope and business impact
3. Isolate the affected system or dependency
4. Apply corrective action within authority
5. Verify resolution
6. Document root cause and outcome

Guessing is avoided.  
Changes are intentional.  
Fixes are repeatable.

## Failure Domains

Incidents are categorized by **system dependency**, not symptom alone.

### Identity and Authentication
- Active Directory availability
- LDAP / LDAPS connectivity
- Service account permissions
- Certificate trust failures
- Time synchronization issues

### Application (osTicket)
- Agent authentication failures
- Role or department misalignment
- SLA assignment errors
- Workflow enforcement issues

### Infrastructure
- Network connectivity and DNS
- Service availability (Apache, MariaDB)
- Disk space or resource exhaustion
- Post-maintenance service failures

## Documented Incident Scenarios

### Incident 1: Agent Unable to Authenticate via Active Directory

**Reported Symptoms**
- Some agents authenticate successfully
- Other agents receive authentication failures
- Local osTicket authentication is disabled

**Initial Handling**
- Tier 1 validated issue scope
- Confirmed no global authentication outage
- Verified LDAP plugin operational

**Escalation**
- Escalated to Tier 2 due to identity-related scope

**Root Cause**
- Active Directory group membership mismatch
- Role mapping inconsistency between AD and osTicket

**Resolution**
- Corrected group membership
- Verified LDAP lookup behavior
- Confirmed role assignment within osTicket

**Outcome**
- Authentication restored
- Group membership documentation updated

### Incident 2: Incorrect SLA Assignment on New Tickets

**Reported Symptoms**
- Tickets defaulting to incorrect SLA
- Response timers inconsistent with issue priority

**Initial Handling**
- Tier 1 reproduced issue across multiple tickets
- Confirmed issue not user-specific

**Escalation**
- Tier 2 reviewed workflow and help topic configuration

**Root Cause**
- Help topic incorrectly mapped to SLA
- Workflow evaluation order misconfigured

**Resolution**
- Corrected help topic rules
- Validated SLA assignment logic

**Outcome**
- SLA timers functioning as designed
- Workflow documentation updated

### Incident 3: osTicket Web Interface Unreachable After Maintenance

**Reported Symptoms**
- HTTP access unavailable
- Server reachable via network
- Database service operational

**Initial Handling**
- Tier 1 confirmed infrastructure reachability
- Identified application-level failure

**Escalation**
- Tier 2 assumed remediation authority

**Root Cause**
- Apache service failed to restart after system update
- Configuration reload error detected in logs

**Resolution**
- Apache service restarted
- Configuration validated
- Logs reviewed for recurring indicators

**Outcome**
- Web interface restored
- Maintenance checklist updated

## Escalation Decision Matrix

| Indicator                      | Tier 1 | Tier 2 | NOC |
|-------------------------------|--------|--------|-----|
| Single-user issue             | ✓      |        |     |
| Multi-user impact             |        | ✓      |     |
| Authentication system failure |        | ✓      |     |
| Infrastructure outage         |        |        | ✓   |
| SLA breach imminent           |        | ✓      |     |

Escalation is driven by **impact and authority**, not guesswork.

## Evidence Collection and Logging

During troubleshooting:
- Relevant system logs are reviewed
- Authentication events are examined
- Configuration changes are documented
- Timestamps are preserved for correlation

Evidence is treated as part of the resolution, not an afterthought.

## Post-Incident Actions

After incident resolution:
- Root cause is documented
- Knowledge Base updated where appropriate
- Tier 1 guidance refined
- Preventative controls identified

Troubleshooting feeds directly into **operational improvement**, not just ticket closure.

## Failure Scenarios Explicitly Accounted For

This environment plans for:
- Domain Controller downtime
- LDAPS certificate expiration
- Service account password expiration
- Database connectivity loss
- Network or DNS misconfiguration

Each scenario has a defined escalation and response path.

## Why This Matters

Anyone can follow installation guides.  
Not everyone can:
- Diagnose layered failures
- Escalate appropriately
- Preserve audit trails
- Prevent recurrence

This troubleshooting framework demonstrates **operational maturity**, not just technical familiarity.

## Summary

Failures are expected.  
Silence is suspicious.

This lab demonstrates the ability to:
- Detect issues
- Resolve them safely
- Learn from failures
- Improve the system over time

Troubleshooting is not a weakness.  
It is proof that the environment is real.
