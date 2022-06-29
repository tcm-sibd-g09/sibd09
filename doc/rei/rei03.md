# C3 : Esquema conceptual

## Modelo E/A

# Entidades:

Departamento(codigo, rua, porta, codigoPostal)

Funcionário(nic, primeroNome, ultimoNome, endereco, dataNascimento, salario, sexo, codigoDepartamento, codigoFilial)

Alugar (codigo, dataInicial, dataFinal, custo, caucao, nicCliente, idServicoAluguer, matriculaVeiculo, codigoFilial)

Serviço (idServico, valor, nDias)

Cliente(nic, primeiroNome, ultimoNome, cartaConducao, telefone, email, codigoPostal)

codigoPostais(codigoPostal, localidade)

Filial(numero, rua, porta, codigoPostalFilial, codigoDepartamento)

Modelos(modelo, marca)

tipoVeiculo(codigo, nome, valorHora)

Veiculos( matricula, modelo, codigo)


# Associações:

Pertence(Funcionário, Departamento) N:1

TrabalhaNuma(Funcionário, Filial) N:1

Vai(Cliente, Alugar) 1:N

EstaEstacionado(Veiculo, Filial) N:1

Tem(Departamento, Filial) 1:N

VaiSer(Serviço, Alugar) 1:N

VaoSer(Veiculos, Alugar) 






### DIAGRAMA 

 ![Diagrama1](https://user-images.githubusercontent.com/96230913/171955084-6d0b55c6-be83-45d4-86d6-e53636172a87.png)




## Regras de negócio adicionais (Restrições)
1- Falta de stock de veiculos
2- Falta de profissionais para efetuar o transporte do serviço

---
[< Previous](rei02.md) | [^ Main](https://github.com/exemploTrabalho/reportSIBD/) | Next >
:--- | :---: | ---: 
