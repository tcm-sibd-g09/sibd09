# C3 : Normalização

## Conversão do Modelo EA para Modelo Relacional

### Passo 1: Entidades e Atributos

CLIENTE (<ins>nic</ins>, telefone, email, cartaconducao, primeironome, ultimonome)

ALUGAR (<ins>código</ins>, datainicial, datafinal, custo, caução)

FILIAL (<ins>numero</ins>, localização(código postal, localidade, rua, porta)

FUNCIONÁRIO (<ins>nic</ins>, endereço, dn, sexo, primeironome, ultimonome, salário)

TIPOVEICULO(<ins>Código</ins>, nome, valorHora)

DEPARTAMENTO (<ins>código</ins>,código postal, localidade, rua, porta)

VEICULO (<ins>matricula</ins>, marca, modelo)

SERVIÇO (<ins>idserviço</ins>, valor, ndias)

### Passo 2: Associações 1:1
Não existe ligações 1:1

### Passo 3: Associações 1:N

CLIENTE (<ins>nic</ins>, telefone, email, cartaconducao, primeironome, ultimonome)

ALUGAR (<ins>código</ins>, datainicial, datafinal, custo, caução, #nic->Cliente, #idserviço->serviço, #matricula->veiculo, #numero->Filial)

FILIAL (<ins>numero</ins>, rua, porta, localidade, #códigopostal->CódigoPostais)

FUNCIONÁRIO (<ins>nic</ins>, endereço, dn, sexo, primeironome, ultimonome, salário, #Código->Departamento, #numero->Filial)

TIPOVEICULO (<ins>Código</ins>, nome, valorHora)

DEPARTAMENTO (<ins>código</ins>, rua, porta, localidade, #CódigoPostal->CódigoPostais)

VEICULO (<ins>matricula</ins>, #modelo->Modelos, #Código->TipoDeVeiculo)

SERVIÇO (<ins>idserviço</ins>, valor, ndias)

CÓDIGOPOSTAIS (<ins>CódigoPostal</ins>, localidade)

MODELOS (<ins>modelo</ins>, marca)

### Passo 4: Associações N:M

Não existe

### Passo 5: Atributo Multivalor

Não existe Atributos Multivalor

### Passo 6: Associação ternária

Não existe associações ternárias

### Passo 7: Entidades Fracas

Não existe Entidades Fracas


## Relações

|CLIENTE|    |      |   |         |                   |
|-----------|----|------|---|---------|-------------------|
|<ins>nic</ins>      |PrimeiroNome|UltimoNome|CartaCondução|telefone|Email|

|ALUGAR    |            |        |        |        |         |         |     |       |
|-------------|------------|------|-----|-----|----|-----|---------|---------|
|<ins>Código</ins>|DataInicial|DataFinal|Custo|Caução|#nic->Cliente|#idserviço->serviço|#matricula->veiculo|#numero->Filial|

|FILIAL    |    |                 |                    |        |
|---------|----|-----------------|--------------------|-----------|
|<ins>numero</ins>|rua|#_códigopostal->CódigoPostais|porta|localidade|

|TIPOVEICULO   |       |          |      
|----------|-------|----------|
|<ins>Código</ins>|nome|ValorHora|

|FUNCIONÁRIO  |         |          |         |                        |           |       |          |           |
|---------|---------|----------|---------|------------------------|-----------|--------|--------|----------|
|<ins>nic</ins>|endereço|dn|sexo|PrimeiroNome|UltimoNome|Salário|#Código->Departamento|#numero->Filial|

|DEPARTAMENTO|    |         |         |         |
|----------|----|---------|---------|----------|
|<ins>código</ins>      |rua|porta|#Códigopostal->CódigoPostais|localidade|


|VEICULO|    |        |
|-------|----|--------|
|<ins>matricula</ins>|#modelo->Modelos|#Código->TipoDeVeiculo|

|SERVIÇO    |        |       |  
|------------|--------|-------|
|<ins>idserviço</ins>|valor|ndias|


|CÓDIGOPOSTAIS         |                        |
|-------------------|------------------------|
|<ins>CódigoPostal</ins>|Localidade|

|MODELOS                |                 |        
|----------------------|-----------------|
|<ins>Modelo</ins>|marca|


## Normalização do Esquema Relacional

### Dependências Funcionais:

nicCliente -> telefone, email, cartaconducao, primeiroNome, ultimoNome

codigoAluguer -> dataInicial,dataFinal, custo, caucao

numero -> codigoPostal, rua, porta

nicFuncionario -> endereco, dn, sexo, PrimeiroNome, UltimoNome, salario

codigoVeiculo -> nome, valorHora

codigoDepartamento -> codigoPostal, localidade, rua, porta

Matricula -> marca, modelo

idServico -> valor, nDias

## 1ºForma Normal 1ºParte (Compostos - atributos)

CLIENTE (<ins>nic</ins>, telefone, email, cartaconducao, PrimeiroNome, UltimoNome)

ALUGAR (<ins>codigo</ins>, dataInicial, dataFinal, custo, caucao, #nic->Cliente, #idserviço->serviço, #matricula->veiculo, #numero->Filial)

FILIAL (<ins>numero</ins>,codigoPostal, localidade, rua, porta)

FUNCIONÁRIO (<ins>nic</ins>, endereco, dn, sexo, PrimeiroNome, UltimoNome, salario, #Código->Departamento, #numero->Filial)

TIPOVEICULO(<ins>Codigo</ins>, nome, valorHora)

DEPARTAMENTO (<ins>codigo</ins>,codigoPostal, localidade, rua, porta)

VEICULO (<ins>matricula</ins>, marca, modelo, #Código->TipoDeVeiculo)

SERVIÇO (<ins>idserviço</ins>, valor, ndias)


## 1ºForma Normal 2ºParte (atributos multivalor)

Não existem alterações 

## 2ºForma Normal

CLIENTE (<ins>nic</ins>, telefone, email, cartaconducao, PrimeiroNome, UltimoNome)

ALUGAR (<ins>código</ins>, datainicial, datafinal, custo, caução, #nic->Cliente, #idserviço->serviço, #matricula->veiculo, #numero->Filial)

FILIAL (<ins>numero</ins>,código postal, localidade, rua, porta)

FUNCIONÁRIO (<ins>nic</ins>, endereço, dn, sexo, PrimeiroNome, UltimoNome, salário, #Código->Departamento, #numero->Filial)

TIPOVEICULO(<ins>Código</ins>, nome, valorHora)

DEPARTAMENTO (<ins>código</ins>,código postal, localidade, rua, porta)

VEICULO (<ins>matricula</ins>, marca, modelo,#Código->TipoDeVeiculo)

SERVIÇO (<ins>idserviço</ins>, valor, ndias)

## 3ºForma Normal 

CLIENTE (<ins>nic</ins>, telefone, email, cartaconducao, PrimeiroNome, UltimoNome)

ALUGAR (<ins>código</ins>, datainicial, datafinal, custo, caução, #nic->Cliente, #idserviço->serviço, #matricula->veiculo, #numero->Filial)

FILIAL (<ins>numero</ins>,#código postal->CódigoPostais, rua, porta)

FUNCIONÁRIO (<ins>nic</ins>, endereço, dn, sexo, PrimeiroNome, UltimoNome, salário, #Código->Departamento, #numero->Filial)

TIPOVEICULO(<ins>Código</ins>, nome, valorHora)

DEPARTAMENTO (<ins>código</ins>,#código postal->CódigoPostais, rua, porta)

VEICULO (<ins>matricula</ins>, #modelo->Modelos,#Código->TipoDeVeiculo)

SERVIÇO (<ins>idserviço</ins>, valor, ndias)

CÓDIGOPOSTAIS (<ins>CódigoPostal</ins>, localidade)

MODELOS (<ins>Modelo</ins>, marca)

## Forma Normal de Boyce-Codd 

Não existem alterações

## 4ºForma Normal 

Não eixste alterações





---
[< Previous](rebd02.md) | [^ Main](https://github.com/exemploTrabalho/reportSIBD/) | [Next >](rebd04.md)
:--- | :---: | ---: 
