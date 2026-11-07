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
