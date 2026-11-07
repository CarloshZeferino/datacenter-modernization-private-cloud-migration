# Datacenter Modernization — Challenges, Solutions & Outcomes

## 1. Executive Summary

This case study describes a corporate infrastructure transformation involving two datacenter environments with different architectural objectives.

The initiative combined infrastructure modernization, vulnerability remediation, security hardening, workload migration, network resilience, backup modernization, disaster recovery, automation, and operational governance.

The transformation followed two distinct infrastructure strategies:

- **Site A:** Migration of the virtualized infrastructure to Google Cloud VMware Engine (GCVE), retaining the Layer 2 and Layer 3 network infrastructure at the original physical site.
- **Site B:** Modernization of the on-premises VMware environment, including compute, storage, network segmentation, and disaster recovery integration with GCVE.

The project also strengthened security and operational practices through centralized identity management, privileged access controls, vulnerability assessment and remediation workflows, infrastructure monitoring, automated incident management, and change governance.

Rather than applying a single architecture to both locations, the initiative adopted solutions according to each site's technical requirements and operational role.

## 2. Business Context

The organization required an infrastructure modernization strategy capable of addressing several interconnected objectives:

- Modernize the existing datacenter infrastructure.
- Address infrastructure vulnerabilities and improve security configuration.
- Evolve the infrastructure architecture while maintaining business application availability requirements.
- Establish resilient connectivity between corporate environments and Google Cloud.
- Improve backup and disaster recovery capabilities.
- Standardize infrastructure provisioning and configuration processes.
- Strengthen monitoring, incident management, and operational governance.
- Align recovery objectives with business and application criticality.

The transformation was therefore broader than a hardware or virtualization refresh. It involved architecture, security, connectivity, operational processes, and business continuity.

## 3. Transformation Challenges

The project required coordinated engineering across multiple infrastructure domains.

### 3.1 Infrastructure modernization

The two sites required different modernization approaches. Site A was migrated to GCVE, while Site B retained an on-premises architecture and received a redesigned compute, storage, and network foundation.

### 3.2 Vulnerability remediation and security hardening

Infrastructure modernization needed to be accompanied by vulnerability remediation and configuration hardening across virtualization, operating systems, network devices, storage systems, physical servers, and virtual machines.

### 3.3 Workload migration and compatibility

The Site A migration required workload transition to GCVE, including VMware-based migration activities, Lift and Shift practices, and application modernization where required.

### 3.4 Network resilience and cloud connectivity

The architecture required reliable connectivity between the corporate sites and Google Cloud, with independent physical circuits, redundant paths, and dynamic routing.

### 3.5 Business continuity and recovery

Backup and disaster recovery capabilities needed to support different recovery requirements according to workload criticality, including replication of Site B virtual machines to GCVE.

### 3.6 Operational standardization

The transformation also required repeatable provisioning, configuration management, monitoring, incident handling, change management, and technical documentation.

## 4. Security and Vulnerability Remediation Strategy

Security remediation was treated as an ongoing workstream throughout infrastructure modernization.

### 4.1 Vulnerability assessment and remediation workflow

The organization used **Tenable** for vulnerability assessment and **ManageEngine** to support patch deployment and remediation activities.

The operational workflow included:

1. The security team generated vulnerability reports.
2. Findings were classified by severity: Critical, High, Medium, and Low.
3. Remediation deadlines were established according to severity.
4. Infrastructure teams performed the required corrections using ManageEngine or specific technical procedures.
5. New Tenable scans were conducted to validate remediation.

This process provided a repeatable mechanism for identifying, prioritizing, addressing, and validating infrastructure vulnerabilities.

### 4.2 Infrastructure hardening

Hardening activities covered:

- VMware ESXi and vCenter.
- Windows Server and Linux operating systems.
- Network switches, firewalls, and routers.
- Dell storage systems.
- Physical servers and virtual machines.

Configuration baselines and recommendations were based on CIS Benchmarks, internal security policies, vendor recommendations, and established technical procedures.

### 4.3 Identity and privileged access management

Centralized identity management was provided through Active Directory, supported by security groups and role-based access control (RBAC).

Administrative access controls included:

- Named administrator accounts.
- Multi-factor authentication (MFA).
- Separation between privileged and everyday accounts.
- Administrative access through a Privileged Access Management (PAM) solution.
- Administrative access hierarchy using security tiers 0, 1, and 2.

**BeyondTrust** supported privileged access governance through password vaulting, session recording and auditing, access approvals, automatic password rotation, controlled remote access, and session duration and schedule restrictions.

> **Important distinction:** Administrative security tiers 0, 1, and 2 represent privileged access boundaries. They are separate from workload service tiers 0, 1, 2, and 3, which represent business criticality and recovery requirements.

### 4.4 Change governance

Security and infrastructure changes followed a controlled Change Management process, including:

- Request for Change (RFC).
- Impact and risk assessment.
- Manager and/or Change Advisory Board (CAB) approval.
- Scheduled maintenance windows.
- Rollback planning.
- Post-implementation validation.

## 5. Two-Site Infrastructure Modernization

The project established two complementary infrastructure architectures.

| Domain | Site A | Site B |
|---|---|---|
| Infrastructure model | Google Cloud VMware Engine | On-premises VMware |
| Workload strategy | Migration to GCVE | Retained and modernized locally |
| Virtualization | VMware on GCVE | VMware vCenter cluster |
| Network security | FortiGate and VMware NSX | FortiGate-based segmentation |
| Microsegmentation | VMware NSX | FortiGate security policies and VLAN segmentation |
| Disaster recovery role | GCVE hosting migrated workloads and receiving Site B replicas | Source environment for VM replication to GCVE |

Both environments used VMware High Availability (HA) and Distributed Resource Scheduler (DRS).

## 6. Site A — Migration to Google Cloud VMware Engine

Site A underwent a full migration of its virtualized infrastructure to Google Cloud VMware Engine.

The migration strategy included VMware Export/Import activities, RackWare, and Lift and Shift practices, according to workload requirements.

Application modernization was also considered where necessary, including operating system vulnerability remediation and application upgrades to newer versions.

### 6.1 Target architecture

The resulting architecture moved the virtualized workloads to GCVE while retaining the Layer 2 and Layer 3 network infrastructure at the original physical site.

Key components included:

- Google Cloud
