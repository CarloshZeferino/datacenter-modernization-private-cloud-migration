# Decisões de Arquitetura e Resultados Técnicos

## Visão Geral

Este documento registra as principais decisões arquiteturais tomadas durante as iniciativas de modernização da infraestrutura, migração para cloud privada, recuperação de desastres, conectividade, segurança e automação.

O objetivo é apresentar o contexto técnico de cada decisão, documentar sua implementação e descrever suas implicações arquiteturais.

Os registros estão limitados às decisões e aos resultados confirmados no projeto. Melhorias quantitativas de desempenho, economias financeiras e outras métricas não são incluídas quando não existem números validados disponíveis.

---

## ADR-001 — Migração do Site A para Google Cloud VMware Engine (GCVE)

**Status:** Implementado

### Contexto

O Site A possuía uma infraestrutura baseada em VMware, selecionada para migração para o Google Cloud VMware Engine (GCVE).

A migração exigia a transferência da infraestrutura virtualizada, preservando a disponibilidade das aplicações, a integração de rede e a continuidade operacional.

### Decisão

Migrar toda a infraestrutura VMware do Site A para o GCVE, utilizando uma combinação de:

- VMware Export/Import.
- Recursos de migração do RackWare.
- Estratégia de migração Lift-and-Shift.
- Correção de vulnerabilidades dos sistemas operacionais.
- Atualização e migração de aplicações para versões mais recentes, quando necessário.
- VMware NSX para microsegmentação das cargas de trabalho.

### Implementação

A migração foi realizada como parte da iniciativa mais ampla de modernização da infraestrutura.

A arquitetura resultante transferiu a infraestrutura virtualizada para o GCVE, mantendo apenas a infraestrutura de rede de Camadas 2 e 3 no site físico original.

### Resultado Arquitetural

- Toda a infraestrutura virtualizada do Site A foi migrada para o GCVE.
- O site original manteve sua infraestrutura de rede L2/L3.
- O VMware NSX foi utilizado para microsegmentação das cargas de trabalho.
- As atividades de correção de sistemas operacionais e aplicações foram incorporadas à iniciativa de migração.

---

## ADR-002 — Manutenção do Site B como Ambiente VMware On-Premises

**Status:** Implementado

### Contexto

O Site B precisava manter uma infraestrutura VMware local, capaz de suportar suas cargas de trabalho e permanecer integrada à arquitetura corporativa e à estratégia de recuperação de desastres.

### Decisão

Manter o Site B como um ambiente VMware on-premises, utilizando uma arquitetura dedicada de processamento e armazenamento.

### Implementação

A arquitetura incluiu:

- VMware vCenter.
- Cluster de quatro nós de processamento e memória.
- VMware HA e DRS.
- Storage block Dell PowerVault ME5224.
- Conectividade iSCSI entre processamento e armazenamento.
- Cabeamento Direct Attach Copper (DAC).
- Infraestrutura de switching Dell PowerSwitch S5224F-ON.
- Firewalls FortiGate para segmentação de rede, VLANs e roteamento Layer 3.

### Resultado Arquitetural

O Site B permaneceu como um ambiente VMware on-premises, com recursos dedicados de processamento e armazenamento em bloco.

A arquitetura manteve a execução local das cargas de trabalho e permitiu sua integração com o ambiente de recuperação de desastres hospedado no GCVE.

---

## ADR-003 — Disaster Recovery do Site B por Replicação Veeam para GCVE

**Status:** Implementado

### Contexto

O Site B precisava de uma estratégia de recuperação de desastres capaz de permitir a recuperação das cargas de trabalho fora do ambiente on-premises principal.

### Decisão

Utilizar o Veeam Backup & Replication v12 para replicar as máquinas virtuais do Site B para o Google Cloud VMware Engine.

### Implementação

A arquitetura de disaster recovery utilizou:

- Veeam Backup & Replication v12.
- Processos de replicação Veeam.
- GCVE como destino de recuperação.
- Recursos de infraestrutura VMware no ambiente de recuperação.

A validação da estratégia incluiu exercícios periódicos de restauração e recuperação, além de uma simulação anual de indisponibilidade total do Site B.

Os objetivos de recuperação eram definidos de acordo com a criticidade das cargas de trabalho, utilizando as classificações Tier 0, Tier 1, Tier 2 e Tier 3.

### Resultado Arquitetural

- As cargas de trabalho do Site B passaram a contar com um caminho de recuperação por replicação para o GCVE.
- A arquitetura disponibilizou um ambiente alternativo de recuperação fora do site principal.
- Os procedimentos de recuperação foram validados periodicamente por meio de exercícios controlados.

---

## ADR-004 — Veeam Scale-Out Backup Repository com Google Cloud Storage Coldline

**Status:** Implementado

### Contexto

A arquitetura de backup precisava de uma estratégia para gerenciamento da capacidade de armazenamento e utilização de object storage em cloud como uma camada adicional.

### Decisão

Implementar um Veeam Scale-Out Backup Repository (SOBR), utilizando Capacity Tier para movimentar os dados de backup para o Google Cloud Storage Coldline.

### Implementação

A arquitetura incorporou:

- Veeam Backup & Replication v12.
- Scale-Out Backup Repository.
- Capacity Tier.
- Google Cloud Storage Coldline.
- Repositórios locais de backup nos sites da infraestrutura.

### Resultado Arquitetural

A arquitetura de backup passou a combinar repositórios locais com armazenamento de objetos em cloud.

O Capacity Tier permitiu a movimentação dos dados de backup para o Google Cloud Storage Coldline como parte da estratégia de armazenamento.

---

## ADR-005 — Arquitetura de Segmentação de Rede Específica por Site

**Status:** Implementado

### Contexto

Os dois sites possuíam arquiteturas de infraestrutura diferentes e precisavam de mecanismos de segmentação de rede alinhados aos respectivos ambientes.

### Decisão

Utilizar VMware NSX para microsegmentação das cargas de trabalho no Site A e segmentação baseada em FortiGate no Site B.

### Implementação

**Site A**

- VMware NSX para microsegmentação das cargas de trabalho.
- FortiGate para segurança de perímetro e conectividade de rede.
- Infraestrutura de rede L2/L3 mantida no site físico original após a migração para GCVE.

**Site B**

- Segmentação de rede baseada em FortiGate.
- Separação por VLANs.
- Roteamento Layer 3 realizado pelo FortiGate.

### Resultado Arquitetural

Cada site implementou uma arquitetura de segmentação alinhada ao seu modelo de infraestrutura.

O Site A utilizou microsegmentação nativa do VMware, enquanto o Site B utilizou segmentação e roteamento baseados em firewall.

---

## ADR-006 — Conectividade Redundante com Google Cloud por Equinix Partner Interconnect

**Status:** Implementado

### Contexto

O ambiente corporativo precisava de conectividade resiliente entre a infraestrutura on-premises e o Google Cloud.

### Decisão

Utilizar o Equinix Enterprise Connectivity para estabelecer conectividade com o Google Cloud Partner Interconnect, com circuitos redundantes e roteamento BGP.

### Implementação

A arquitetura de conectividade incluiu:

- Equinix como parceiro de conectividade.
- Google Cloud Partner Interconnect.
- Dois circuitos independentes.
- Circuitos em localidades físicas distintas.
- Equipamentos e caminhos de rede redundantes.
- Roteamento BGP.
- Firewalls FortiGate em ambos os sites.

A conectividade com a Internet e com o Google Cloud foi integrada por meio da infraestrutura de firewall dos dois sites.

### Resultado Arquitetural

A arquitetura disponibilizou caminhos redundantes de conectividade entre a infraestrutura corporativa e o Google Cloud.

A diversidade física dos circuitos e o roteamento BGP foram incorporados ao projeto para suportar a resiliência da rede.

---

## ADR-007 — Stack de Automação de Infraestrutura

**Status:** Implementado

### Contexto

As atividades de provisionamento e configuração de infraestrutura precisavam de uma abordagem consistente de automação entre ambientes Google Cloud, VMware e on-premises.

### Decisão

Adotar uma arquitetura de automação baseada em múltiplas ferramentas, utilizando Terraform, Ansible, Packer e Azure DevOps.

### Implementação

As ferramentas foram divididas por responsabilidade:

| Tecnologia | Responsabilidade |
|---|---|
| Terraform | Provisionamento de infraestrutura em GCP, VMware e ambientes on-premises |
| Ansible | Configuração de servidores e instalação de softwares |
| Packer | Criação de imagens de servidores |
| Azure DevOps | Pipelines corporativos de automação |
| PowerShell | Automação de Windows Server e Active Directory |
| Bash | Administração e automação Linux |

Os pipelines do Azure DevOps executavam automaticamente os processos de Terraform, Ansible e Packer.

O GitHub também era utilizado nos projetos de laboratório pessoal.

### Resultado Arquitetural

A stack de automação estabeleceu uma abordagem comum para provisionamento de infraestrutura, configuração de servidores e criação de imagens entre diferentes plataformas.

---

## Consolidação dos Resultados Arquiteturais

As decisões documentadas neste capítulo estabeleceram a seguinte arquitetura:

1. A infraestrutura virtualizada do Site A foi migrada para o GCVE, mantendo apenas a infraestrutura de rede L2/L3 no site original.
2. O Site B permaneceu como ambiente VMware on-premises, com recursos dedicados de processamento e armazenamento.
3. O disaster recovery do Site B foi integrado ao GCVE por meio da replicação Veeam.
4. O armazenamento de backups incorporou Veeam SOBR Capacity Tier e Google Cloud Storage Coldline.
5. A segmentação de rede foi implementada com VMware NSX no Site A e FortiGate no Site B.
6. A conectividade com o Google Cloud utilizou Equinix Partner Interconnect, circuitos redundantes e BGP.
7. A automação da infraestrutura foi implementada com Terraform, Ansible, Packer e Azure DevOps.

## Escopo e Limitações da Documentação

Estes ADRs descrevem decisões arquiteturais confirmadas e sua implementação.

Os seguintes detalhes não foram quantificados intencionalmente, pois não foram fornecidos números validados do projeto:

- Duração da migração e quantidade de cargas de trabalho.
- Redução de custos de infraestrutura.
- Melhorias de desempenho.
- Largura de banda e latência de rede.
- Capacidade de backup e períodos de retenção.
- Valores medidos de RPO e RTO.
- Percentuais de disponibilidade.

Esses registros poderão ser ampliados com métricas validadas e evidências de projeto à medida que estiverem disponíveis.
