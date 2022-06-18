# C3 : Normalização

## Conversão do Modelo EA para Modelo Relacional

### Passo 1: Entidades e Atributos

Cliente (<ins>nic</ins>, telefone, email, cartaconducao, primeironome, ultimonome)

Alugar (<ins>código</ins>, datainicial, datafinal, custo, caução)

Filial (<ins>numero</ins>, localização(código postal, localidade, rua, porta)

Funcionário (<ins>nic</ins>, endereço, dn, sexo, primeironome, ultimonome, salário)

TipoVeiculo(<ins>Código</ins>, nome, valorHora)

Departamento (<ins>código</ins>,código postal, localidade, rua, porta)

Veiculo (<ins>matricula</ins>, marca, modelo, stock)

Serviço (<ins>idserviço</ins>, valor, ndias)

### Passo 2: Associações 1:1
Não existe ligações 1:1

#### Passo 3: Associações 1:N

Cliente (<ins>nic</ins>, telefone, email, cartaconducao, primeironome, ultimonome)

Alugar (<ins>código</ins>, datainicial, datafinal, custo, caução, #nic->Cliente, #idserviço->serviço, #matricula->veiculo, #numero->Filial)

Filial (<ins>numero</ins>, rua, porta, localidade, #códigopostal->CódigoPostais)

Funcionário (<ins>nic</ins>, endereço, dn, sexo, primeironome, ultimonome, salário, #Código->Departamento, #numero->Filial)

TipoVeiculo(<ins>Código</ins>, nome, valorHora)

Departamento (<ins>código</ins>, rua, porta, localidade, #CódigoPostal->CódigoPostais)

Veiculo (<ins>matricula</ins>, #modelo->Modelos, #Código->TipoDeVeiculo)

Serviço (<ins>idserviço</ins>, valor, ndias)

CódigoPostais (<ins>CódigoPostal</ins>, localidade)

Modelos (<ins>modelo</ins>, marca)

### Passo 4: Associações N:M

Não existem ligações N:M

### Passo 5: Atributo Multivalor

Não existe Atributos Multivalor

### Passo 6: Associação ternária

Não existe associações ternárias

### Passo 7: Entidades Fracas

Não existe Entidades Fracas


## Relações

|Cliente|    |      |   |         |                   |
|-----------|----|------|---|---------|-------------------|
|<ins>nic</ins>      |PrimeiroNome|UltimoNome|CartaCondução|telefone|Email|

|Alugar    |            |        |        |        |         |         |     |       |
|-------------|------------|------|-----|-----|----|-----|---------|---------|
|<ins>Código</ins>|DataInicial|DataFinal|Custo|Caução|#nic->Cliente|#idserviço->serviço|#matricula->veiculo|#numero->Filial|

|Filial    |    |                 |                    |        |
|---------|----|-----------------|--------------------|-----------|
|<ins>numero</ins>|rua|#_códigopostal->CódigoPostais|porta|localidade|

|TipoVeiculo   |       |          |      
|----------|-------|----------|
|<ins>Código</ins>|nome|ValorHora|

|Funcionário  |         |          |         |                        |           |       |
|---------|---------|----------|---------|------------------------|-----------|--------|
|<ins>nic</ins>|endereço|dn|sexo|PrimeiroNome|UltimoNome|Salário|#Código->Departamento|#numero->Filial|

|Departamento|    |         |         |         |
|----------|----|---------|---------|----------|
|<ins>código</ins>      |rua|porta|#Códigopostal->CódigoPostais|localidade|


|Veiculo|    |           |        |
|-------|----|-----------|--------|
|<ins>matricula</ins>|stock|#modelo->Modelos|#Código->TipoDeVeiculo|

|Serviço    |        |       |  
|------------|--------|-------|
|<ins>idserviço</ins>|valor|ndias|


|CódigoPostais         |                        |
|-------------------|------------------------|
|<ins>CódigoPostal</ins>|Localidade|

|Modelos                |                 |        
|----------------------|-----------------|
|<ins>Modelo</ins>|marca|


## Normalização do Esquema Relacional

## 1ºForma Normal 1ºParte (Compostos - atributos)

Cliente (_nic, telefone, email, cartaconducao, PrimeiroNome, UltimoNome)

Alugar (_código, datainicial, datafinal, custo, caução, #nic->Cliente, #idserviço->serviço, #matricula->veiculo, #numero->Filial)

Filial (_numero,código postal, localidade, rua, porta)

Funcionário (_nic, endereço, dn, sexo, PrimeiroNome, UltimoNome, salário, #Código->Departamento, #numero->Filial)

TipoVeiculo(_Código, nome, valorHora)

Departamento (_código,código postal, localidade, rua, porta)

Veiculo (_matricula, marca, modelo, stock, #Código->TipoDeVeiculo)

Serviço (_idserviço, valor, ndias)

## 1ºForma Normal 2ºParte (atributos multivalor)

Não existem alterações 

## 2ºForma Normal

Já está, pois não existem ligações M:N

## 3ºForma Normal 

Cliente (_nic, telefone, email, cartaconducao, PrimeiroNome, UltimoNome)

Alugar (_código, datainicial, datafinal, custo, caução, #nic->Cliente, #idserviço->serviço, #matricula->veiculo, #numero->Filial)

Filial (_numero,#código postal->CódigoPostais, rua, porta)

Funcionário (_nic, endereço, dn, sexo, PrimeiroNome, UltimoNome, salário, #Código->Departamento, #numero->Filial)

TipoVeiculo(_Código, nome, valorHora)

Departamento (_código,#código postal->CódigoPostais, rua, porta)

Veiculo (_matricula, #modelo->Modelos, stock, #Código->TipoDeVeiculo)

Serviço (_idserviço, valor, ndias)

CódigoPostais (_CódigoPostal, localidade)

Modelos (_Modelo, marca)

## Forma Normal de Boyce-Codd 

Cliente (_nic, telefone, email, cartaconducao, PrimeiroNome, UltimoNome)

Alugar (_código, datainicial, datafinal, custo, caução, #nic->Cliente, #idserviço->serviço, #matricula->veiculo, #numero->Filial)

Filial (_numero,#código postal->CódigoPostais, rua, porta)

Funcionário (_nic, endereço, dn, sexo, PrimeiroNome, UltimoNome, salário, #Código->Departamento, #numero->Filial)

TipoVeiculo(_Código, nome, valorHora)

Departamento (_código,#código postal->CódigoPostais, rua, porta)

Veiculo (_matricula, #modelo->Modelos, stock, #Código->TipoDeVeiculo)

Serviço (_idserviço, valor, ndias)

CódigoPostais (_CódigoPostal, localidade)

Modelos (_Modelo, marca)

## 4ºForma Normal 

Não eixste alterações

---
[< Previous](rebd02.md) | [^ Main](https://github.com/exemploTrabalho/reportSIBD/) | [Next >](rebd04.md)
:--- | :---: | ---: 
