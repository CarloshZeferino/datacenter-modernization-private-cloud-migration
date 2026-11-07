# Modernização de Data Center Corporativo e Migração para Private Cloud

**Arquitetura de Infraestrutura | Modernização de Data Center | Cloud Híbrida | Segurança | Continuidade de Negócios**

[English Version](README.md) | **Português**

---

## 1. Resumo Executivo

Este projeto apresenta uma iniciativa de modernização de infraestrutura corporativa, envolvendo a transformação de dois ambientes de data center e a criação de um novo ambiente de hospedagem em cloud, com foco em evolução tecnológica, segurança, resiliência operacional, continuidade de negócios e governança de TI.

A iniciativa contemplou três componentes principais:

- **Site A — Infraestrutura de Rede:** após a migração, permaneceu fisicamente ativo exclusivamente para suportar a infraestrutura de rede e os serviços de conectividade L2 e L3.
- **GCVE — Novo Site de Infraestrutura em Cloud:** recebeu toda a infraestrutura virtualizada anteriormente hospedada no Site A, passando a atuar como novo ambiente de hospedagem.
- **Site B — Data Center On-Premises:** permaneceu em operação local, passando por uma modernização de sua infraestrutura de virtualização, computação, armazenamento e rede.

O projeto também envolveu a evolução dos processos de segurança, conectividade, backup, disaster recovery, automação, monitoramento e governança operacional.

A documentação apresenta decisões arquiteturais, tecnologias utilizadas, estratégias de implementação, procedimentos técnicos e resultados da transformação.

## 2. Visão Geral da Transformação

### 2.1 Site A — Transformação para um Ambiente de Rede

O Site A passou por uma transformação significativa. Toda a infraestrutura virtualizada anteriormente hospedada nesse ambiente foi migrada para o Google Cloud VMware Engine (GCVE).

Após a migração, o Site A deixou de atuar como ambiente de hospedagem de workloads e permaneceu fisicamente ativo exclusivamente para manter a infraestrutura de rede e conectividade L2 e L3.

Principais características:

- Migração integral da infraestrutura virtualizada para GCVE.
- Manutenção da infraestrutura física de rede.
- Preservação dos serviços de conectividade L2 e L3.
- FortiGate para segurança de perímetro e conectividade.
- Conectividade com o ambiente GCVE.
- Descontinuação da hospedagem local dos workloads virtualizados.

A estratégia de migração envolveu abordagens de VMware Export/Import, RackWare e Lift and Shift, considerando as características e necessidades dos workloads.

Durante a transformação também foram realizadas atividades de correção de vulnerabilidades dos sistemas operacionais e atualização de aplicações para versões mais recentes.

### 2.2 GCVE — Novo Site de Infraestrutura em Cloud

O Google Cloud VMware Engine passou a funcionar como o novo ambiente de hospedagem da infraestrutura virtualizada migrada do Site A.

Esse novo ambiente foi estruturado para suportar os workloads corporativos, mantendo a utilização das tecnologias VMware em uma infraestrutura hospedada na Google Cloud Platform.

Principais componentes:

- Google Cloud VMware Engine (GCVE).
- VMware NSX para microsegmentação.
- VMware HA e DRS.
- FortiGate no contexto de segurança de perímetro e conectividade com o ambiente cloud.
- Workloads migrados do Site A.
- Integração com a estratégia de Disaster Recovery do Site B.

### 2.3 Site B — Modernização da Infraestrutura On-Premises

O Site B permaneceu em ambiente on-premises, passando por uma modernização de sua infraestrutura de virtualização, computação, armazenamento e rede.

Principais componentes:

- Cluster VMware vSphere 8 com quatro nós de computação.
- Servidores Dell PowerEdge R760.
- VMware vCenter, HA e DRS.
- Storage Dell PowerVault ME5224 com conectividade iSCSI.
- Interconexão por cabos DAC.
- Switches Dell PowerSwitch S5224F-ON.
- FortiGate para segmentação por VLANs e roteamento L3.
- Soluções Illumio/Guardicore no contexto de segurança e segmentação.
- Integração com a estratégia de Disaster Recovery baseada em Veeam e GCVE.

## 3. Arquitetura de Alto Nível

O diagrama abaixo representa conceitualmente a arquitetura resultante da transformação, destacando a separação entre a infraestrutura de rede remanescente no Site A, o novo ambiente de hospedagem GCVE e o data center on-premises do Site B.

```mermaid
flowchart TB

    subgraph SITEA["SITE A — INFRAESTRUTURA DE REDE"]
        A_NET["Infraestrutura Física de Rede"]
        A_L2L3["Conectividade L2 / L3"]
        A_FW["FortiGate"]

        A_NET --> A_L2L3
        A_L2L3 --> A_FW
    end

    subgraph GCVE["GCVE — NOVO SITE DE INFRAESTRUTURA EM CLOUD"]
        G_VMWARE["Google Cloud VMware Engine"]
        G_NSX["VMware NSX"]
        G_VMS["Workloads Virtuais Migrados"]

        G_VMWARE --> G_NSX
        G_NSX --> G_VMS
    end

    subgraph SITEB["SITE B — DATA CENTER ON-PREMISES"]
        B_FW["FortiGate"]
        B_SW["Dell PowerSwitch S5224F-ON"]
        B_VC["VMware vCenter / vSphere 8"]
        B_ESX["4 x Dell PowerEdge R760"]
        B_ST["Dell PowerVault ME5224"]
        B_SEG["Segmentação de Rede"]

        B_FW --> B_SW
        B_SW --> B_VC
        B_VC --> B_ESX
        B_ESX <-->|iSCSI / DAC| B_ST
        B_FW --> B_SEG
    end

    subgraph BACKUP["BACKUP E DISASTER RECOVERY"]
        VEEAM["Veeam Backup & Replication v12"]
        SOBR["Scale-Out Backup Repository"]
        GCS["Google Cloud Storage Coldline"]
    end

    A_FW <-->|Conectividade| G_VMWARE
    B_VC --> VEEAM
    VEEAM --> SOBR
    SOBR --> GCS
    VEEAM -->|"Replicação de VMs"| G_VMWARE
```

*Representação conceitual da arquitetura. Não representa todos os componentes físicos, caminhos de rede, configurações de conectividade ou detalhes de implementação.*

## 4. Principais Tecnologias

| Categoria | Tecnologias |
|---|---|
| Virtualização | VMware vSphere 8, vCenter, HA, DRS |
| Cloud | Google Cloud Platform, GCVE |
| Migração | RackWare, VMware Export/Import |
| Segurança | FortiGate, VMware NSX, Illumio/Guardicore |
| Computação | Dell PowerEdge R760 |
| Armazenamento | Dell PowerVault ME5224, iSCSI |
| Rede | Dell PowerSwitch S5224F-ON, DAC, SD-WAN, BGP |
| Conectividade Cloud | Equinix Enterprise Connectivity, Google Cloud Partner Interconnect |
| Backup e DR | Veeam Backup & Replication v12 |
| Cloud Storage | Google Cloud Storage Coldline |
| Automação | Terraform, Ansible, Packer |
| Monitoramento | Zabbix, Grafana |
| Segurança e Vulnerabilidades | Tenable, ManageEngine, BeyondTrust |
| Governança | ITSM, Change Management, Azure DevOps |

## 5. Frentes de Trabalho da Transformação

A iniciativa foi organizada em diferentes frentes técnicas e operacionais.

### 5.1 Modernização de Data Center e Cloud

Migração de workloads para GCVE, transformação do Site A em um ambiente dedicado à infraestrutura de rede e modernização do ambiente on-premises do Site B.

### 5.2 Arquitetura de Rede e Conectividade

Implementação de conectividade redundante, SD-WAN, BGP, Equinix Enterprise Connectivity e Google Cloud Partner Interconnect.

A arquitetura considerou circuitos independentes, caminhos físicos distintos e redundância de equipamentos e conectividade.

### 5.3 Segurança e Gestão de Vulnerabilidades

Fortalecimento dos controles de segurança, hardening, gestão de vulnerabilidades, controle de acesso privilegiado, microsegmentação e governança de mudanças.

Foram utilizados controles de identidade, BeyondTrust, Tenable, ManageEngine, VMware NSX e FortiGate, além das soluções Illumio/Guardicore.

### 5.4 Backup e Disaster Recovery

Arquitetura Veeam com SOBR, Capacity Tier, Google Cloud Storage Coldline e replicação de máquinas virtuais do Site B para o GCVE.

A estratégia também contemplou testes periódicos de restauração, validação funcional e exercícios de recuperação de desastres.

### 5.5 Automação e Infrastructure as Code

Uso de Terraform, Ansible e Packer para provisionamento, configuração e padronização de infraestrutura.

As ferramentas foram integradas a pipelines corporativos no Azure DevOps para execução automatizada de atividades de infraestrutura.

### 5.6 Governança Operacional

Estruturação de processos de monitoramento, gestão de incidentes, mudanças, documentação técnica e planejamento de capacidade.

### 5.7 Continuidade de Negócios

Definição de estratégias de recuperação, classificação de criticidade, RPO, RTO e testes periódicos de restauração e recuperação.

### 5.8 Monitoramento e Gestão de Serviços

Integração de alertas com ITSM e Microsoft Teams, abertura automática de incidentes, classificação de severidade e escalonamento conforme impacto.

## 6. Documentação Técnica do Projeto

A documentação está organizada por domínio técnico para facilitar a navegação e demonstrar as decisões e práticas utilizadas durante a transformação.

| Área | Documentação |
|---|---|
| Arquitetura | [Architecture](architecture/) |
| Visão executiva | [Architecture Overview](architecture-overview/) |
| Decisões técnicas | [Architecture Decisions](architecture-decisions/) |
| Governança | [Governance](governance/) |
| Segurança | [Security](security/) |
| Rede e conectividade | [Network](network/) |
| Backup e recuperação | [Backup](backup/) |
| Automação | [Automation](automation/) |
| Procedimentos operacionais | [Operational Runbooks](operational-runbooks/) |
| Troubleshooting e estudos de caso | [Troubleshooting](troubleshooting/) |
| Diagramas | [Diagrams](diagrams/) |
| Documentação complementar | [Docs](docs/) |

## 7. Liderança e Responsabilidades no Projeto

A iniciativa envolveu atividades de arquitetura, planejamento, execução técnica e governança de infraestrutura.

Entre as principais responsabilidades estão:

- Planejamento e evolução da arquitetura de infraestrutura.
- Coordenação técnica da modernização dos ambientes.
- Estratégia de migração de workloads para cloud.
- Transformação do Site A em ambiente de infraestrutura de rede.
- Estruturação do GCVE como novo site de hospedagem.
- Modernização da infraestrutura on-premises do Site B.
- Definição de padrões de segurança e conectividade.
- Planejamento de backup, disaster recovery e continuidade de negócios.
- Evolução dos processos de automação e Infrastructure as Code.
- Implementação de controles de governança e gestão de mudanças.
- Acompanhamento de riscos, vulnerabilidades e capacidade.
- Alinhamento das soluções técnicas com as necessidades do negócio.

## 8. Resultados Estratégicos

A transformação estabeleceu uma arquitetura híbrida, combinando um novo ambiente de infraestrutura em cloud com um data center on-premises modernizado e uma infraestrutura física de rede remanescente no Site A.

Principais resultados:

- Migração integral da infraestrutura virtualizada do Site A para GCVE.
- Transformação do Site A em um ambiente dedicado à infraestrutura de rede e conectividade.
- Estabelecimento do GCVE como novo site de hospedagem dos workloads migrados.
- Modernização da plataforma de virtualização e computação do Site B.
- Evolução da arquitetura de conectividade entre os ambientes.
- Fortalecimento dos controles de segurança e segmentação.
- Aprimoramento dos processos de gestão de vulnerabilidades.
- Estruturação de uma estratégia de backup e recuperação com Veeam.
- Replicação de workloads do Site B para GCVE.
- Utilização de armazenamento em cloud para Capacity Tier.
- Evolução da automação de infraestrutura.
- Fortalecimento da governança operacional e da continuidade de negócios.

## 9. Sobre Este Portfólio

Este repositório apresenta uma documentação técnica e arquitetural de uma iniciativa real de modernização de infraestrutura corporativa.

O conteúdo foi estruturado para demonstrar experiência prática em arquitetura de infraestrutura, cloud híbrida, segurança, virtualização, automação, continuidade de negócios e governança de TI.

Informações sensíveis da organização, como endereços IP, nomes de servidores, credenciais, identificadores internos, configurações proprietárias e detalhes confidenciais, foram omitidas.

O objetivo é demonstrar a abordagem técnica, as decisões arquiteturais e a capacidade de conduzir iniciativas de transformação tecnológica em ambientes corporativos complexos.
