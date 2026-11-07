# Site A — Headquarters
# Google Cloud VMware Engine (GCVE) Architecture

[English](site-a-gcve.md) | [Português](site-a-gcve.pt-BR.md)

## 1. Architecture Overview

The organization's headquarters hosted the primary data center and represented the most critical infrastructure environment within the transformation program.

The initial assessment identified significant infrastructure obsolescence, hardware reliability issues, storage failures, security vulnerabilities, and the absence of centralized virtualization management and structured backup processes.

The strategic decision was to migrate the primary data center to Google Cloud VMware Engine (GCVE), establishing a modern private cloud infrastructure reference for the organization.

## 2. Legacy Environment — Before Migration

The assessment identified the following conditions:

| Component | Legacy Environment |
|---|---|
| Physical Servers | More than 17 servers |
| Virtualization | VMware 5.5 and 6.5 |
| Virtualization Management | Standalone hosts, no vCenter |
| Storage | Legacy storage systems |
| Storage Health | Disk failures |
| Hardware Management | Lack of centralized iDRAC management |
| Backup | No structured backup solution |
| Governance | No standardized infrastructure governance |
| Security | Identified vulnerabilities and outdated operating systems |

### Key Challenges

- Hardware obsolescence and reliability issues.
- Storage failures and operational risks.
- Fragmented virtualization management.
- Lack of centralized infrastructure visibility.
- Security vulnerabilities across the infrastructure.
- Absence of structured backup and recovery processes.
- Limited operational documentation and asset inventory.

## 3. Target Environment — Google Cloud VMware Engine

The target architecture was based on Google Cloud VMware Engine (GCVE), providing a private cloud platform for the organization's primary VMware workloads.

### Architecture Components

| Domain | Technology |
|---|---|
| Private Cloud Platform | Google Cloud VMware Engine |
| Virtualization | VMware vSphere 8 |
| Network Microsegmentation | VMware NSX |
| Migration Tooling | RackWare |
| Migration Methods | VMware Export/Import and Lift and Shift |
| Backup and Recovery | Veeam Backup & Replication v12 |
| Availability | VMware HA and DRS |

## 4. Migration Strategy

The migration combined different approaches according to workload characteristics and technical requirements.

### VMware Export/Import

Export and import procedures were used to move virtual machines from the legacy VMware environment into the target infrastructure.

### RackWare

RackWare migration tooling was used to support workload migration activities.

### Lift and Shift

Application workloads were migrated while maintaining their operational characteristics where appropriate.

### Progressive Workload Modernization

The migration process also incorporated improvements to the workloads:

- Operating system upgrades.
- Remediation of operating system vulnerabilities.
- Migration of applications to updated operating system versions.
- Alignment of workload security with the target architecture.

## 5. Security Architecture — VMware NSX

VMware NSX was adopted for network virtualization and microsegmentation.

The security strategy incorporated network-level controls and workload-level policies, allowing security requirements to evolve during the migration process.

Key initiatives:

- Implementation and adjustment of network microsegmentation.
- Progressive application of workload security policies.
- Operating system vulnerability remediation.
- Reduction of legacy operating system exposure.
- Integration of security improvements into migration activities.

## 6. Availability, Backup and Recovery

The target environment incorporated:

- VMware HA.
- VMware DRS.
- Veeam Backup & Replication v12.
- RTO and RPO definition and validation.
- Infrastructure and application restore testing.
- Step-by-step recovery documentation.
- Recorded recovery tests involving business stakeholders.

Recovery procedures were documented and validated with the respective business areas, maintaining evidence of the execution and results.

## 7. Governance and Operational Readiness

The transformation included the establishment of structured infrastructure governance:

- Master asset inventory.
- Infrastructure technical documentation.
- Standardized operational procedures.
- Operating system and third-party software patch management.
- Backup and restore procedures.
- Recovery test documentation and evidence.
- Operational transition and ongoing support processes.

## 8. Strategic Outcomes

The migration established GCVE as the organization's primary private cloud infrastructure reference.

The transformation addressed legacy infrastructure risks while combining workload migration, operating system modernization, security improvements, backup implementation, and operational governance.

The resulting architecture provided a foundation for future infrastructure modernization initiatives.

---

*This architecture document describes an anonymized enterprise infrastructure transformation. Detailed configurations, network addresses, credentials, customer identities, and confidential operational information have been intentionally excluded.*
