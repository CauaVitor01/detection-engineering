# Adversary Emulation with Atomic Red Team

Este repositório contém a documentação técnica e o relatório de evidências do laboratório de **Adversary Emulation** utilizando o framework **Atomic Red Team** e o módulo **Invoke-AtomicRedTeam**.

O objetivo deste projeto foi validar controles de segurança (SIEM/EDR) através da simulação controlada de técnicas do **MITRE ATT&CK**, culminando em um estudo de caso real do grupo de ameaça **APT37 (Reaper)**.

## 📄 Documentação Completa
O relatório detalhado com todos os logs, prints de telemetria e análises de impacto está disponível no arquivo:
 **[atomic_red_team.pdf](./atomic_red_team.pdf)**

---

## Resumo do Projeto

### 1. Operação Técnica
Domínio do módulo `Invoke-AtomicRedTeam` para execução de testes atômicos no Windows:
- **Inspeção:** Uso de `-ShowDetails` para análise de comandos antes da execução.
- **Gestão de Pré-requisitos:** Validação de binários via `-CheckPrereqs`.
- **Higiene Pós-Ataque:** Execução sistemática de `-Cleanup` para remoção de IoCs e manutenção da integridade do host.

### 2. Emulação de Adversários (Intelligence-Led)
Utilização do **MITRE ATT&CK Navigator** para mapear e emular grupos específicos:
- **admin@338:** Foco em técnicas de *Phishing* (T1566.001) e *Discovery* (T1083).
- **APT37 (Reaper):** Estudo de caso completo simulando o ciclo de vida de um ataque de ciberespionagem norte-coreano.

### 3. Validação de Telemetria (Blue Team)
Análise de logs gerados durante os ataques para validar a visibilidade das ferramentas de defesa:
- **Sysmon:** Identificação de eventos de criação de processos (ID 1), modificação de registro (ID 13) e criação de arquivos (ID 11).
- **Aurora EDR:** Monitoramento de alertas baseados em regras **Sigma** para detecção de persistência (Run/RunOnce).

---

## Laboratórios Realizados (Principais Evidências)

| Técnica MITRE | Descrição | Artefato/Evidência |
| :--- | :--- | :--- |
| **T1053.005** | Scheduled Task | Criação da tarefa `spawn`. |
| **T1547.001** | Registry Run Keys | Modificação em `HKLM\...\RunOnceEx`. |
| **T1218.005** | LOLBins (Mshta) | Execução de VBScript via Mshta.exe. |
| **T1106-1** | Native API | Criação do arquivo `T1106.exe` (Sysmon ID 11). |

---

## Customização
O projeto também explorou a criação de testes personalizados através do **Atomic GUI** (`Start-AtomicGui`), permitindo a adaptação de payloads para contornar políticas de senhas locais e simular cenários de infraestrutura específicos.

---

## Referências
- [Atomic Red Team Library](https://github.com/redcanaryco/atomic-red-team)
- [MITRE ATT&CK Framework](https://attack.mitre.org/)
- [Aurora EDR - Sigma Based Detection](https://github.com/NextronSystems/aurora)
