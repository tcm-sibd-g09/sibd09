# C3 : Normalização

## Relações

Cliente (_nic, telefone, email, cartaconducao, nome (primeiro, ultimo)
Alugar (_código, datainicial, datafinal, custo, caução)
Filial (_numero, localização(código postal, localidade, rua, porta)
Funcionário (_nic, endereço, dn, sexo, nome(primerio, ultimo), salário)
TipoVeiculo(_Código, nome, valorHora)
Departamento (_código, Localização(código postal, localidade, rua, porta))
Veiculo (_matricula, marca, modelo, stock)
Serviço (_idserviço, valor, ndias)

### Ligações 1:1

Não existe ligações 1:1

### Ligações 1:N

Cliente (_nic, telefone, email, cartaconducao, nome (primeiro, ultimo))
Alugar (_código, datainicial, datafinal, custo, caução, #nic->Cliente, #idserviço->serviço, #matricula->veiculo, #numero->Filial)
Filial (_numero, localização(rua, cidade))
Funcionário (_nic, endereço, dn, sexo, nome(primerio, ultimo), salário, #Código->Departamento, #numero->Filial)
TipoVeiculo(_Código, nome, valorHora)
Departamento (_código, Localização)
Veiculo (_matricula, marca, modelo, stock, #Código->TipoDeVeiculo)
Serviço (_idserviço, valor, ndias)

### Ligações M:N

Não existe ligações M:N

### 1ºForma Normal 1ºParte (Compostos - atributos)

Cliente (_nic, telefone, email, cartaconducao, PrimeiroNome, UltimoNome)
Alugar (_código, datainicial, datafinal, custo, caução, #nic->Cliente, #idserviço->serviço, #matricula->veiculo, #numero->Filial)
Filial (_numero,código postal, localidade, rua, porta)
Funcionário (_nic, endereço, dn, sexo, PrimeiroNome, UltimoNome, salário, #Código->Departamento, #numero->Filial)
TipoVeiculo(_Código, nome, valorHora)
Departamento (_código,código postal, localidade, rua, porta)
Veiculo (_matricula, marca, modelo, stock, #Código->TipoDeVeiculo)
Serviço (_idserviço, valor, ndias)

### 1ºForma Normal 2ºParte (atributos multivalor)

Não existem alterações 

### 2ºForma Normal

Já está, pois não existem ligações M:N

### 3ºForma Normal 

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

### Forma Normal de Boyce-Codd 

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

### 4ºForma Normal 

Não eixste alterações

## Normalização do Esquema Relacional
_(Apresentar o estudo da normalização das relações obtidas na secção anterior. Desnormalizar se necessário.)_

---
[< Previous](rebd02.md) | [^ Main](https://github.com/exemploTrabalho/reportSIBD/) | [Next >](rebd04.md)
:--- | :---: | ---: 
