# Detection Engineering & Endpoint Defense (Windows)

Este repositório documenta a implementação, testes e análise de soluções de **Endpoint Detection and Response (EDR)**, com foco no agente **Aurora** e na telemetria nativa do **Event Tracing for Windows (ETW)**. O objetivo é demonstrar a capacidade de transformar telemetria bruta em detecções resilientes baseadas em comportamento.

---

## Sumário Técnico

1. [Arquitetura EDR](https://www.google.com/search?q=%231-arquitetura-edr)
2. [Fundamentos de Visibilidade: ETW](https://www.google.com/search?q=%232-fundamentos-de-visibilidade-etw)
3. [Implementação Aurora Agent (Sigma-Based)](https://www.google.com/search?q=%233-implementa%C3%A7%C3%A3o-aurora-agent-sigma-based)
4. [Validação e Testes de Campo](https://www.google.com/search?q=%234-valida%C3%A7%C3%A3o-e-testes-de-campo)
5. [Análise de Lacunas e Mitigação](https://www.google.com/search?q=%235-an%C3%A1lise-de-lacunas-e-mitiga%C3%A7%C3%A3o)

---

## 1. Arquitetura EDR

A solução de EDR (Endpoint Detection and Response) é o pilar de defesa proativa. Diferente de defesas perimetrais, o EDR foca no monitoramento contínuo do host:

* **Pilares:** Monitoramento, Análise de Padrões, Resposta Automatizada e Investigação Forense.
* **Diferencial:** Redução do *Dwell Time* (tempo de permanência do atacante) através de respostas automáticas como isolamento de rede e encerramento de processos.

---

## 2. Fundamentos de Visibilidade: ETW

O **Event Tracing for Windows (ETW)** é a fonte primária de telemetria utilizada.

* **Estrutura:** Controladores (gerenciam sessões), Provedores (geram logs) e Consumidores (analisam dados).
* **Event Viewer:** Interface para validação humana de logs categorizados em Segurança, Sistema e Aplicativo.

---

## 3. Implementação Aurora Agent (Sigma-Based)

O **Aurora** atua como um EDR "Lean", aplicando regras **Sigma** em tempo real sobre o fluxo ETW sem a sobrecarga de um driver de kernel complexo.

### 3.1. Aurora vs. Sysmon

| Característica | Aurora | Sysmon |
| --- | --- | --- |
| **Fonte** | ETW (User/Kernel) | Driver de Kernel |
| **Respostas** | Kill, Suspend, Dump | Apenas Log |
| **Volume** | Baixo (Alertas) | Alto (Telemetria) |

### 3.2. Orquestração de Respostas

* **Predefinidas:** Ações imediatas como `Kill` (encerrar processo) e `Suspend`.
* **Customizadas:** Automação via `cmd.exe` para contenção personalizada (ex: backup de arquivos em tempo real).

---

## 4. Validação e Testes de Campo

Testes baseados no framework **MITRE ATT&CK** para validar a eficácia das regras Sigma:

* **T1087 (Discovery):** Execução de `whoami /priv` detectada como regra de nível **Alto**.
* **T1071 (C2):** Simulação de *DNS Beaconing* detectada como regra de nível **Crítico**.

---

## 5. Análise de Lacunas e Mitigação

Nenhuma ferramenta é infalível. Identificamos e mitigamos os seguintes "pontos cegos":

| Área de Risco | Desafio | Estratégia de Solução |
| --- | --- | --- |
| **Named Pipes** | ETW ruidoso/limitado | Aurora (Modo Intenso) + Sysmon |
| **Registry** | Identificadores complexos | Aurora (Modo Intenso) + Sysmon |
| **ETW Tampering** | Desativação por atacantes | Módulo **Canary** + `--report-stats` |

---

## Conclusão

Este projeto demonstra que a robustez do SOC moderno depende da combinação de telemetria profunda (ETW), padronização de detecção (Sigma) e estratégias de mitigação para as limitações inerentes ao sistema operacional.

---

**Autor:** Cauã

**Especialidade:** SOC | Detection Engineering | DFIR

