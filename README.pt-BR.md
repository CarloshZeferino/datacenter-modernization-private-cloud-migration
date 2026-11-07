# Modernização de Data Centers e Migração para Cloud Privada

**Arquitetura de Infraestrutura | VMware | Google Cloud VMware Engine | Cibersegurança | Governança de TI**

[English](README.md) | [Português](README.pt-BR.md)

---

## Resumo Executivo

Este case apresenta um programa corporativo de transformação de infraestrutura envolvendo dois ambientes críticos de Data Center da organização.

A iniciativa combinou migração para cloud privada, modernização de infraestrutura on-premises, melhorias de cibersegurança, continuidade de negócio e governança de TI.

A transformação endereçou infraestrutura legada, obsolescência da virtualização, falhas de hardware, vulnerabilidades de segurança e ausência de processos estruturados de backup e governança operacional.

### Visão Geral da Transformação

| Ambiente | Estratégia de Transformação | Arquitetura de Destino |
|---|---|---|
| Site A – Matriz | Migração de Data Center | Google Cloud VMware Engine (GCVE) |
| Site B – Segundo Site | Modernização On-Premises | Novo cluster VMware vSphere 8 |

## Principais Tecnologias

- VMware vSphere 8, vCenter, HA e DRS
- Google Cloud VMware Engine (GCVE)
- VMware NSX
- Ferramenta de migração RackWare
- Veeam Backup & Replication v12
- Dell PowerEdge R760
- Dell PowerVault ME5224
- Dell PowerSwitch S5224F-ON
- FortiGate
- Illumio / Guardicore
- Conectividade iSCSI e DAC

## Frentes de Transformação

### 1. Assessment de Infraestrutura
- Inventário e assessment técnico da infraestrutura.
- Identificação de obsolescência de hardware e vulnerabilidades.
- Avaliação do ambiente legado de virtualização.
- Documentação técnica e mapeamento de dependências.

### 2. Migração para Cloud
- Migração do principal Data Center para GCVE.
- VMware Export/Import e RackWare.
- Estratégias de migração Lift and Shift.
- Modernização de sistemas operacionais durante a migração.

### 3. Modernização On-Premises
- Implantação de cluster VMware com quatro nós.
- Arquitetura corporativa Dell de compute e storage.
- Gerenciamento centralizado da virtualização.
- Modernização da conectividade de rede e storage.

### 4. Arquitetura de Segurança
- Microsegmentação VMware NSX na matriz.
- Segmentação de rede com FortiGate e arquitetura baseada em VLANs no segundo site.
- Segmentação de workloads com Illumio / Guardicore.
- Correção de vulnerabilidades de sistemas operacionais e softwares de terceiros.

### 5. Backup, Recuperação e Continuidade de Negócio
- Veeam Backup & Replication v12.
- Definição e validação de RTO e RPO.
- Testes de restore de infraestrutura e aplicações.
- Participação das áreas de negócio nos testes de recuperação.
- Evidências gravadas e documentação passo a passo dos procedimentos.

### 6. Governança e Operações de TI
- Lista mestra de ativos.
- Documentação de infraestrutura.
- Procedimentos operacionais e runbooks técnicos.
- Processos de gestão de patches.
- Preparação operacional e transição para sustentação.

## Liderança do Projeto

Liderança técnica e executiva ao longo de todo o ciclo de transformação, incluindo assessment, desenho de arquitetura, benchmarking tecnológico, elaboração de Business Case, defesa de orçamento perante a diretoria, planejamento e execução das migrações, melhorias de segurança, implantação de governança e transição operacional.

## Documentação do Projeto

| Documentação | Descrição |
|---|---|
| [Visão Executiva](docs/executive-overview.md) | Contexto e objetivos estratégicos |
| Assessment de Infraestrutura | Ambiente legado e riscos identificados |
| Estratégia de Migração | Metodologias e execução das migrações |
| Arquitetura de Destino | Arquitetura dos dois ambientes |
| Arquitetura de Segurança | Segurança de rede e workloads |
| Backup e Disaster Recovery | Backup, RTO, RPO e testes de recuperação |
| Governança e Operações | Gestão de ativos e processos operacionais |

## Resultados Estratégicos

A transformação estabeleceu duas plataformas complementares de infraestrutura, fortalecendo segurança, disponibilidade, capacidade de recuperação, documentação e governança operacional.

---

*Este case descreve uma experiência profissional em ambiente corporativo anonimizado. Informações confidenciais da organização e detalhes sensíveis da infraestrutura foram intencionalmente omitidos.*
