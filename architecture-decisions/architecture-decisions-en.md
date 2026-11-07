# Architecture Decisions & Technical Outcomes

## Overview

This document records the major architectural decisions made during the infrastructure modernization, private cloud migration, disaster recovery, connectivity, security, and automation initiatives.

The purpose is to provide technical context for each decision, document its implementation, and describe its architectural implications.

The records focus on confirmed project decisions and outcomes. Quantitative performance improvements, financial savings, and other metrics are not included where no validated figures are available.

---

## ADR-001 — Migration of Site A to Google Cloud VMware Engine (GCVE)

**Status:** Implemented

### Context

Site A hosted a VMware-based infrastructure that was selected for migration to Google Cloud VMware Engine (GCVE).

The migration required moving the virtualized infrastructure while preserving application availability, network integration, and operational continuity.

### Decision

Migrate the entire VMware infrastructure from Site A to GCVE, using a combination of:

- VMware Export/Import.
- RackWare migration capabilities.
- Lift-and-Shift migration strategy.
- Operating system vulnerability remediation.
- Application upgrades and migration to newer versions where required.
- VMware NSX for workload microsegmentation.

### Implementation

The migration was performed as part of the broader infrastructure modernization initiative.

The resulting architecture moved the virtualized infrastructure to GCVE while retaining only the Layer 2 and Layer 3 network infrastructure at the original physical site.

### Architectural Outcome

- Site A's virtualized infrastructure was migrated to GCVE.
- The original site retained its L2/L3 network infrastructure.
- VMware NSX provided workload microsegmentation.
- Operating system and application remediation activities were incorporated into the migration initiative.

---

## ADR-002 — Retention of Site B as an On-Premises VMware Environment

**Status:** Implemented

### Context

Site B required a local VMware infrastructure capable of supporting its workloads while remaining integrated into the broader enterprise architecture and disaster recovery strategy.

### Decision

Maintain Site B as an on-premises VMware environment using a dedicated compute and storage architecture.

### Implementation

The architecture included:

- VMware vCenter.
- A four-node compute and memory cluster.
- VMware HA and DRS.
- Dell PowerVault ME5224 block storage.
- iSCSI connectivity between compute and storage.
- Direct Attach Copper (DAC) cabling.
- Dell PowerSwitch S5224F-ON switching infrastructure.
- FortiGate firewalls for network segmentation, VLANs, and Layer 3 routing.

### Architectural Outcome

Site B remained an on-premises VMware environment, with dedicated compute and block storage resources.

The architecture maintained local workload execution while allowing integration with the disaster recovery environment hosted in GCVE.

---

## ADR-003 — Site B Disaster Recovery Through Veeam Replication to GCVE

**Status:** Implemented

### Context

Site B required a disaster recovery strategy capable of supporting workload recovery outside the primary on-premises environment.

### Decision

Use Veeam Backup & Replication v12 to replicate Site B virtual machines to Google Cloud VMware Engine.

### Implementation

The disaster recovery architecture used:

- Veeam Backup & Replication v12.
- Veeam replication workflows.
- GCVE as the disaster recovery destination.
- VMware infrastructure capabilities at the recovery environment.

Disaster recovery validation included periodic restore and recovery exercises, with an annual simulation of a total Site B outage.

Recovery objectives were defined according to workload criticality, using Tier 0, Tier 1, Tier 2, and Tier 3 classifications.

### Architectural Outcome

- Site B workloads had a replication-based recovery path to GCVE.
- The architecture provided an alternative recovery environment outside the primary site.
- Recovery procedures were periodically validated through controlled exercises.

---

## ADR-004 — Veeam Scale-Out Backup Repository with Google Cloud Storage Coldline

**Status:** Implemented

### Context

The backup architecture required a strategy to manage backup storage capacity and use cloud object storage as an additional storage tier.

### Decision

Implement a Veeam Scale-Out Backup Repository (SOBR) using Capacity Tier to move backup data to Google Cloud Storage Coldline.

### Implementation

The architecture incorporated:

- Veeam Backup & Replication v12.
- Scale-Out Backup Repository.
- Capacity Tier.
- Google Cloud Storage Coldline.
- Local backup repositories at the infrastructure sites.

### Architectural Outcome

The backup architecture combined local backup repositories with cloud-based object storage.

Capacity Tier enabled the movement of backup data to Google Cloud Storage Coldline as part of the storage strategy.

---

## ADR-005 — Site-Specific Network Segmentation Architecture

**Status:** Implemented

### Context

The two sites had different infrastructure architectures and required network segmentation mechanisms aligned with their respective environments.

### Decision

Use VMware NSX for workload microsegmentation at Site A and FortiGate-based segmentation at Site B.

### Implementation

**Site A**

- VMware NSX for workload microsegmentation.
- FortiGate for perimeter security and network connectivity.
- L2/L3 network infrastructure retained at the original physical site after migration to GCVE.

**Site B**

- FortiGate-based network segmentation.
- VLAN separation.
- Layer 3 routing through FortiGate.

### Architectural Outcome

Each site implemented a segmentation architecture aligned with its infrastructure model.

Site A used VMware-native microsegmentation, while Site B used firewall-based segmentation and routing.

---

## ADR-006 — Redundant Connectivity to Google Cloud Through Equinix Partner Interconnect

**Status:** Implemented

### Context

The enterprise environment required resilient connectivity between the on-premises infrastructure and Google Cloud.

### Decision

Use Equinix Enterprise Connectivity to establish Google Cloud Partner Interconnect connectivity, with redundant circuits and BGP routing.

### Implementation

The connectivity architecture included:

- Equinix as the connectivity partner.
- Google Cloud Partner Interconnect.
- Two independent circuits.
- Physically diverse circuit locations.
- Redundant equipment and network paths.
- BGP routing.
- FortiGate firewalls at both sites.

Internet and Google Cloud connectivity were integrated through the firewall infrastructure at both sites.

### Architectural Outcome

The architecture provided redundant connectivity paths between the enterprise infrastructure and Google Cloud.

Physical path diversity and BGP routing were incorporated into the connectivity design to support network resilience.

---

## ADR-007 — Infrastructure Automation Toolchain

**Status:** Implemented

### Context

Infrastructure provisioning and configuration activities required a consistent automation approach across Google Cloud, VMware, and on-premises environments.

### Decision

Adopt a multi-tool automation architecture using Terraform, Ansible, Packer, and Azure DevOps.

### Implementation

The toolchain was divided by responsibility:

| Technology | Responsibility |
|---|---|
| Terraform | Infrastructure provisioning across GCP, VMware, and on-premises environments |
| Ansible | Server configuration and software installation |
| Packer | Server image creation |
| Azure DevOps | Corporate automation pipelines |
| PowerShell | Windows Server and Active Directory automation |
| Bash | Linux administration and automation |

Azure DevOps pipelines executed Terraform, Ansible, and Packer workflows automatically.

GitHub was also used for personal laboratory projects.

### Architectural Outcome

The automation toolchain provided a common approach for infrastructure provisioning, server configuration, and image creation across different platforms.

---

## Consolidated Architectural Outcomes

The decisions documented in this chapter established the following architecture:

1. Site A's virtualized infrastructure was migrated to GCVE, retaining only L2/L3 network infrastructure at the original site.
2. Site B remained an on-premises VMware environment with dedicated compute and storage resources.
3. Site B disaster recovery was integrated with GCVE through Veeam replication.
4. Backup storage incorporated Veeam SOBR Capacity Tier and Google Cloud Storage Coldline.
5. Network segmentation was implemented using VMware NSX at Site A and FortiGate at Site B.
6. Google Cloud connectivity used Equinix Partner Interconnect, redundant circuits, and BGP.
7. Infrastructure automation was implemented using Terraform, Ansible, Packer, and Azure DevOps.

## Documentation Scope and Limitations

These ADRs describe confirmed architectural decisions and their implementation.

The following details are intentionally not quantified because validated project figures have not been provided:

- Migration duration and workload counts.
- Infrastructure cost reduction.
- Performance improvements.
- Network bandwidth and latency.
- Backup capacity and retention periods.
- Measured RPO and RTO values.
- Availability percentages.

These records can be expanded with validated project metrics and supporting evidence as they become available.
