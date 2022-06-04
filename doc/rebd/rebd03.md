# C3 : Normalização

## Conversão do Modelo EA para Modelo Relacional

### Passo 1: Entidades e Atributos

Cliente (_nic, telefone, email, cartaconducao, nome (primeiro, ultimo)

Alugar (_código, datainicial, datafinal, custo, caução)

Filial (_numero, localização(código postal, localidade, rua, porta)

Funcionário (_nic, endereço, dn, sexo, nome(primerio, ultimo), salário)

TipoVeiculo(_Código, nome, valorHora)

Departamento (_código, Localização(código postal, localidade, rua, porta))

Veiculo (_matricula, marca, modelo, stock)

Serviço (_idserviço, valor, ndias)

### Passo 2: Associações 1:1
Não existe ligações 1:1

#### Passo 3: Associações 1:N

Cliente (_nic, telefone, email, cartaconducao, nome (primeiro, ultimo))

Alugar (_código, datainicial, datafinal, custo, caução, #nic->Cliente, #idserviço->serviço, #matricula->veiculo, #numero->Filial)

Filial (_numero, localização(rua, cidade))

Funcionário (_nic, endereço, dn, sexo, nome(primerio, ultimo), salário, #Código->Departamento, #numero->Filial)

TipoVeiculo(_Código, nome, valorHora)

Departamento (_código, Localização)

Veiculo (_matricula, marca, modelo, stock, #Código->TipoDeVeiculo)

Serviço (_idserviço, valor, ndias)


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
|_nic      |PrimeiroNome|UltimoNome|CartaCondução|telefone|Email|

|Alugar    |            |        |        |        |         |         |     |       |
|-------------|------------|------|-----|-----|----|-----|---------|---------|
|_Código|DataInicial|DataFinal|Custo|Caução|#nic->Cliente|#idserviço->serviço|#matricula->veiculo|#numero->Filial

|Filial    |    |                 |                    |
|---------|----|-----------------|--------------------|
|_numero|rua|#_códigopostal->CódigoPostais|porta|

|TipoVeiculo   |       |          |      
|----------|-------|----------|
|_Código|nome|ValorHora|

|Funcionário  |         |          |         |                        |           |       |
|---------|---------|----------|---------|------------------------|-----------|--------|
|_nic|endereço|dn|sexo|PrimeiroNome|UltimoNome|Salário|#Código->Departamento|#numero->Filial

|Departamento|    |         |         |
|----------|----|---------|---------|
|_código      |rua|porta|#Códigopostal->CódigoPostais|


|Veiculo|    |           |        |
|-------|----|-----------|--------|
|_matricula|stock|#modelo->Modelos|#Código->TipoDeVeiculo|

|Serviço    |        |       |  
|------------|--------|-------|
|_idserviço|valor|ndias|


|CódigoPostais         |                        |
|-------------------|------------------------|
|_CódigoPostal|Localidade|

|Modelos                |                 |        
|----------------------|-----------------|
|_Modelo|marca|


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
