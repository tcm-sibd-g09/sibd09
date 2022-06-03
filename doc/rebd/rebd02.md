# C2 : Esquema conceptual

## Modelo E/A
Entidades:

DEPARTAMENTO 

FILIAL (_número,localização (cidade, rua))

ALUGAR (_Código, Caução, Custo, DataFinal, DataInicial)

VEICULO

SERVIÇO

TIPOVEICULO (Código, Nome)

FUNCIONÁRIO (Nome (Primeiro e Ultimo), _número CC, endereço, salário, sexo, data de nascimento)

CLIENTE (Nome (Primeiro e Ultimo), número do CC, carta de condução, email, nº de telefone)


Associações:

Levantar (ALUGAR, FILIAL) N:1 

Trabalha (FILIAL, FUNCIONÁRIO) 1:N

Entregar (ALUGAR, FILIAL) N:1

Estacionado (VEICULO, FILIAL) N:1

Escolha (VEICULO, TIPOVEICULO) N:1

TipoDeServiço(ALUGAR, SERVIÇO)

TrabalhaEm (DEPARTAMENTO, FUNCIONÁRIO) 1:N

DIAGRAMA 

 ![Diagrama1](https://user-images.githubusercontent.com/96230913/171955084-6d0b55c6-be83-45d4-86d6-e53636172a87.png)




## Regras de negócio adicionais (Restrições)
1- Falta de stock de veiculos
2- Falta de profissionais para efetuar o transporte do serviço

---
[< Previous](rebd01.md) | [^ Main](https://github.com/exemploTrabalho/reportSIBD/) | [Next >](rebd03.md)
:--- | :---: | ---: 
