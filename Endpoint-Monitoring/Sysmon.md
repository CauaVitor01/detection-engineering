Aqui está o arquivo **Markdown** final e integrado para o seu repositório no GitHub, consolidando a teoria da engenharia de detecção com as evidências técnicas extraídas do arquivo **_Sysmon.pdf**.

---

# 🛡️ Windows Sysmon: Engenharia de Detecção e Investigação Forense

Este repositório apresenta uma documentação técnica detalhada sobre o uso do **Windows Sysmon** para monitoramento avançado, caça a ameaças (*Threat Hunting*) e resposta a incidentes.

## No repositório a um arquivo com atividades,imagens e explicação do Sysmon
> 
> 

---

## 1. Matriz de Eventos Críticos (Telemetria)

O Sysmon amplia a visibilidade do sistema operacional através de IDs de eventos específicos:

* 
**ID 1 (Process Creation):** Detecção de execuções suspeitas e anomalias em linhas de comando.


* 
**ID 3 (Network Connection):** Rastreamento de *beacons* de Comando e Controle (C2) e movimentação lateral.


* 
**ID 10 (Process Access):** Monitoramento de acesso à memória do `lsass.exe` (técnica de *dumping* de credenciais).


* 
**ID 11 (File Create):** Identificação de artefatos de Ransomware e *Droppers*.


* 
**ID 12/13/14 (Registry Event):** Captura de persistência via chaves de registro e modificações de segurança.


* 
**ID 22 (DNS Query):** Investigação de exfiltração de dados e resolução de domínios maliciosos.



---

## 2. Metodologia de Hunting via CLI

A busca por ameaças foi realizada utilizando consultas **XPath** granulares no PowerShell para isolar artefatos de alta fidelidade:

Hunting de Frameworks (Metasploit/C2) 

Foco em portas de conexão reversa não convencionais:

```powershell
Get-WinEvent -Path ".\Hunting_Metasploit.evtx" -FilterXPath '*/System/EventID=3 and */EventData/Data[@Name="DestinationPort"]=4444'

```



Detecção de Mimikatz (Acesso ao LSASS) 

Identificação de processos não autorizados tentando ler a memória do processo de autoridade de segurança local:

```powershell
Get-WinEvent -Path ".\Hunting_Mimikatz.evtx" -FilterXPath '*/System/EventID=10 and */EventData/Data[@Name="TargetImage"]="C:\Windows\system32\lsass.exe"'

```



---

## 3. Relatório de Investigações Reais

Dados extraídos dos cenários práticos documentados no relatório forense.

Investigação 1: Infecção via USB 

* 
**Cenário:** Identificação de infecção originada por hardware externo.


* 
**Chave de Registro do Dispositivo:** `HKLM/System/CurrentControlSet/Enum/WpdBusEnumRoot/UMB/2&37c186b&0&STORAGE#VOLUME#_??_USBSTOR#DISK&VEN_SANDISK&PROD_U3_CRUZER_MICRO&REV_8.01#4054910EF19005B3&0#\FriendlyName`.


* 
**Identificação via RawAccessRead:** `\Device\HarddiskVolume3`.


* 
**Primeiro Executável disparado:** `rundll.32.exe`.



Investigação 2: Mascaramento HTML e C2 

* 
**Cenário:** Execução de *payload* disfarçado para evasão de antivírus e estabelecimento de conexão reversa.


* 
**Percurso da Carga Útil (Payload):** `C:\Users\IEUser\AppData\Local\Microsoft\Windows\Temporary Internet Files\Content.IE5\S97WTYG7\update.hta`.


* 
**Arquivo de Mascaramento:** `C:\Users\IEUser\Downloads\update.html`.


* 
**Binário Assinado (LotL):** `C:\Windows\System32\mshta.exe`.


* **Indicadores de Rede (C2):** IP `10.0.2.18` | Porta `4443`.



Investigação 3: Persistência (Registro e Agendamento) 

* **Infraestrutura C2:** IP Adversário `172.30.1.253` | Host Afetado `DESKTOP-0153T4R` | Servidor `empirec2`.


* 
**Persistência em Registro:** Payload armazenado em `HKLM\SOFTWARE\Microsoft\Network\debug`.


* 
**Comando PowerShell de Inicialização:** Utilização de execução oculta e codificada (`-enc`) para carregar o payload do registro.


* 
**Persistência via Tarefa:** Uso de `c:\users\q\AppData:blah.txt` e acesso suspeito ao `lsass.exe`.



Investigação 4: Infraestrutura de Botnet 

* 
**Vetor de Ataque:** IP `172.30.1.253` operando na porta `80`.


* 
**Framework C2 Identificado:** **Empire**.



---

## Conclusão

A investigação demonstrou que o monitoramento granular de processos, rede e registro através do Sysmon é capaz de reconstruir a linha do tempo de ataques complexos, identificando técnicas de **Living-off-the-Land (LotL)** e persistência que burlariam assinaturas tradicionais.

---

**Analista Responsável:** Cauã **Data da Conclusão:** 11 de Março de 2026 



**Deseja que eu ajude com a organização das pastas no seu repositório para o PDF e o Markdown?**
