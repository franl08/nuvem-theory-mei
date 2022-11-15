# Teórica 08

## Armazenamento

### Funcionalidades

#### Disponibilidade de Dados

- **RAID**: *Redundant Array of Inexpensive Drives*;
- Replicação;
- *Erasure-Codes*.
  - Pega no ficheiro e parte em *k* blocos e *x* blocos de paridade.
    - Ocupa o espaço do ficheiro + $\frac{1}{2}$ do tamanho do ficheiro;
    - Tolera mais falhas que a replicação.

#### Otimizações de *Performance*

- **Localidade de Dados**
  - Tenta garantir que os dados estão o mais próximo possível dos nós que os estão a processar;
  - O armazenamento e o processamento encontram-se no mesmo dispositivo/servidor;
  - **Exemplos**: *HBase* e *HDFS*, *active storage*.

- ***Caching***
  - Mantém os dados num armazenamento mais rápido, tipicamente em RAM;
  - Mantém os dados perto do cliente e/ou acessíveis a partir de uma origem rápida;
  - Evita a espera pela escrita/leitura de dados do armazenamento local/remoto;
  - **Exemplos**: *file system page cache*, *Alluxio*.

#### Eficiência de Espaço

- **Compressão**
  - Reduz o conteúdo redundante entre e nos ficheiros;
  - Encontra conteúdo redundante num ficheiro ou conjunto de ficheiros e comprime-o;
  - Geralmente, é estático, no entanto, até quando é um processo dinâmico é mais lento que a deduplicação.

- **Deduplicação**
  - Elimina as cópias redundantes num sistema de armazenamento;
  - Processo dinâmico.

#### Segurança

- **Encriptação de Dados**
  - *Encryption at rest*:
    - Os dados são encriptados antes de serem guardados de forma persistente;
    - Os dados são encriptados quando chegam ao disco.
  - *Encryption in transit*:
    - Encripta os dados "no caminho" até ao disco.

- **Controlo de Acesso**
  - Evita o acesso não autorizado de utilizadores aos dados.

### Soluções de Armazenamento Complexas e Monolíticas

- Para resolver um pedido é preciso passar por muitos componentes.
  - É difícil de dar *tracking*;
  - É difícil de otimizar.
- A combinação ideal de funcionalidades de armazenamento depende dos requisitos de cada aplicação:
  - Tamanho dos ficheiros;
  - Padrões de acesso ao armazenamento;
  - ...

### *Software-Defined Storage*

- Segue os príncipios das *Software-Defined Networks* (SDN);
- Separa o processo em 2 planos:
  - **Plano de Dados**;
    - Pedacinhos de *middleware* entre os diversos pontos. Apenas sabem otimizar o *I/O*, mas não querem saber do trabalho dos outros pontos.
  - **Plano de Controlo**.
    - Cérebro do armazenamento. Controla a infraestrutura de armazenamento e tem em atenção a sua estrutura, o que permite que tome decisões acerca do que cada *stage* (do plano de dados) deverá fazer.