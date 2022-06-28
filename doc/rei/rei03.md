# C3 : Esquema conceptual

## Modelo E/A

Entidades:

Departamento 

Filial (número, gerente, localização (cidade, rua), nº de empregados)

Serviço aluguer de carros (caução, tipo de veiculo, a marca, o local, o nº de dias, valor a pagar, data inicial e data final)

Serviço de transporte (valor fixo, tipo de veiculo, o tipo de transporte, inicio e fim do serviço, o valor a pagar)

Funcionário (Nome (Primeiro e Ultimo), número CC, endereço, salário, sexo, data de nascimento)

Cliente (Nome (Primeiro e Ultimo), número do CC, carta de condução, email, nº de telefone)


Associações:

Pertence (Funcionário, departamento) N:1

TrabalhaNuma (Funcionário, filial) N:1



Aluga (Cliente, tipo de serviço) 1:1






### DIAGRAMA 

 ![Diagrama1](https://user-images.githubusercontent.com/96230913/171955084-6d0b55c6-be83-45d4-86d6-e53636172a87.png)




NOTA: Cada entidade-tipo e cada associação devem ter um pequeno texto – um ou dois parágrafos – para descrever esse elemento do modelo e os seus atributos)

## Regras de negócio adicionais (Restrições)
1- Falta de stock de veiculos
2- Falta de profissionais para efetuar o transporte do serviço

---
[< Previous](rei02.md) | [^ Main](https://github.com/exemploTrabalho/reportSIBD/) | Next >
:--- | :---: | ---: 
