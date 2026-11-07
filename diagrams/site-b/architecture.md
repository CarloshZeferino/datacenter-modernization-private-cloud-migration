
# Site B — Architecture Before & After

## 1. BEFORE — Legacy Infrastructure

```mermaid
flowchart TB
    USERS[Users and Applications]
    NETWORK[Flat Network<br/>No Network Segmentation]

    subgraph LEGACY["Previous Infrastructure"]
        HOSTS[VMware Standalone Hosts<br/>No Cluster]
        DISKS[Internal Server Disks<br/>Local Storage]
        HOSTS --> DISKS
    end

    USERS --> NETWORK
    NETWORK --> HOSTS
```

## 2. AFTER — Modernized Infrastructure

```mermaid
flowchart TB
    USERS[Users and Applications]

    FW[FortiGate<br/>Firewall and Layer 3 Routing]
    VLAN[VLAN Segmentation]

    SW[Dell PowerSwitch S5224F-ON<br/>Network Switching]

    subgraph CLUSTER["VMware Virtualization Cluster"]
        VC[vCenter Server]
        N1[Compute Node 1]
        N2[Compute Node 2]
        N3[Compute Node 3]
        N4[Compute Node 4]

        VC --- N1
        VC --- N2
        VC --- N3
        VC --- N4

        HA[VMware HA and DRS]
    end

    STORAGE[Dell PowerVault ME5224<br/>Shared Block Storage]

    USERS --> FW
    FW --> VLAN
    VLAN --> SW

    SW --> N1
    SW --> N2
    SW --> N3
    SW --> N4

    SW <-->|iSCSI over DAC| STORAGE

    HA -.-> N1
    HA -.-> N2
    HA -.-> N3
    HA -.-> N4
```

---

**Note:** Conceptual architecture diagrams. They do not represent exact physical connections, quantities of network links or detailed configurations.
