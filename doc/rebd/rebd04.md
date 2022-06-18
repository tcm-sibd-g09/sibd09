# C4 : Esquema Relacional  <!-- omit in toc -->
- [Relações](#relações)
  - [Tabela_a](#tabela_a)
  - [Tabela_b](#tabela_b)
- [Vistas](#vistas)

## Relações
# Clientes

## Descrição

Esta tabela irá guardar informações sobre os clientes.

## Colunas

| **Nome** | **Descrição** | **Domínio** | **por Omissão** | **Automático** | **Nulo** |
| --- | --- | --- | --- | --- | --- |
| **numeroCliente** | Número de cliente (auto-incrementado). | INT | - | Sim | Não |
| **nome** | Nome do cliente. | VARCHAR(45) | - | Não | Não |
| **telemovel** | Telemóvel do cliente. | INT | - |
 | Não |
| **codigoPostal** | Código postal do cliente. | VARCHAR (45) | - | Não | Sim |
| **numeroContribuinte** | Numero de contribuinte da loja que o cliente pertence (FK). | INT | - | Não | Não |

## Restrições de Integridade


### Chave primária

| **Coluna(s)** |
| --- |
| **numeroCliente** |


### Referencial (chaves estrangeiras)

| **Nome** | **Coluna(s)** | **Tabela referênciada** | **Coluna(s) referênciada(s)** | **Indexar** |
| --- | --- | --- | --- | --- |
| **FK\_Loja\_Clientes** | numeroContribuinte | Loja | numeroContribuinte | Não |

# Fornecedores

## Descrição

Esta tabela irá guardar informações sobre os fornecedores.

## Colunas

| **Nome** | **Descrição** | **Domínio** | **por Omissão** | **Automático** | **Nulo** |
| --- | --- | --- | --- | --- | --- |
| **codigoFornecedor** | Código do fornecedor (auto-incrementado). | INT | - | Sim | Não |
| **nome** | Nome do fornecedor. | VARCHAR(45) | - | Não | Não |
| **morada** | Morada do fornecedor. | VARCHAR(45) | - | Não |
| **codigoPostal** | Código postal do fornecedor. | VARCHAR(45) | - | Não | Não |
| **numeroContribuinte** | Numero de contribuinte da loja que fornece produtos (FK). | INT | - | Não | Não |

## Restrições de Integridade


### Chave primária

| **Coluna(s)** |
| --- |
| **codigoFornecedor** |


### Referencial (chaves estrangeiras)

| **Nome** | **Coluna(s)** | **Tabela referênciada** | **Coluna(s) referênciada(s)** | **Indexar** |
| --- | --- | --- | --- | --- |
| **FK\_Loja\_Fornecedores** | numeroContribuinte | Loja | numeroContribuinte | Não |

# Funcionarios

## Descrição

Esta tabela irá guardar informações sobre os funcionários.

## Colunas

| **Nome** | **Descrição** | **Domínio** | **por Omissão** | **Automático** | **Nulo** |
| --- | --- | --- | --- | --- | --- |
| **codigoFuncionario** | Código de funcionário (auto-incrementado). | INT | - | Sim | Não |
| **tipo** | Tipo de funcionário. | VARCHAR(45) | - | Não | Não |
| **nome** | Nome do funcionário. | VARCHAR(45) | - | Não | Não |
| **morada** | Morada do funcionário. | VARCHAR(200) | - | Não | Não |
| **nif** | NIF do funcionário. | INT | - | Não | Não |
| **telemovel** | Telemóvel do funcionário. | VARCHAR(45) | - | Não | Não |
| **Email** | Email do funcionário. | VARCHAR(45) | - | Não | Sim |
| **numeroContribuinte** | Numero de contribuinte da loja que o funcionário trabalha (FK). | INT | - | Não | Não |

## Restrições de Integridade


### Chave primária

| **Coluna(s)** |
| --- |
| **codigoFuncionario** |


### Referêncial (chaves estrangeiras)

| **Nome** | **Coluna(s)** | **Tabela referênciada** | **Coluna(s) referênciada(s)** | **Indexar** |
| --- | --- | --- | --- | --- |
| **FK\_Loja\_Funcionarios** | numeroContribuinte | Loja | numeroContribuinte | Não |

# Loja

## Descrição

Esta tabela irá guardar informações acerca das lojas.

## Colunas

| **Nome** | **Descrição** | **Domínio** | **por Omissão** | **Automático** | **Nulo** |
| --- | --- | --- | --- | --- | --- |
| **numeroContribuinte** | NIF da loja (cada loja terá um NIF diferente). | INT | - | Não | Não |
| **nome** | Nome da loja. | VARCHAR(45) | - | Não | Não |
| **morada** | Morada da loja. | VARCHAR(45) | - | Não | Não |
| **codigoPostal** | Código postal da loja. | VARCHAR(45) | - | Não | Não |
| **Telefone** | Telefone da loja. | INT | - | Não | Não |

## Restrições de Integridade


### Chave primária

| **Coluna(s)** |
| --- |
| **numeroContribuinte** |

# Pedidos

## Descrição

Esta tabela irá guardar informações sobre os pedidos.

## Colunas

| **Nome** | **Descrição** | **Domínio** | **por Omissão** | **Automático** | **Nulo** |
| --- | --- | --- | --- | --- | --- |
| **numeroPedido** | Número do Pedido. | INT | - | Não | Não |
| **codigoFuncionario** | Código do funcionário que efectuou o pedido (FK). | INT | - | Não | Não |

## Restrições de Integridade


### Chave primária

| **Coluna(s)** |
| --- |
| **numeroPedido** |


### Referencial (chaves estrangeiras)

| **Nome** | **Coluna(s)** | **Tabela referênciada** | **Coluna(s) referênciada(s)** | **Indexar** |
| --- | --- | --- | --- | --- |
| **FK\_Funcionarios\_Pedidos** | codigoFuncionario | Funcionarios | codigoFuncionario | Sim |

# Produto

## Descrição

Esta tabela irá guardar informações sobre os produtos.

## Colunas

| **Nome** | **Descrição** | **Domínio** | **por Omissão** | **Automático** | **Nulo** |
| --- | --- | --- | --- | --- | --- |
| **codigoProduto** | Código do produto (auto-incrementado). | INT | - | Sim | Não |
| **stockLoja** | Stock na Loja. | INT | - | Não | Não |
| **stockArmazem** | Stock no armazém. | INT | - | Não | Não |
| **tamanho** | Tamanho do produto. | VARCHAR(45) | - | Não | Sim |
| **numeroContribuinte** | Numero de contribuinte da loja que tem o produto (FK). | INT | - | Não | Não |
| **descricao** | Descrição do produto. | VARCHAR(200) | - | Não | Não |
| **preco** | Preço do produto. | DECIMAL(10,2) | - | Não | Não |

## Restrições de Integridade


### Chave primária

| **Coluna(s)** |
| --- |
| **codigoProduto** |


### Referêncial (chaves estrangeiras)

| **Nome** | **Coluna(s)** | **Tabela referênciada** | **Coluna(s) referênciada(s)** | **Indexar** |
| --- | --- | --- | --- | --- |
| **FK\_Loja\_Produto** | numeroContribuinte | Loja | numeroContribuinte | Sim |

# Reservas

## Descrição

Esta tabela irá guardar informações sobre as reservas.

## Colunas

| **Nome** | **Descrição** | **Domínio** | **por Omissão** | **Automático** | **Nulo** |
| --- | --- | --- | --- | --- | --- |
| **numeroReserva** | Número da reserva (auto-incrementado). | INT | - | Sim | Não |
| **apelido** | Apelido da reserva. | VARCHAR(45) | - | Não | Não |
| **valor** | Valor da reserva. | DECIMAL(10,2) | - | Não | Não |
| **estadoPagamento** | Estado do pagamento da reserva. | VARCHAR(45) | - | Não | Sim |
| **numeroCliente** | Numero de cliente que efectuou a reserva (FK). | INT | - | Não | Não |

## Restrições de Integridade


### Chave primária

| **Coluna(s)** |
| --- |
| **numeroReserva** |


### Referêncial (chaves estrangeiras)

| **Nome** | **Coluna(s)** | **Tabela referênciada** | **Coluna(s) referênciada(s)** | **Indexar** |
| --- | --- | --- | --- | --- |
| **FK\_Clientes\_Reservas** | numeroCliente | Clientes | numeroCliente | Sim |

# Vendas

## Descrição

Esta tabela irá guardar informações sobre as vendas.

## Colunas

| **Nome** | **Descrição** | **Domínio** | **por Omissão** | **Automático** | **Nulo** |
| --- | --- | --- | --- | --- | --- |
| **codigo** | Código da venda (auto-incrementado). | INT | - | Sim | Não |
| **numeroContribuinte** | Numero de contribuinte da loja que vende produtos (FK). | INT | - | Não | Não |

## Restrições de Integridade


### Chave primária

| **Coluna(s)** |
| --- |
| **codigo** |


### Referêncial (chaves estrangeiras)

| **Nome** | **Coluna(s)** | **Tabela referênciada** | **Coluna(s) referênciada(s)** | **Indexar** |
| --- | --- | --- | --- | --- |
| **FK\_Loja\_Vendas** | numeroContribuinte | Loja | numeroContribuinte | Sim |

# Produtoreservas

## Descrição

Tabela para relacionar as entidades Produto e Reservas.

## Colunas

| **Nome** | **Descrição** | **Domínio** | **por Omissão** | **Automático** | **Nulo** |
| --- | --- | --- | --- | --- | --- |
| **codigoProduto** | Código do produto. | INT | - | Não | Não |
| **numeroReserva** | Número da reserva. | INT | - | Não | Não |

## Restrições de Integridade


### Chave primária

| **Coluna(s)** |
| --- |
| **codigoProduto** |
| **numeroReserva** |


### Referêncial (chaves estrangeiras)

| **Nome** | **Coluna(s)** | **Tabela referênciada** | **Coluna(s) referênciada(s)** | **Indexar** |
| --- | --- | --- | --- | --- |
| **FK\_Produto\_Reservas** | codigoProduto | produto | codigoProduto | Sim |
| **FK\_Reservas** | numeroReserva | reservas | numeroReserva | Sim |

# Produtovendas

## Descrição

Tabela para relacionar as entidades Produto e Vendas.

## Colunas

| **Nome** | **Descrição** | **Domínio** | **por Omissão** | **Automático** | **Nulo** |
| --- | --- | --- | --- | --- | --- |
| **codigoProduto** | Código do produto. | INT | - | Não | Não |
| **codigo** | Código da venda. | INT | - | Não | Não |
| **valor** | Valor do produto na venda. | DECIMAL(10,2) | - | Não | Não |

## Restrições de Integridade


### Chave primária

| **Coluna(s)** |
| --- |
| **codigoProduto** |
| **codigo** |


### Referêncial (chaves estrangeiras)

| **Nome** | **Coluna(s)** | **Tabela referênciada** | **Coluna(s) referênciada(s)** | **Indexar** |
| --- | --- | --- | --- | --- |
| **FK\_Produtos** | codigoProduto | produto | codigoProduto | Sim |
| **FK\_Vendas** | codigo | vendas | codigo | Sim |

# Produtopedidos

## Descrição

Tabela para relacionar as entidades Produto e Pedidos.

## Colunas

| **Nome** | **Descrição** | **Domínio** | **por Omissão** | **Automático** | **Nulo** |
| --- | --- | --- | --- | --- | --- |
| **codigoProduto** | Código do produto. | INT | - | Não | Não |
| **numeroPedido** | Número do Pedido. | INT | - | Não | Não |
| **quantidade** | Quantidade do Produto no Pedido. | INT | - | Não | Não |
| **valor** | Valor do Produto no Pedido. | DECIMAL(10,2) | - | Não | Não |

## Restrições de Integridade


### Chave primária

| **Coluna(s)** |
| --- |
| **codigoProduto** |
| **numeroPedido** |


### Referêncial (chaves estrangeiras)

| **Nome** | **Coluna(s)** | **Tabela referênciada** | **Coluna(s) referênciada(s)** | **Indexar** |
| --- | --- | --- | --- | --- |
| **FK\_Pedidos** | numeroPedido | pedidos | numeroPedido | Sim |
| **FK\_Produto** | codigoProduto | produtos | codigoProduto | Sim |



### Tabela_a






## Vistas



---
| [< Previous](rebd03.md) | [^ Main](https://github.com/exemploTrabalho/reportSIBD/) | [Next >](rebd05.md) |
| :---------------------- | :------------------------------------------------------: | ------------------: |
