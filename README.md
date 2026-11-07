# Enterprise Data Center Modernization & Private Cloud Migration

**Infrastructure Architecture | VMware | Google Cloud VMware Engine | Cybersecurity | IT Governance**

[English](README.md) | [Português](README.pt-BR.md)

---

## Executive Summary

This case study presents an enterprise infrastructure transformation program involving two critical data center environments.

The initiative combined private cloud migration, on-premises infrastructure modernization, cybersecurity improvements, business continuity, and IT governance.

The transformation addressed legacy infrastructure, virtualization obsolescence, hardware failures, security vulnerabilities, and the absence of structured backup and operational governance.

### Transformation Overview

| Environment | Transformation Strategy | Target Architecture |
|---|---|---|
| Site A – Headquarters | Data center migration | Google Cloud VMware Engine (GCVE) |
| Site B – Secondary Site | On-premises modernization | New VMware vSphere 8 cluster |

## Key Technologies

- VMware vSphere 8, vCenter, HA and DRS
- Google Cloud VMware Engine (GCVE)
- VMware NSX
- RackWare migration tooling
- Veeam Backup & Replication v12
- Dell PowerEdge R760
- Dell PowerVault ME5224
- Dell PowerSwitch S5224F-ON
- FortiGate
- Illumio / Guardicore
- iSCSI and DAC connectivity

## Transformation Workstreams

### 1. Infrastructure Assessment
- Infrastructure inventory and technical assessment.
- Identification of hardware obsolescence and vulnerabilities.
- Legacy virtualization assessment.
- Technical documentation and dependency mapping.

### 2. Cloud Migration
- Migration of the primary data center to GCVE.
- VMware Export/Import and RackWare.
- Lift and Shift migration strategies.
- Operating system modernization during migration.

### 3. On-Premises Modernization
- Deployment of a four-node VMware cluster.
- Dell enterprise compute and storage architecture.
- Centralized virtualization management.
- Modernized network and storage connectivity.

### 4. Security Architecture
- VMware NSX microsegmentation at headquarters.
- FortiGate network segmentation and VLAN architecture at the secondary site.
- Illumio / Guardicore workload segmentation.
- Operating system and third-party software vulnerability remediation.

### 5. Backup, Recovery & Business Continuity
- Veeam Backup & Replication v12.
- RTO and RPO definition and validation.
- Infrastructure and application restore testing.
- Business stakeholder participation in recovery exercises.
- Recorded evidence and step-by-step recovery documentation.

### 6. IT Governance & Operations
- Master asset inventory.
- Infrastructure documentation.
- Operational procedures and technical runbooks.
- Patch management processes.
- Operational readiness and transition to support.

## Project Leadership

Technical and executive leadership across the transformation lifecycle, including assessment, architecture design, technology benchmarking, business case development, executive budget presentation, migration execution, security improvements, governance implementation, and operational transition.

## Project Documentation

| Documentation | Description |
|---|---|
| [Executive Overview](docs/executive-overview.md) | Project context and strategic objectives |
| Infrastructure Assessment | Legacy environment and identified risks |
| Migration Strategy | Migration methodologies and execution |
| Target Architecture | Architecture of both environments |
| Security Architecture | Network and workload security |
| Backup & Disaster Recovery | Backup, RTO, RPO and recovery validation |
| Governance & Operations | Asset management and operational processes |

## Strategic Outcomes

The transformation established two complementary infrastructure platforms while strengthening security, availability, recoverability, documentation, and operational governance.

---

*This case study describes professional experience in an anonymized enterprise environment. Confidential organizational information and sensitive infrastructure details have been intentionally excluded.*
