# Site B — Secondary Data Center
# On-Premises Infrastructure Modernization

[English](site-b-on-premises.md) | [Português](site-b-on-premises.pt-BR.md)

## 1. Architecture Overview

The secondary data center was the organization's second most important infrastructure site.

The initial environment consisted of more than 10 standalone physical servers running legacy VMware versions 5.5 and 6.5, without centralized vCenter management, structured backup capabilities, or standardized infrastructure governance.

The transformation established a new enterprise virtualization platform, incorporating modern compute, block storage, network switching, firewall segmentation, and workload-level security.

The project included technical and executive leadership throughout the modernization lifecycle, from architecture design and business case development to implementation and operational transition.

## 2. Legacy Environment — Before Modernization

| Component | Legacy Environment |
|---|---|
| Physical Servers | More than 10 standalone servers |
| Virtualization | VMware 5.5 and 6.5 |
| Virtualization Management | No centralized vCenter |
| Compute Architecture | Standalone hosts |
| Backup | No structured backup solution |
| Governance | No standardized processes |
| Security | Infrastructure modernization and vulnerability remediation required |

### Key Challenges

- Standalone virtualization hosts.
- Lack of centralized infrastructure management.
- Legacy virtualization versions.
- Absence of structured backup and recovery.
- Lack of standardized documentation and asset inventory.
- Need for improved network and workload security.

## 3. Target Architecture — Enterprise VMware Cluster

The target infrastructure was designed around a new four-node VMware cluster.

### Compute and Virtualization

| Component | Technology |
|---|---|
| Server Platform | Dell PowerEdge R760 |
| Cluster Size | 4 compute nodes |
| Hypervisor | VMware vSphere 8 |
| Centralized Management | VMware vCenter |
| High Availability | VMware HA |
| Resource Management | VMware DRS |

The new cluster established centralized virtualization management and high availability capabilities.

### Storage Architecture

| Component | Technology |
|---|---|
| Storage Platform | Dell PowerVault ME5224 |
| Storage Type | Enterprise Block Storage |
| Connectivity Protocol | iSCSI |
| Physical Connectivity | Direct Attach Copper (DAC) |

The PowerVault ME5224 provided the block storage platform for the VMware environment, connected through iSCSI.

### Network Architecture

| Network Layer | Technology | Responsibility |
|---|---|---|
| Layer 2 | Dell PowerSwitch S5224F-ON | Top-of-Rack switching |
| Layer 3 | FortiGate | Routing and network segmentation |
| Network Segmentation | VLANs | Logical network separation |
| Workload Security | Illumio / Guardicore | Virtual machine segmentation |

The architecture combined enterprise switching, firewall-based segmentation, and software-defined workload security.

## 4. Security Architecture

The security model was designed using multiple complementary control layers.

### Network Security — FortiGate

FortiGate firewalls were used for:

- VLAN-based network segmentation.
- Layer 3 routing.
- Network traffic control.
- Segmentation between infrastructure and workload networks.

### Layer 2 Connectivity — Dell PowerSwitch

Dell PowerSwitch S5224F-ON switches provided the Top-of-Rack switching layer.

### Workload Segmentation — Illumio / Guardicore

Illumio / Guardicore software-based segmentation was implemented for virtual machine workloads, adding granular security controls beyond traditional network segmentation.

### Operating System Security

Security remediation activities included:

- Operating system vulnerability remediation.
- Operating system patch management.
- Third-party software patch management.
- Security improvements integrated into infrastructure modernization.

## 5. Backup, Availability and Disaster Recovery

The modernized environment incorporated:

- VMware HA.
- VMware DRS.
- Veeam Backup & Replication v12.
- RTO and RPO definition and validation.
- Infrastructure and application restore testing.
- Step-by-step recovery procedures.
- Recorded test evidence with business stakeholder participation.

Recovery testing was documented to validate technical procedures and business application recovery readiness.

## 6. Infrastructure Governance

The project established structured governance and operational management practices.

Key initiatives:

- Master asset inventory.
- Standardized infrastructure documentation.
- Operational procedures and technical runbooks.
- Operating system and third-party software patch management.
- Backup and restore documentation.
- Recovery test procedures and recorded evidence.
- Operational support and transition processes.

## 7. Project Leadership and Delivery

The project included end-to-end technical and executive leadership.

Key responsibilities:

- Target architecture and infrastructure topology design.
- Technology benchmarking and solution evaluation.
- Business case development.
- Budget presentation and justification to executive leadership.
- VMware cluster implementation.
- Infrastructure migration planning and execution.
- Security architecture implementation.
- Governance and operational process establishment.
- Transition to continuous infrastructure operations.

## 8. Strategic Outcomes

The modernization replaced a fragmented standalone virtualization environment with a centralized enterprise VMware architecture.

The resulting infrastructure established a stronger foundation for:

- Centralized virtualization management.
- High availability and resource management.
- Enterprise storage connectivity.
- Network and workload segmentation.
- Structured backup and recovery.
- Infrastructure governance and operational consistency.

---

*This architecture document describes an anonymized enterprise infrastructure transformation. Detailed configurations, network addresses, credentials, customer identities, and confidential operational information have been intentionally excluded.*
