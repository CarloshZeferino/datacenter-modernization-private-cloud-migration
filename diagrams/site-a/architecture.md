# Site A — Headquarters Architecture

## 1. Before Migration — Legacy Data Center

```mermaid
flowchart TB
    DC["Headquarters — Legacy Data Center"]

    DC --> H["17+ Physical Servers"]
    H --> V55["VMware 5.5"]
    H --> V65["VMware 6.5"]

    V55 --> S["Standalone Hosts"]
    V65 --> S

    S --> ST["Legacy Storage Systems"]
    ST --> F["Disk Failures"]

    DC --> R["Infrastructure Risks"]
    R --> R1["No vCenter"]
    R --> R2["No Structured Backup"]
    R --> R3["Hardware Failures"]
    R --> R4["Security Vulnerabilities"]
    R --> R5["No Standardized Governance"]

flowchart TB
    GCVE["Google Cloud VMware Engine — GCVE"]

    GCVE --> VS["VMware vSphere 8"]
    VS --> HA["VMware HA"]
    VS --> DRS["VMware DRS"]
    VS --> NSX["VMware NSX"]

    NSX --> MS["Network Microsegmentation"]

    GCVE --> BK["Veeam Backup & Replication v12"]

    BK --> REC["Recovery Management"]
    REC --> RTO["RTO Definition and Validation"]
    REC --> RPO["RPO Definition and Validation"]
    REC --> TEST["Infrastructure and Application Restore Tests"]

    TEST --> BIZ["Business Stakeholder Validation"]
    BIZ --> EVID["Documented and Recorded Evidence"]
