# Threat Hunting: Final Stage Investigation (TA0009, TA0010, TA0040)

Este repositório apresenta a investigação forense das etapas conclusivas da **Unified Kill Chain**. O foco está na detecção de ações críticas realizadas pelo adversário após a consolidação do acesso, visando a coleta, o roubo de dados e a interrupção do sistema.

> 📁 **[CLIQUE AQUI PARA ACESSAR O RELATÓRIO DE TÁTICAS FINAIS (PDF)](./Forensic_Report_Final_Objectives.pdf)**
>
> *Este documento contém as evidências técnicas, logs do PowerShell Operational e correlações de eventos que comprovam a exfiltração e o impacto final no ambiente.*

---

## Escopo da Investigação (Ações sobre Objetivos)

O relatório detalha como a telemetria do **Sysmon** e o **Script Block Logging** foram utilizados para identificar comportamentos anômalos que burlam defesas tradicionais:

### Coleta (TA0009)
* **Cenário:** Identificação de um **Keylogger** persistente injetado via PowerShell (`chrome-update_api.ps1`).
* **Descoberta:** Captura de credenciais PII (e-mail: `hunted-victim2323@gmail.com`) através do monitoramento de APIs de ganchos de teclado (Hooks).

### Exfiltração (TA0010)
* **Cenário:** Roubo de arquivos sensíveis via **Tunelamento ICMP**.
* **Descoberta:** Fragmentação do arquivo `icmpdata.ps1` em 21 pacotes de eco ICMP destinados ao servidor C2 externo (`10.10.161.211`), demonstrando evasão de firewall.

### Impacto (TA0040)
* **Cenário:** Destruição de backups para inviabilizar a recuperação de desastres.
* **Descoberta:** Uso de ferramentas nativas (*Living off the Land*) como `vssadmin.exe` para deleção de Shadow Copies, disparado pelo processo pai `powershell.exe` (PID `3732`).

---

## Metodologia de Detecção
* **Análise Proativa:** Foco na redução do **Dwell Time** através da busca por padrões de execução "in-memory".
* **Lógica de Busca:** Criação de consultas **KQL** baseadas em assinaturas de ferramentas de ataque e chamadas de sistema (Win32 APIs).
* **Mapeamento:** Alinhamento total com as táticas finais do framework **MITRE ATT&CK**.

---

## Analista Responsável
* **Nome:** Cauã
* **Data:** 13 de Março de 2026
* **Área:** Engenharia de Detecção / Forense Digital
