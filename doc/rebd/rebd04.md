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
| **Primeironome** | Primeiro Nome do cliente | VARCHAR(100) | - | Não | Não |
| **UltimoNome** | Ultimo Nome do cliente | VARCHAR(100) | - | Não | Não |
| **CartaCondução** | Numero da carta de condução do cliente | BIGINT | - | Não | Não |
| **Telefone** | Numero de telemóvel do cliente | BIGINT | - | Não | Não |
| **Email**  | Email do email do cliente | VARCHAR(100) | - | Não | Não |



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
| **codigoPostal** | Código postal do fornecedor. | INT | - | Não | Não |
| **localidade** | Nome da localidade | INT | - | Não | Não |

## Restrições de Integridade


### Chave primária

| **Coluna(s)** |
| --- |
| **codigoPostal** |

# Alugar

## Descrição

Esta tabela irá guardar informações sobre alugueres.

## Colunas

| **Nome** | **Descrição** | **Domínio** | **por Omissão** | **Automático** | **Nulo** |
| --- | --- | --- | --- | --- | --- |
| **codigo** | Código do aluguer (auto-incrementado). | INT | - | Sim | Não |
| **dataIncial** | Data inicial do aluguer | Date | - | Não | Não |
| **dataFinal** | Data final do aluguer | Date | - | Não | Não |
| **custo** | Custo do aluguer | numeric (10, 2) | - | Não | Não |
| **caucao** | Caução do aluguer | numeric (10, 2) | - | Não | Não |
| **idCliente** | Identificação do cliente | INT | - | Não | Não |
| **idServiço** | Identificação do serviço | INT | - | Não | Sim |
| **matriculaVeiculo** | Matricula do veiculo do aluguer | Varchar (30) | - | Não | Sim |
| **idFilial** | Identificação de filial | INT | - | Não | Não |


## Restrições de Integridade


### Chave primária

| **Coluna(s)** |
| --- |
| **codigo** |


### Referêncial (chaves estrangeiras)

| **Nome** | **Coluna(s)** | **Tabela referênciada** | **Coluna(s) referênciada(s)** | **Indexar** |
| --- | --- | --- | --- | --- |
| **FK\_alugar\_Funcionarios** | Clientes | Alugar |  | Não |

# Departamento

## Descrição

Esta tabela irá guardar informações acerca do departamento.

## Colunas

| **Nome** | **Descrição** | **Domínio** | **por Omissão** | **Automático** | **Nulo** |
| --- | --- | --- | --- | --- | --- |
| **codigo** | Identificação através de um codigo | INT | - | Sim | Não |
| **codpostal** | Código Postal do departamento | INT | - | Não | Não |
| **rua** | Nome da rua. | VARCHAR(100) | - | Não | Não |
| **porta** | Numero da porta | INT | - | Não | Não |


## Restrições de Integridade


### Chave primária

| **Coluna(s)** |
| --- |
| **codigo** |

# Filial

## Descrição

Esta tabela irá guardar informações sobre as filial.

## Colunas

| **Nome** | **Descrição** | **Domínio** | **por Omissão** | **Automático** | **Nulo** |
| --- | --- | --- | --- | --- | --- |
| **numero** | Número da filial | INT | - | Não | Não |
| **codpostal** | Código Postal da filial | INT | - | Não | Não |
| **rua** | Nome da rua | Varchar (100) | - | Não | Não |
| **porta** | Numero da porta | INT | - | Não | Não |
| **idDepartamento** | Identificação do departamento | INT | - | Não | Não |

## Restrições de Integridade


### Chave primária

| **Coluna(s)** |
| --- |
| **numero** |


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
| **nic** | nic do funcionário | INT | - | Não | Não |
| **email** | email do funcionário | Varchar (100) | - | Não | Não |
| **dataNascimento** | Data de nascimento do funcionário | date | - | Não | Não |
| **Salário** | Salário do funcionário | numeric (10, 2) | - | Não | Não |
| **idFilial** | Identificação do filial | INT | - | Não | Não |
| **primeiroNome** | primeiro nome do funcionário | VARCHAR(100) | - | Não | Não |
| **ultimoNome** | ultimo nome do funcionário | VARCHAR(100) | - | Não | Não |
| **idDepartamento** | Identificação do departamento | INT | - | Não | Não |

## Restrições de Integridade


### Chave primária

| **Coluna(s)** |
| --- |
| **nic** |


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
| **modelo** | modelo do veiculo | VARCHAR(100) | - | Não | Não |
| **marca** | marca do veiculo | VARCHAR(100) | - | Não | Não |

## Restrições de Integridade


### Chave primária

| **Coluna(s)** |
| --- |
| **modelo** |


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
| **idServiço** | Identificação do serviço | INT | - | Sim | Não |
| **valor** | Valor do serviço | Numeric (10, 2) | - | Não | Não |
| **nDias** | Numero de dias do serviço | INT | - | Não | Não |

## Restrições de Integridade


### Chave primária

| **Coluna(s)** |
| --- |
| **idServiço** |


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
| **codigo** | Código do veiculo | INT | - | Não | Não |
| **nome** | Nome do tipo de veiculo | VARCHAR (100) | - | Não | Não |
| **valorHora** | Número do valor que paga à hora | FLOAT | - | Não | Não |

## Restrições de Integridade


### Chave primária

| **Coluna(s)** |
| --- |
| **codigo** |


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
| **matricula** | Matricula do veiculo | VARCHAR (30) | - | Não | Não |
| **modelo** | Modelo do veiculo | VARCHAR (100) | - | Não | Não |
| **idTipoVeiculo** | Identificação do veiculo | INT | - | Não | Não |

## Restrições de Integridade


### Chave primária

| **Coluna(s)** |
| --- |
| **matricula** |



### Referêncial (chaves estrangeiras)

| **Nome** | **Coluna(s)** | **Tabela referênciada** | **Coluna(s) referênciada(s)** | **Indexar** |
| --- | --- | --- | --- | --- |
| **FK\_Produtos** | codigoProduto | produto | codigoProduto | Sim |
| **FK\_Vendas** | codigo | vendas | codigo | Sim |



### Tabela_a

![Tabela](https://user-images.githubusercontent.com/96230913/171996254-6a55cbd7-25bf-4d17-a3ef-de3687815773.png)




## Vistas



---
| [< Previous](rebd03.md) | [^ Main](https://github.com/exemploTrabalho/reportSIBD/) | [Next >](rebd05.md) |
| :---------------------- | :------------------------------------------------------: | ------------------: |
