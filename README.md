# osTicket Helpdesk Home Lab (Enterprise Simulation)

## Overview
This project is a fully implemented **osTicket helpdesk deployment** designed to simulate a real-world enterprise IT service desk integrated with Active Directory. The lab demonstrates end-to-end service desk operations including centralized authentication, role-based access control, SLA-driven workflows, and realistic ticket lifecycles aligned with desktop support and NOC-style environments.

The environment mirrors how a small-to-mid-size organization might deploy and operate a production helpdesk platform. Emphasis is placed on security, operational workflows, and documentation quality rather than basic application installation.

## Lab Environment
- **Hypervisor:** Oracle VirtualBox  
- **Operating System:** Debian GNU/Linux 12 (Bookworm)  
- **Web Server:** Apache 2  
- **Application Stack:** PHP 8.2  
- **Database:** MariaDB  
- **Ticketing Platform:** osTicket v1.18.x  
- **Directory Services:** Microsoft Active Directory  
- **Authentication:** LDAP over SSL (LDAPS)

## Architecture & Design
The deployment follows a centralized, single-application server model commonly used in enterprise support environments:

- Dedicated Debian Linux server hosting osTicket
- Apache serving the web application
- PHP handling application logic
- MariaDB providing persistent data storage
- Windows Active Directory providing centralized identity management
- Secure LDAPS communication for authentication

The architecture prioritizes operational realism while maintaining enterprise-aligned security practices.

## Authentication & Identity Integration
The helpdesk is fully integrated with Active Directory using **LDAP over SSL (LDAPS)** to provide centralized authentication and identity consistency.

### Active Directory Configuration
- **Domain:** lab.local  
- **Domain Controller:** dc01.lab.local  
- **LDAPS Port:** 636  
- **Service Account:** svc_osticket@lab.local  

The Debian server trusts the internal Microsoft Certificate Authority, ensuring encrypted and validated directory communication.

### Authentication Model
- End users authenticate using Active Directory credentials
- Support agents authenticate using Active Directory accounts
- The service account is restricted to directory read operations
- All directory communication is encrypted using TLS

## Role-Based Access Control (RBAC)
Access within osTicket is controlled through departments, roles, and permission sets designed to enforce separation of duties.

### Defined Roles
- **Tier 1 Support**
  - User-facing ticket handling
  - Basic troubleshooting and resolution
- **Tier 2 Support**
  - Ticket escalation and reassignment
  - Priority and SLA adjustments
- **NOC / Infrastructure**
  - Infrastructure-focused ticket queues
  - Limited exposure to user data
- **Administrator**
  - Full system configuration and management

Roles are mapped to departments and reflect typical enterprise service desk structures.

## Helpdesk Workflows

### Ticket Intake
- Web-based user portal authenticated via Active Directory
- Categorized help topics aligned with enterprise service catalogs
- Department-based ticket routing

### Ticket Lifecycle
1. Ticket submission
2. Automatic categorization and routing
3. Agent assignment
4. User communication and internal notes
5. Escalation or reassignment as required
6. Resolution and closure
7. Automated post-resolution handling

### Service Level Agreements (SLAs)
- Priority-based SLAs (P1–P3)
- Response and resolution targets
- SLA enforcement based on ticket category and department

## Security Considerations

### Application Security
- Role-based permission enforcement
- Separation of user, agent, and admin interfaces
- Removal of installation artifacts post-deployment

### Server Security
- Dedicated database user for osTicket
- Restricted file permissions and ownership
- Service isolation between Apache, database, and system users

### Directory Security
- Encrypted LDAPS communication
- Least-privilege service account usage
- Certificate-based trust validation

## Validation & Testing
The deployment was validated through:
- Successful Active Directory-authenticated user logins
- Successful agent authentication with role enforcement
- Creation, routing, escalation, and resolution of test tickets
- SLA enforcement verification
- Service restarts without configuration loss
- Validation of secure LDAPS communication

## Troubleshooting & Lessons Learned
Issues were resolved using standard enterprise troubleshooting practices, including:
- Apache and PHP log analysis
- PHP extension dependency resolution
- Database authentication troubleshooting
- File permission and ownership correction
- Certificate trust validation for LDAPS

Reinstallation was intentionally avoided in favor of controlled troubleshooting.

## Documentation
Supporting documentation, configuration notes, and screenshots are available in the `/docs` and `/screenshots` directories.

## Skills Demonstrated
- Linux server administration (Debian)
- Web application deployment and hardening
- Apache and PHP configuration
- MariaDB administration
- Active Directory integration using LDAPS
- Role-based access control design
- Service desk and NOC-style workflows
- SLA design and enforcement
- Log analysis and troubleshooting
- Enterprise technical documentation
