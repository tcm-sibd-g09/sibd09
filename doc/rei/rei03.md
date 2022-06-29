# C3 : Esquema conceptual

## Modelo E/A

### Entidades:

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


### Associações:

TrabalhaEm(Funcionário, Departamento) N:1 T/P

TrabalhaPara(Funcionário, Filial) N:1 T/P

Vai(Cliente, Alugar) 1:N P/T

EstaEstacionado(Veiculo, Filial) N:1 P/T

Apoiado(Filial, Departamento) N:1 T/T

VaiSer(Serviço, Alugar) 1:N P/P






### DIAGRAMA 

 ![Diagrama1](https://user-images.githubusercontent.com/InstantCar.png)




## Regras de negócio adicionais (Restrições)
1- Falta de stock de veiculos
2- Falta de profissionais para efetuar o transporte do serviço

---
[< Previous](rei02.md) | [^ Main](https://github.com/exemploTrabalho/reportSIBD/) | Next >
:--- | :---: | ---: 
