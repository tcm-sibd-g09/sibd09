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
| **nic** | Número de cliente (auto-incrementado) | INT | - | Sim | Não |
| **Primeironome** | Nome do cliente | VARCHAR(100) | - | Não | Não |
| **UltimoNome** | Ultimo nome do cliente | VARCHAR(100) | - | Não | Não |
| **CartaCondução** | Numero da carta de condução do cliente | BIGINT | - | Não | Não |
| **Telefone** | Numero de telemóvel do cliente | BIGINT | - | Não | Não |
| **Email**  | Email do email do cliente | VARCHAR(100) | - | Não | Não |
| **CodPostal**| Número do código postal do cliente | INT | - | Não| Não |


## Restrições de Integridade


### Chave primária

| **Coluna(s)** |
| --- |
| **nic** |


### Referencial (chaves estrangeiras)

| **Nome** | **Coluna(s)** | **Tabela referênciada** | **Coluna(s) referênciada(s)** | **Indexar** |
| --- | --- | --- | --- | --- |
| **FK\_clientes\_CodPostais** | numeroCliente | CodPostais | numeroCódigoPostais | Não |

# CódigoPostais

## Descrição

Esta tabela irá guardar informações sobre os CódigosPostais.

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

# Alugar

## Descrição

Esta tabela irá guardar informações sobre alugar.

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

# Departamento

## Descrição

Esta tabela irá guardar informações acerca o departamento.

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

# Filial

## Descrição

Esta tabela irá guardar informações sobre as filial.

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

# Funcionário

## Descrição

Esta tabela irá guardar informações sobre os funcionários.

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

# Modelos

## Descrição

Esta tabela irá guardar informações sobre os modelos.

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

# Serviço

## Descrição

Esta tabela irá guardar informações sobre os serviço.

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

# TipoVeiculo

## Descrição

Esta tabela irá guardar informações sobre os tipos de veiculos.

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

# Veiculos

## Descrição

Esta tabela irá guardar informações sobre os veiculos.

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



### Tabela_a






## Vistas



---
| [< Previous](rebd03.md) | [^ Main](https://github.com/exemploTrabalho/reportSIBD/) | [Next >](rebd05.md) |
| :---------------------- | :------------------------------------------------------: | ------------------: |
