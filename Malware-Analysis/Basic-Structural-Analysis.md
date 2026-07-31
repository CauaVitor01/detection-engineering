# Laboratorio de Analise Estatica de Malware

> **Nota de Documentacao:** Este arquivo Markdown apresenta um resumo executivo da analise estatica. Para a investigacao completa, incluindo resolucoes de desafios praticos, checklists e capturas de tela (prints) evidenciando o uso de ferramentas como PEstudio e Capa, consulte o arquivo PDF (`Basic_Structural_Analysis.pdf`) disponivel neste repositorio.

---

## 1. Visao Geral do Projeto

Este repositorio contem o registro tecnico e as descobertas realizadas durante o modulo de Analise Estatica Basica. O foco principal consistiu na investigacao de binarios compilados para Windows (arquivos PE - Portable Executable) sem a execucao das amostras, utilizando ambientes estritamente isolados e ferramentas forenses especializadas.

---

## 2. Ferramentas Utilizadas

A triagem e a analise estatica foram suportadas pelo seguinte conjunto de ferramentas e tecnicas:

* **Ambientes de Analise:** FLARE VM (Windows) e REMnux (Linux).
* **Extracao de Dados e Strings:** `strings.exe` e `FLOSS` (FireEye Labs Obfuscated String Solver).
* **Assinaturas e Hashing:** SHA-256 (Identidade unica), `Imphash` (Mapeamento de Família via Imports) e `ssdeep` (Fuzzy Hashing para analise de similaridade).
* **Analise Estrutural:** `PEstudio` (Inspecao profunda de cabecalhos, secoes, DLLs importadas e APIs).
* **Taticas e Tecnicas (CTI):** `Capa` da Mandiant (Mapeamento automatizado para a matriz MITRE ATT&CK e Malware Behavior Catalog).

---

## 3. Descobertas Principais

Durante os exercicios praticos, foram analisadas 6 amostras distintas de malware, resultando nos seguintes mapeamentos tecnicos:

* **Evasao de Defesas:** Identificacao de tecnicas Anti-VM e Evasao de Sandbox (a Amostra 4 apresentou 86 correspondencias diretas de evasao).
* **Ofuscacao:** Recuperacao com sucesso de strings ocultas e ofuscadas nos binarios, como o executavel `DbgView.exe`, utilizando a ferramenta FLOSS.
* **Conexoes de Rede (C2):** Identificacao de bibliotecas criticas importadas, como `rpcrt4.dll` e `wininet.dll`, evidenciando capacidades de comunicacao remota e acesso a internet.
* **Analise de Similaridade:** Aplicacao de fuzzy hashing (`ssdeep`) para confirmar 93% de similaridade estrutural entre diferentes amostras pertencentes a uma mesma familia de malware.

---

## 4. Aviso de Seguranca

Todas as analises documentadas foram realizadas de forma estatica em um ambiente rigorosamente controlado, utilizando snapshots de Maquinas Virtuais (VMs) para garantir o isolamento total da rede e a integridade do hardware host.
