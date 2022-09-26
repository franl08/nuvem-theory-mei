# Teórica 02

## Aplicações Distribuídas

### Porquê usá-las?

- Modularidade;
- Desempenho;
- Disponibilidade/Resiliência.

### Sistemas Monolíticos

Múltiplos serviços para múltiplos alvos, mas tudo a correr numa única máquina... Ou seja, tipos de sistemas não distribuídos.

**Desvantagens:**

- Ponto de falha único;
- Carga não é distribuída, o que provoca um ponto de contenção;
- Os serviços não são isolados.

Tipicamente, queremos ter estas 3 garantias nos nossos serviços:

#### Replicação

- Múltiplas cópias dos mesmos dados e funcionalidades;
- Providencia resiliência e, no caso de permitir que um cliente se conecte a outro servidor, poder de escala.

#### Particionamento

No caso de particionar apenas os dados, podemos dar-lhe o nome de *sharding*.

- O servidor é divido horizontalmente (*sharding*);
- Oferece poder de escalabilidade;
- Pode ser aplicado a computação, dados, etc...

#### Arquitetura Orientada aos Serviços (SOA)

Cada componente da aplicação deve correr num servidor diferente.

- Divide o servidor de forma vertical;
- Providencia escalabilidade e modularidade;
- Isto pode causar problemas na decomposição de serviços:
  - *Quão micro deve ser?*;
- Tem um *deploy* complexo.

#### Nota:

- **Escala Vertical**: Para escalar, podemos aumentar os recursos do *server*;
- **Escala Horizontal**: Para escalar, podemos aumentar o número de servidores.

### Arquiteturas Distribuídas

Veja-se uns exemplos de arquiteturas distribuídas:

- *Client-server*;
- Servidor *proxy*;
- *Master-server*;
- *Server group*;
- *Multi-tier*;
- *Bus*.

#### *Client-server*

- As funcionalidades e os dados encontram-se no servidor;
- O cliente tem uma interface e fala com o servidor através de um protocolo num *stub*;
  - Um *stub* é um pacote de *middleware* presente no lado do cliente.
- **Desvantagens**:
  - Ponto único de falha;
  - Gargalo na escalabilidade.

#### *Proxy Server*

- Adiciona-se um *proxy* entre o cliente e múltiplos *servers*;
- Do lado do cliente é como se existisse um único servidor que é o *proxy*;
- **Vantagens**:
  - Permite o balanceamento do trabalho (maior escala e maior disponibilidade);
- **Desvantagens**:
  - Ponto único de falha;
    - Não possui qualquer estado e tem um trabalho mais levve, o que provoca uma menor probabilidade de falha.
  - Tem um número máximo de conexões simultâneas.

#### *Master Server*

Também conhecido por *Master-Slave*.

- Cliente entra em contacto com o *master* para saber onde se encontra o recurso pretendido;
- Após saber onde é que o recurso pretendido se encontra, entra em contacto diretamente com o servidor.
- **Vantagens**:
  - Menos informação no ponto único de falha.
- **Desvantagens**:
  - Ponto único de falha.

#### *Server Group*

- Todos os *servers* podem responder a pedidos;
- Tem uma coordenação difícil;
- **Vantagens**:
  - Muito resiliente.
- **Desvantagens**:
  - Muito pesado (o que provoca um baixo número de clientes) devido à lógica de balanceamento.

#### *Bus*

- Lógica de barramento;
- Participantes produzem e consomem informação para o *bus*;
- Um nó pode ser servidor **e** cliente;
- Os participantes devem ter um protocolo comum entre si;
- **Vantagens**:
  - Altamente flexível.

#### *Multi-tier*

- Cada servidor atua como um cliente do nível inferior (ao estilo do modelo OSI);
- Permite o *deploy* independente e o escalonamento de diferentes funcionalidades;
- Cada camada tem um *stub* e protocolo para comunicar com a camada inferior;
- **Vantagens**:
  - Grande modularidade.
- **Desvantagens**:
  - Muitos pontos únicos de falha.

**ATENÇÃO**:

De forma a termos a melhor solução possível, podemos combinar diversas arquiteturas.

#### Estados em *multi-tier*

- Não há estados nas camadas superiores (p.e. *web server*);
- Estados transientes/em cache nas camadas do meio;
- Estados persistentes nas últimas camadas.
  - **Quanto mais para baixo se vai na pilha, mais complexa fica a replicação.**