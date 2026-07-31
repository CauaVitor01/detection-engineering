# Tactical Detection & Threat Intelligence Engineering

Este repositório documenta a implementação de estratégias avançadas de detecção de ameaças, integrando Inteligência de Ameaças (CTI), padronização via regras Sigma e técnicas de monitoramento proativo para fortalecer a postura de segurança defensiva.

---

## Sumário
1. [Inteligência de Ameaças e Padronização Sigma](#1-inteligência-de-ameaças-e-padronização-sigma)
2. [Resposta a Vulnerabilidades Zero-Day](#2-resposta-a-vulnerabilidades-zero-day)
3. [Estratégias de Deception e Auditoria de Objetos](#3-estratégias-de-deception-e-auditoria-de-objetos)
4. [Especificações Técnicas e Ferramental](#4-especificações-técnicas-e-ferramental)

---

## 1. Inteligência de Ameaças e Padronização Sigma
A detecção eficiente fundamenta-se no mapeamento de Indicadores de Comprometimento (IOCs). Através da análise de infraestrutura e correlação de rede, expandimos o escopo de detecção para abranger a infraestrutura completa do adversário.

### Engenharia de Detecção com Sigma
Para mitigar a dependência de fornecedores específicos (vendor lock-in), as detecções são desenvolvidas utilizando a linguagem Sigma (YAML).
* **Portabilidade:** Assinaturas genéricas conversíveis para Elastic Stack, Splunk e Microsoft Sentinel.
* **Escopo:** Identificação de fluxos de rede suspeitos e downloads de executáveis em domínios de baixa reputação.



---

## 2. Resposta a Vulnerabilidades Zero-Day
Em cenários de exploração de vulnerabilidades críticas (Zero-Day), o tempo de resposta é o principal KPI. Este projeto demonstra a conversão acelerada de inteligência da comunidade em regras acionáveis via Uncoder.io.

### Estudos de Caso Aplicados
* **Follina (MSDT):** Implementação de alertas via ElastAlert e consultas Lucene para monitoramento de argumentos suspeitos no processo `msdt.exe`.
* **Log4j (RCE):** Desenvolvimento de consultas SPL (Splunk) voltadas à detecção de instâncias de shells (bash, powershell) originadas de processos host Java.



---

## 3. Estratégias de Deception e Auditoria de Objetos
Além da detecção baseada em assinaturas, o projeto contempla a implementação de sensores de alta fidelidade através de mecanismos de engodo (Deception) e auditoria de integridade.

### Monitoramento de Ativos Críticos
Configuração de SACLs (System Access Control Lists) em arquivos de alta sensibilidade para gerar alertas de exfiltração de dados.
* **Mecanismo:** Ativação de Políticas de Auditoria de Acesso a Objetos no Windows.
* **Indicador:** Monitoramento do Event ID 4663. Como estes ativos não possuem finalidade comercial, a taxa de falsos positivos é virtualmente nula.



---

## 4. Especificações Técnicas e Ferramental
Abaixo, os componentes técnicos utilizados para a validação das estratégias descritas:

* **SIEM/Análise de Logs:** Elastic Stack (Kibana/Elasticsearch), Splunk Enterprise.
* **Linguagens de Consulta:** Sigma, Lucene, SPL (Search Processing Language).
* **Protocolos de Auditoria:** SACL, Windows Event Forwarding (WEF), CTI Lifecycle.

---
**Analista Responsável:** [Seu Nome]  
**Área de Atuação:** Blue Team | Detection Engineering | Threat Hunting
