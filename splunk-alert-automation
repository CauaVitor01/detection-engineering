# Automação de Monitoramento e Resposta a Incidentes (Splunk)

## Objetivo
Elevar a performance operacional do SOC por meio da automatização de análises recorrentes. Este projeto foca na redução do tempo de resposta a incidentes (MTTR) através da criação de relatórios agendados e alertas proativos no Splunk Enterprise.

## Arquitetura do Cenário
O laboratório foi estruturado utilizando o Splunk Enterprise para centralização e análise de logs, com agentes Universal Forwarder coletando dados de infraestrutura crítica (VPN).

---

## Tecnologias e Ferramentas
* **SIEM:** Splunk Enterprise
* **Linguagem de Consulta:** SPL (Search Processing Language)
* **Fontes de Dados:** Logs de Servidor VPN (`vpn_server`)
* **Recursos:** Relatórios Agendados, Dashboards, Alertas

---

## Metodologia de Implementação

### 1. Automação de Relatórios Agendados
Implementação de rotinas automatizadas para rastreamento de acessos VPN, garantindo padronização na análise de logs entre diferentes turnos.

**Consulta SPL de Referência:**
```splunk
host=vpn_server | stats count by Username
2. Dashboards de Monitoramento (SOC)
Desenvolvimento de visualizações focadas em comportamento anômalo e volume de eventos, facilitando a identificação rápida de anomalias.

Visualização: Gráfico de Colunas (Column Chart) para análise de volume.

UI: Tema Escuro (Dark Theme) para melhor ergonomia visual em SOCs.

3. Alertas Proativos
Configuração de alertas em tempo real para detecção de potenciais ataques de força bruta, com envio de notificações automáticas via e-mail para a equipe de resposta.

Condição: Número de resultados > 5.

Ação: Suprimir alertas repetitivos por 60 minutos (Throttling).

Conclusão
A implementação automatizada resultou na otimização do tempo dos analistas, permitindo foco em investigações de alta complexidade em vez de tarefas repetitivas.

Documentação Técnica
O relatório detalhado contendo a análise técnica e instruções de configuração pode ser encontrado aqui:
[Clique para ler o relatório (PDF)](Automatização de Monitoramento de Segurança no Splunk via Relatórios Agendados.pdf)
