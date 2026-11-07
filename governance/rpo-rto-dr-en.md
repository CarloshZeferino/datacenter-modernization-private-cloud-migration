
# RPO, RTO and Disaster Recovery

## 1. Overview

The business continuity and disaster recovery strategy was established to protect the infrastructure environments across Site A and Site B.

The solution leveraged Veeam Backup & Replication v12 as the data protection platform, with backup repositories distributed across local storage and Google Cloud Storage.

The objective was to establish recovery criteria, minimize operational impact and ensure infrastructure service restoration capabilities.

## 2. Recovery Point Objective (RPO)

RPO represents the maximum acceptable amount of data loss following an incident.

Recovery objectives must consider:

- Service criticality.
- Backup frequency.
- Job execution windows.
- Restore point retention.
- Business requirements.

**Defined RPO:** To be documented according to the objectives established for each service.

## 3. Recovery Time Objective (RTO)

RTO represents the maximum expected time required to restore a service following an outage.

The criteria include:

- Backup availability.
- Restore point identification time.
- Infrastructure processing capacity.
- Virtual machine recovery time.
- Technical and functional service validation.

**Defined RTO:** To be documented according to the objectives established for each service.

## 4. Disaster Recovery Strategy

The Disaster Recovery strategy was supported by the Veeam v12 backup architecture, including:

- Site A and Site B infrastructure protection.
- Centralized Veeam Backup Server at Site A.
- Veeam Backup Proxy at Site B.
- Local and cloud backup repositories.
- SOBR with Capacity Tier.
- Google Cloud Storage Coldline for backup storage.

## 5. Recovery Procedures

Recovery procedures included:

1. Incident identification.
2. Service impact assessment.
3. Identification of available restore points.
4. Selection of the appropriate backup.
5. Restore execution.
6. Virtual machine integrity validation.
7. Service validation with responsible business teams.
8. Evidence and recovery results documentation.

## 6. Recovery Testing

Infrastructure restore tests were performed using documented step-by-step procedures.

Activities included:

- Restore test execution.
- Procedure evidence collection.
- Recording recovery activities.
- Technical validation of restored environments.
- Results validation with business teams.

## 7. Governance and Continuous Improvement

Recovery processes should be periodically reviewed, considering infrastructure changes, service criticality and business requirements.

Test results should be used to identify opportunities for improving recovery procedures.

## 8. Conclusion

The implementation of recovery objectives, backup protection and restore testing established an operational foundation for infrastructure resilience and business continuity across both sites.

---

**Note:** RPO and RTO targets must be documented using actual business-approved values. Recovery test results must be distinguished from target objectives.
