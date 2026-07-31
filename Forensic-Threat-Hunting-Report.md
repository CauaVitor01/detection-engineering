# SOC Lab: Investigação e Engenharia de Detecção

Este repositório documenta uma investigação forense completa focada em **Threat Hunting** e análise de telemetria. O objetivo foi identificar e mapear as etapas de um ataque simulado em ambiente Windows, utilizando o framework **MITRE ATT&CK**.

> 📁 **[CLIQUE AQUI PARA ACESSAR O RELATÓRIO COMPLETO (PDF)](./Forensic_Threat_Hunting_Report.pdf)**
>
> **Nota:** Por motivos de organização, todas as **evidências visuais (screenshots)**, correlação de logs e as respostas detalhadas das atividades práticas estão consolidadas no arquivo PDF acima.

---

## Resumo das Táticas Investigadas

A investigação percorreu o ciclo de vida do ataque, documentando as seguintes táticas:

### 1. Descoberta (Discovery)
* **Atividade:** Reconhecimento de rede, usuários e Active Directory.
* **Indicadores:** Uso de `SharpHound.exe`, comandos de enumeração e varredura de portas via `n.exe`.

### 2. Escalada de Privilégios (Privilege Escalation)
* **Atividade:** Abuso de tokens de impersonação e configurações de serviço.
* **Indicadores:** Exploração de `SeImpersonatePrivilege` (**PrintSpoofer**) e sequestro de binários de serviço via Registro.

### 3. Acesso por Credenciais (Credential Access)
* **Atividade:** Roubo de segredos em memória e replicação de diretório.
* **Indicadores:** Dumping de memória do **LSASS** e ataque **DCSync** via conta privilegiada.

### 4. Movimentação Lateral (Lateral Movement)
* **Atividade:** Transição entre sistemas utilizando ferramentas administrativas e hashes.
* **Indicadores:** Execução remota via **WMI (Impacket)** e autenticação **Pass-the-Hash (PtH)**.

---

## 🛠️ Tecnologias Utilizadas
* **SIEM & Logs:** Elastic Stack (Kibana), Sysmon, Packetbeat.
* **Queries:** KQL (Kibana Query Language) e XPath.
* **Framework:** MITRE ATT&CK.

---
**Analista Responsável:** Cauã
**Data:** 12 de Março de 2026
