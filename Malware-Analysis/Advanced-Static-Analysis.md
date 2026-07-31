# Advanced Static Analysis: Desconstrução de Malware e Engenharia Reversa

> **Nota de Documentação:** Este arquivo Markdown apresenta um resumo executivo dos conceitos, ferramentas e estudos de caso abordados na análise estática avançada de malware. Para visualizar o mapeamento de fluxo, a descompilação de código e as capturas de tela (prints) da ferramenta Ghidra, consulte o documento em formato PDF correspondente disponível neste repositório.

---

## 1. Introdução à Análise Estática Avançada

A análise avançada foca na desconstrução do código de máquina (Assembly) via desassembladores para entender a lógica interna do malware sem executá-lo. O objetivo principal é mapear o fluxo de controle, identificar APIs utilizadas pelo adversário e vencer técnicas de evasão (Anti-VM/Anti-Debug) implementadas no código.

---

## 2. Ferramentas e Fluxo de Trabalho (Ghidra)

O **Ghidra** (desenvolvido pela NSA) é a ferramenta base utilizada nesta etapa. O seu principal diferencial é o **Descompilador**, que traduz instruções de baixo nível em pseudocódigo C legível, acelerando a triagem.

O fluxo de análise apoia-se nas seguintes janelas e funções:
* **Symbol Tree:** Utilizada para a localização de funções principais de execução, como `entry` ou `main`.
* **Listing:** Visualização direta de Opcodes e instruções em Assembly (ex: `PUSH`, `CALL`).
* **Strings:** Busca ativa por textos em claro, endereços IP e caminhos de arquivos ocultos.

---

## 3. Estruturas de Código no Assembly

Compreender como os compiladores traduzem a lógica de programação para Assembly é essencial para a engenharia reversa.

* **Condicionais (If-Else):** Geralmente identificadas por instruções de comparação (`CMP`) seguidas de saltos lógicos (`JZ`, `JNZ`).
  * *Resultado da Análise (if-else.exe):* A string executada foi `"This program demonstrates if-else construct"`.
* **Loops (While/For):** Identificados por saltos incondicionais ou condicionais que retornam o fluxo de controle a endereços de memória anteriores.
  * *Resultado da Análise (while-loop.exe):* O endereço de memória do `CALL` final identificado foi `00401543`.

---

## 4. Estudo de Caso: Process Hollowing (Benign.exe)

O estudo prático abordou a técnica de *Process Hollowing*, uma tática de injeção onde o malware substitui o código de um processo legítimo alocado na memória pelo seu próprio código malicioso, mascarando sua execução.

* **Processo Alvo:** O malware inicia o binário legítimo `iexplore.exe` em modo suspenso.
* **Chamada de Criação:** Identificou-se o uso da API `CreateProcessA` no endereço virtual `0040108f`.
* **Esvaziamento de Memória:** O espaço do processo legítimo foi limpo utilizando a API `ZwUnmapViewOfSection`.
* **Payload Injetado:** O arquivo malicioso inserido foi localizado no caminho `C:\Users\THM-Attacker\Desktop\Injectors\evil.exe`.
* **Tratamento de Erro:** Caso a injeção do payload falhe, o fluxo do programa desvia automaticamente para o endereço `00401509`.

---

## 5. APIs Windows de Alto Interesse para SOC

A presença de funções específicas nos *Imports* do arquivo PE (Portable Executable) revela as intenções e a categoria da ameaça. A tabela abaixo documenta as APIs críticas mapeadas durante a análise:

| Categoria do Malware | APIs Windows Associadas |
| :--- | :--- |
| **Keylogging** | `SetWindowsHookEx`, `GetAsyncKeyState` |
| **C2 / Downloader** | `URLDownloadToFile`, `InternetOpen`, `HttpSendRequest` |
| **Exfiltração de Dados** | `FtpPutFile`, `InternetReadFile`, `GetClipboardData` |
| **Injeção de Código / Dropper** | `VirtualAllocEx`, `WriteProcessMemory`, `ResumeThread` |
| **Evasão (Anti-Análise)** | `IsDebuggerPresent`, `CheckRemoteDebuggerPresent`, `GetTickCount` |
