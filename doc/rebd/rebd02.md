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

TipoDeServiço(SERVIÇO, ALUGAR) 1:N P/P

TrabalhaEm(FUNCIONÁRIO,DEPARTAMENTO) N:1 

Pode(cliente,alugar) 1:N

TipoVeículo(veiculo,alguar)1:N


### DIAGRAMA 


![InstantCar](https://user-images.githubusercontent.com/96230913/174440125-1e7a643a-90ba-4ca7-9ff5-08d8f7098bee.png)





## Regras de negócio adicionais (Restrições)
1- Falta de stock de veiculos
2- Falta de profissionais para efetuar o transporte do serviço

---
[< Previous](rebd01.md) | [^ Main](https://github.com/exemploTrabalho/reportSIBD/) | [Next >](rebd03.md)
:--- | :---: | ---: 
