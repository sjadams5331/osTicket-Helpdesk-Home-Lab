# Architecture (osTicket Helpdesk Home Lab)

## Purpose
This document describes the architecture of the osTicket Helpdesk Home Lab, including system components, network layout, and the primary data flows between users, osTicket, the database backend, and Active Directory (LDAPS). The design goal is to simulate a small-to-mid-size enterprise service desk platform integrated with centralized identity.

## High-Level Summary
This lab uses a **single Debian 12 application server** hosting osTicket and its supporting services (Apache/PHP and MariaDB). Authentication is centralized through **Microsoft Active Directory** using **LDAP over SSL (LDAPS)**. The environment runs on **Oracle VirtualBox** with internal lab networking to allow controlled communication between the osTicket server and the Domain Controller.

## Components

### Virtual Machines
- **osticket01** (Debian 12)
  - Hosts osTicket v1.18.x
  - Apache 2 + PHP 8.2 application stack
  - MariaDB database backend
  - Acts as the web application and database server in this lab

- **dc01** (Windows Server, Active Directory)
  - AD DS for `lab.local`
  - DNS for `lab.local`
  - Certificate Services (internal Microsoft CA) used to support LDAPS
  - Provides directory authentication and identity lookups for osTicket

## Network Layout

### VirtualBox Networking (Typical Lab Design)
This lab is designed so the VMs can communicate with each other on an isolated network while still allowing optional internet access for updates.

Common patterns:
- **Host-Only Network** (internal lab traffic)
  - Used for AD and osTicket communication
  - Example DC IP: `192.168.56.103`

![Network Layout](../screenshots/arch-virtualbox-networking.png)

- **NAT Adapter** (optional outbound internet access)
  - Used for package updates and downloads
  - Not required for internal authentication flows

## Key Hostnames / Identity
- **AD Domain:** `lab.local`
- **Domain Controller:** `dc01.lab.local`
- **DC IP:** `192.168.56.103`
- **osTicket Server:** `osticket01.lab.local`
- **Service Account:** `svc_osticket@lab.local`
- **Authentication URI:** `ldaps://dc01.lab.local:636`

## Ports and Protocols

### osTicket Server (osticket01)
- **TCP 80**: HTTP (lab/testing)
- **TCP 443**: HTTPS (recommended for production-style setup; may be a future enhancement)
- **Local socket/TCP 3306**: MariaDB (restricted to local access where possible)

### Domain Controller (dc01)
- **TCP 636**: LDAPS (required for secure LDAP binds)
- **TCP/UDP 53**: DNS (for `lab.local` name resolution, if used)

## Trust and Certificate Model (LDAPS)
LDAPS requires the client (Debian/osTicket server) to trust the certificate presented by the Domain Controller. In this lab:

- The **AD Certificate Authority** issues the LDAPS certificate (directly or via auto-enrollment).
- The Debian server is configured to **trust the internal Microsoft CA**.
- osTicket is configured to bind to AD over `ldaps://` to protect credentials and directory queries in transit.

![Trust and Certificate Model](../screenshots/LDAP-installed.png)

This design mirrors enterprise environments where internal PKI is used to secure authentication and service-to-service communication.

## Data Flow

### 1) User Ticket Submission (Authenticated User)
1. User browses to the osTicket web portal on `osticket01`
2. User authenticates using AD credentials (via osTicket LDAP authentication)
3. osTicket queries AD over LDAPS for authentication and user attributes
4. User submits a ticket through the portal
5. osTicket writes ticket data to MariaDB

**Flow:**
User Browser → Apache/PHP (osTicket) → (LDAPS) Active Directory  
osTicket → MariaDB

### 2) Agent Ticket Handling (Helpdesk / NOC)
1. Agent logs into the osTicket agent portal
2. Agent authenticates via AD (LDAPS)
3. Agent triages and responds to tickets
4. Ticket updates and notes are stored in MariaDB
5. Role-based access control limits what the agent can view/change

**Flow:**
Agent Browser → Apache/PHP (osTicket) → (LDAPS) Active Directory  
osTicket → MariaDB

### 3) Directory Authentication (LDAPS)
1. osTicket binds to AD using the service account (`svc_osticket@lab.local`) for directory lookup/search
2. User authentication is validated against AD using secure LDAP communication
3. TLS trust is validated using the internal Microsoft CA chain installed on Debian

**Flow:**
osTicket → (TLS/LDAPS:636) → dc01.lab.local

## Security Boundaries and Assumptions
- End users have **no server access** and interact only with the web portal.
- Agents have **application-level access** governed by RBAC (roles/departments).
- Server administration (Linux and database) is restricted to administrators.
- Directory communication is encrypted using LDAPS to avoid credential exposure.
- MariaDB is intended to be restricted to local access on `osticket01` where feasible.

## Design Decisions
- **Single-server osTicket deployment** keeps complexity low while still reflecting common SMB/departmental enterprise setups.
- **LDAPS integration** reflects real enterprise expectations for secure centralized authentication.
- **Internal CA trust** mirrors production patterns and demonstrates PKI fundamentals.
- **VirtualBox isolation** allows safe testing of authentication, RBAC, and workflows without exposing services publicly.
