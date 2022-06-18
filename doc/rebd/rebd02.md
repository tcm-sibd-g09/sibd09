# C2 : Esquema conceptual

## Modelo E/A
Entidades:

CLIENTE (<ins>nic</ins>, telefone, email, cartaconducao, nome (primeiro, ultimo))

ALUGAR (<ins>código</ins>, datainicial, datafinal, custo, caução)

FILIAL (<ins>numero</ins>, localização(código postal, localidade, rua, porta)

FUNCIONÁRIO (<ins>nic</ins>, endereço, dn, sexo, nome(primerio, ultimo), salário)

TIPOVEICULO(<ins>Código</ins>, nome, valorHora)

DEPARTAMENTO (<ins>código</ins>, Localização(código postal, localidade, rua, porta))

VEICULO (<ins>matricula</ins>, marca, modelo)

SERVIÇO (<ins>idserviço</ins>, valor, ndias)

Associações:

Levantar (ALUGAR, FILIAL) N:1 P/P

Trabalha (FILIAL, FUNCIONÁRIO) 1:N P/T

Entregar (ALUGAR, FILIAL) N:1 P/P

Estacionado (VEICULO, FILIAL) N:1 P/T

Escolha (VEICULO, TIPOVEICULO) N:1 T/P

TipoDeServiço(ALUGAR, SERVIÇO) 1:1 P/P

TrabalhaEm (DEPARTAMENTO, FUNCIONÁRIO) 1:N P/T

DIAGRAMA 


![InstantCar](https://user-images.githubusercontent.com/96230913/171990586-d2a8e846-5ca0-48f8-aa52-f9a130ccedce.png)




## Regras de negócio adicionais (Restrições)
1- Falta de stock de veiculos
2- Falta de profissionais para efetuar o transporte do serviço

---
[< Previous](rebd01.md) | [^ Main](https://github.com/exemploTrabalho/reportSIBD/) | [Next >](rebd03.md)
:--- | :---: | ---: 
