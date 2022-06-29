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

TrabalhaEm(Funcionário, Departamento) N:1 T/P

TrabalhaPara(Funcionário, Filial) N:1 T/P

Vai(Cliente, Alugar) 1:N P/T

EstaEstacionado(Veiculo, Filial) N:1 P/T

Apoiado(Filial, Departamento) N:1 T/T

VaiSer(Serviço, Alugar) 1:N P/P






### DIAGRAMA 

![Diagrama1](https://user-images.githubusercontent.com/96230913/171955084-6d0b55c6-be83-45d4-86d6-e53636172a87.png)




## Regras de negócio adicionais (Restrições)
1- Falta de stock de veiculos
2- Falta de profissionais para efetuar o transporte do serviço

---
[< Previous](rei02.md) | [^ Main](https://github.com/exemploTrabalho/reportSIBD/) | Next >
:--- | :---: | ---: 
