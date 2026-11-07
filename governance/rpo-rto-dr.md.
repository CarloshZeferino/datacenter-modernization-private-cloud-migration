
# RPO, RTO e Disaster Recovery

## 1. Visão Geral

A estratégia de continuidade de negócio e recuperação de desastres foi estruturada para proteger os ambientes de infraestrutura dos Sites A e B.

A solução utilizou Veeam Backup & Replication v12 como plataforma de proteção de dados, com repositórios distribuídos entre armazenamento local e Google Cloud Storage.

O objetivo foi estabelecer critérios de recuperação, minimizar impactos operacionais e garantir a capacidade de restauração dos serviços de infraestrutura.

## 2. Recovery Point Objective (RPO)

O RPO representa o intervalo máximo de perda de dados aceitável após um incidente.

Os objetivos de recuperação devem considerar:

- Criticidade dos serviços.
- Frequência dos backups.
- Janela de execução dos jobs.
- Retenção dos pontos de restauração.
- Necessidades das áreas de negócio.

**RPO definido:** A documentar conforme os objetivos estabelecidos para cada serviço.

## 3. Recovery Time Objective (RTO)

O RTO representa o tempo máximo esperado para recuperação de um serviço após uma interrupção.

Os critérios considerados incluem:

- Disponibilidade dos backups.
- Tempo de localização dos pontos de restauração.
- Capacidade de processamento da infraestrutura.
- Tempo de recuperação das máquinas virtuais.
- Validação técnica e funcional dos serviços.

**RTO definido:** A documentar conforme os objetivos estabelecidos para cada serviço.

## 4. Disaster Recovery Strategy

A estratégia de Disaster Recovery foi apoiada pela arquitetura de backup Veeam v12, contemplando:

- Proteção dos ambientes Site A e Site B.
- Veeam Backup Server centralizado no Site A.
- Veeam Backup Proxy no Site B.
- Repositórios de backup locais e em nuvem.
- SOBR com Capacity Tier.
- Google Cloud Storage Coldline para armazenamento de backups.

## 5. Recovery Procedures

Os procedimentos de recuperação contemplaram:

1. Identificação do incidente.
2. Avaliação do impacto sobre os serviços.
3. Identificação dos pontos de restauração disponíveis.
4. Seleção do backup adequado.
5. Execução do processo de restore.
6. Validação da integridade da máquina virtual.
7. Validação dos serviços com as áreas responsáveis.
8. Registro das evidências e resultados.

## 6. Recovery Testing

Foram realizados testes de restauração de infraestrutura com procedimentos documentados passo a passo.

As atividades incluíram:

- Execução de testes de restore.
- Registro das evidências dos procedimentos.
- Gravação das etapas de recuperação.
- Validação técnica dos ambientes restaurados.
- Validação dos resultados com as áreas de negócio.

## 7. Governance and Continuous Improvement

Os processos de recuperação devem ser revisados periodicamente, considerando alterações na infraestrutura, criticidade dos serviços e necessidades do negócio.

Os resultados dos testes devem servir como base para identificar oportunidades de melhoria nos procedimentos de recuperação.

## 8. Conclusion

The implementation of recovery objectives, backup protection and restore testing established an operational foundation for infrastructure resilience and business continuity across both sites.

---

**Note:** RPO and RTO targets must be documented using the actual business-approved values. Recovery test results must be distinguished from target objectives.
