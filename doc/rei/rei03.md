# C3 : Esquema conceptual

## Modelo E/A

### Entidades:

CLIENTE (nic, telefone, email, cartaconducao, nome (primeiro, ultimo))

ALUGAR (código, datainicial, datafinal, custo, caução)

FILIAL (numero, localização(código postal, localidade, rua, porta)

FUNCIONÁRIO (nic, endereço, dn, sexo, nome(primerio, ultimo), salário)

TIPOVEICULO(Código, nome, valorHora)

DEPARTAMENTO (código, Localização(código postal, localidade, rua, porta))

VEICULO (matricula, marca, modelo)

SERVIÇO (idserviço, valor, ndias)


### Associações:

Levantar (ALUGAR, FILIAL) N:1 P/P

Trabalha (FILIAL, FUNCIONÁRIO) 1:N P/T

Entregar (ALUGAR, FILIAL) N:1 P/P

Estacionado (VEICULO, FILIAL) N:1 P/T

Escolha (VEICULO, TIPOVEICULO) N:1 T/P

TipoDeServiço(SERVIÇO, ALUGAR) 1:N P/P

TrabalhaEm(FUNCIONÁRIO, DEPARTAMENTO) N:1

Pode(cliente, alugar) 1:N

TipoVeículo(veiculo, alugar)1:N 





### DIAGRAMA 

![InstantCar](https://user-images.githubusercontent.com/96230913/174440125-1e7a643a-90ba-4ca7-9ff5-08d8f7098bee.png)




## Regras de negócio adicionais (Restrições)
1- Falta de stock de veiculos
2- Falta de profissionais para efetuar o transporte do serviço

---
[< Previous](rei02.md) | [^ Main](https://github.com/exemploTrabalho/reportSIBD/) | Next >
:--- | :---: | ---: 
