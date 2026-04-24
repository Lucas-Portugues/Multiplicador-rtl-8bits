# Multiplicador de 8-bits com Arquitetura RTL
**Projeto de Sistemas Digitais | Engenharia de Computação**

Este repositório contém o projeto de um **multiplicador de números inteiros de 8 bits** (com saída de 16 bits) desenvolvido para a disciplina de Sistemas Digitais. A implementação segue rigorosamente a **Metodologia RTL**, dividindo o sistema em um bloco de controle e um bloco operacional.

## Especificações Técnicas
* **Entradas:** Dois números inteiros de 8 bits ($A$ e $B$) e um sinal de controlo `comece`.
* **Saída:** Um produto final de 16 bits.
* **Algoritmo:** Implementação de multiplicação através do algoritmo de somas sucessivas e deslocamentos (*shifts*).

## Metodologia RTL
O hardware foi projetado para traduzir um algoritmo de alto nível diretamente para componentes físicos coordenados:

### 1. Bloco Operacional (Datapath)
Responsável pelo armazenamento e processamento dos dados. Inclui os seguintes componentes:
* **Extensor de Sinal:** Converte a entrada $A$ de 8 bits para 16 bits para garantir a precisão do produto final.
* **Registadores:** Registadores dedicados para o Multiplicando ($Reg A$), Multiplicador ($Reg B$) e Produto final ($Reg Produto$).
* **Bloco de Soma e Deslocamento:** Utiliza um somador de 16 bits e lógica de *shift left* ($<<1$) e *shift right* ($>>1$).
* **Contador e Comparador:** Circuito para controlar as 8 iterações necessárias para completar a multiplicação de 8 bits.

### 2. Bloco de Controle (FSM)
Consiste numa **Máquina de Estados de alto nível** que coordena o fluxo de dados através dos seguintes estados principais:
* **Q0 (IDLE):** Aguarda o sinal `comece = 1` para iniciar a operação.
* **Q1 (INIT):** Estado de carga, onde os valores de $A$ e $B$ são registados e o produto é zerado.
* **Q2 (ADD):** Verifica o bit menos significativo do multiplicador; se for '1', adiciona o multiplicando ao produto.
* **Q3 (SHIFT):** Realiza os deslocamentos dos registadores e incrementa o contador de iterações.
* **Q4 (DONE):** Sinaliza a conclusão da operação e disponibiliza o resultado de 16 bits.

## Estrutura de Arquivos
* `Multiplicador.qpf` / `Multiplicador.qsf`: Ficheiros de projeto e configurações do Quartus.
* `Multiplicador.bdf`: Diagrama principal do sistema (Top-level).
* `*.bdf` / `*.bsf`: Blocos funcionais internos e seus respectivos símbolos (Mux, Somadores, Registadores).
* `TabelaProjetoSD-1.pdf`: Tabela de transição de estados e sinais de controle (LA, RA, LB, RB, etc.).
* `Projeto SD.pdf`: Diagramas RTL originais, incluindo a máquina de estados ASM e o bloco operacional.

---
*Projeto desenvolvido por **Lucas Fernando da Silva Português** como requisito da disciplina de Sistemas Digitais.* **Curso:** Engenharia de Computação  
**Instituição:** Instituto de Computação (IC) - Universidade Federal de Alagoas (UFAL)
