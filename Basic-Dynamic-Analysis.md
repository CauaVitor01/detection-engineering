# Relatório de Análise Dinâmica de Malware 

## 1. Escopo e Ambiente (Sandboxing)
A análise foi conduzida em um ambiente isolado para garantir a segurança da infraestrutura.
* **Isolamento:** Rede configurada em modo *Host-Only*.
* **Integridade:** Uso de Snapshots para garantir um estado limpo antes de cada execução.

---

## 2. Monitoramento de Atividade (ProcMon)
Utilizamos o **Process Monitor** para observar a interação da amostra `1.exe` com o sistema em tempo real.

* **Conexão de Rede:** Tentativa de comunicação com o host `94-73-155-12.cizgi.net.tr:2448`.
* **Operação:** Evento de `TCP Reconnect` detectado.
* **Processo:** O executável iniciou a partir do caminho `C:\Users\Administrator\Desktop\samples\1.exe`.

---

## 3. Registro de Chamadas de API (API Monitor)
Através do monitoramento de APIs, identificamos as seguintes ações:

* **Manipulação de Arquivos:** Criação do arquivo `C:\myapp.exe` (Técnica de Masquerading).
* **Conectividade:** Uso da API `InternetConnectW` para tráfego de rede.
* **Técnica de Evasão:** Detecção da chamada `Sleep`, usada para atrasar a execução e evitar detecção por sandboxes automáticas.

---

## 4. Inspeção de Memória e Processos (Process Explorer)
O **Process Explorer** foi fundamental para validar técnicas de ocultação:

| Técnica | Detecção | Resultado |
| :--- | :--- | :--- |
| **Masquerading** | Verificação de Assinatura (Verify) | **N** (Sem assinatura válida da Microsoft) |
| **Process Hollowing** | Comparação de Strings (Image vs Memory) | **N** (Conteúdo da RAM diverge do disco) |
| **Persistência** | Mutex de Controle | `\Sessions\X\BaseNamedObjects\SMX:XXXX:XXX:WilStaging_XX` |

---

## 5. Modificações de Sistema (Regshot)
O uso do **Regshot** confirmou alterações permanentes que sobrevivem à reinicialização:
* **Anti-Análise:** Eficaz contra malwares que detectam processos de monitoramento ativos.
* **Achados:** Criação de chaves de registro para execução automática e persistência no sistema.

---

## 6. Conclusão
A amostra analisada demonstra ser um **Trojan** com capacidades de injeção de código (**Process Hollowing**). O artefato tenta se passar por um processo legítimo da Microsoft para iludir o usuário e o administrador do sistema, estabelecendo persistência através do registro do Windows.
