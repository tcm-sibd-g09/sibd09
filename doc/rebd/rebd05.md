# C3 : SQL

## DDL

CREATE SCHEMA IF NOT EXISTS `sibd09` DEFAULT CHARACTER SET utf8mb4 COLLATE utf8mb4_0900_ai_ci ;
USE `sibd09` ;

-- -----------------------------------------------------
-- Table `sibd09`.`codigopostais`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `sibd09`.`codigopostais` (
  `codigoPostal` INT NOT NULL,
  `localidade` VARCHAR(100) NOT NULL,
  PRIMARY KEY (`codigoPostal`))
ENGINE = InnoDB
DEFAULT CHARACTER SET = utf8mb4
COLLATE = utf8mb4_0900_ai_ci;


-- -----------------------------------------------------
-- Table `sibd09`.`filial`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `sibd09`.`filial` (
  `numero` INT NOT NULL,
  `rua` VARCHAR(100) NOT NULL,
  `porta` INT NOT NULL,
  `codigoPostalFilial` INT NOT NULL,
  PRIMARY KEY (`numero`),
  INDEX `codigoPostalFilial_idx` (`codigoPostalFilial` ASC) VISIBLE,
  CONSTRAINT `codigoPostalFilial`
    FOREIGN KEY (`codigoPostalFilial`)
    REFERENCES `sibd09`.`codigopostais` (`codigoPostal`))
ENGINE = InnoDB
DEFAULT CHARACTER SET = utf8mb4
COLLATE = utf8mb4_0900_ai_ci;


-- -----------------------------------------------------
-- Table `sibd09`.`servico`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `sibd09`.`servico` (
  `idServico` INT NOT NULL AUTO_INCREMENT,
  `valor` DECIMAL(10,2) NOT NULL,
  `nDias` INT NOT NULL,
  PRIMARY KEY (`idServico`))
ENGINE = InnoDB
DEFAULT CHARACTER SET = utf8mb4
COLLATE = utf8mb4_0900_ai_ci;


-- -----------------------------------------------------
-- Table `sibd09`.`tipoveiculo`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `sibd09`.`tipoveiculo` (
  `codigo` INT NOT NULL,
  `nome` VARCHAR(100) NOT NULL,
  `valorHora` FLOAT NOT NULL,
  PRIMARY KEY (`codigo`))
ENGINE = InnoDB
DEFAULT CHARACTER SET = utf8mb4
COLLATE = utf8mb4_0900_ai_ci;


-- -----------------------------------------------------
-- Table `sibd09`.`modelos`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `sibd09`.`modelos` (
  `modelo` VARCHAR(100) NOT NULL,
  `marca` VARCHAR(100) NOT NULL,
  PRIMARY KEY (`modelo`))
ENGINE = InnoDB
DEFAULT CHARACTER SET = utf8mb4
COLLATE = utf8mb4_0900_ai_ci;


-- -----------------------------------------------------
-- Table `sibd09`.`veiculos`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `sibd09`.`veiculos` (
  `matricula` VARCHAR(30) NOT NULL,
  `modelo` VARCHAR(100) NOT NULL,
  `codigo` INT NOT NULL,
  PRIMARY KEY (`matricula`),
  INDEX `modelo_idx` (`modelo` ASC) VISIBLE,
  INDEX `codigo_idx` (`codigo` ASC) VISIBLE,
  CONSTRAINT `codigo`
    FOREIGN KEY (`codigo`)
    REFERENCES `sibd09`.`tipoveiculo` (`codigo`),
  CONSTRAINT `modelo`
    FOREIGN KEY (`modelo`)
    REFERENCES `sibd09`.`modelos` (`modelo`))
ENGINE = InnoDB
DEFAULT CHARACTER SET = utf8mb4
COLLATE = utf8mb4_0900_ai_ci;


-- -----------------------------------------------------
-- Table `sibd09`.`cliente`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `sibd09`.`cliente` (
  `nic` INT NOT NULL AUTO_INCREMENT,
  `primeiroNome` VARCHAR(100) NOT NULL,
  `ultimoNome` VARCHAR(100) NOT NULL,
  `cartaConduçao` BIGINT NOT NULL,
  `telefone` BIGINT NOT NULL,
  `email` VARCHAR(100) NOT NULL,
  PRIMARY KEY (`nic`))
ENGINE = InnoDB
DEFAULT CHARACTER SET = utf8mb4
COLLATE = utf8mb4_0900_ai_ci;


-- -----------------------------------------------------
-- Table `sibd09`.`alugar`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `sibd09`.`alugar` (
  `codigo` INT NOT NULL AUTO_INCREMENT,
  `dataInicial` DATE NOT NULL,
  `dataFinal` DATE NOT NULL,
  `custo` DECIMAL(10,2) NOT NULL,
  `caucao` DECIMAL(10,2) NOT NULL,
  `nicCliente` INT NOT NULL,
  `idServicoAluguer` INT NOT NULL,
  `matriculaVeiculo` VARCHAR(30) NOT NULL,
  `codigoFilial` INT NOT NULL,
  PRIMARY KEY (`codigo`),
  INDEX `nicCliente_idx` (`nicCliente` ASC) VISIBLE,
  INDEX `idServicoAluguer_idx` (`idServicoAluguer` ASC) VISIBLE,
  INDEX `matriculaVeiculo_idx` (`matriculaVeiculo` ASC) VISIBLE,
  INDEX `codigoFilial_idx` (`codigoFilial` ASC) VISIBLE,
  CONSTRAINT `codigoFilial`
    FOREIGN KEY (`codigoFilial`)
    REFERENCES `sibd09`.`filial` (`numero`),
  CONSTRAINT `idServicoAluguer`
    FOREIGN KEY (`idServicoAluguer`)
    REFERENCES `sibd09`.`servico` (`idServico`),
  CONSTRAINT `matriculaVeiculo`
    FOREIGN KEY (`matriculaVeiculo`)
    REFERENCES `sibd09`.`veiculos` (`matricula`),
  CONSTRAINT `nicCliente`
    FOREIGN KEY (`nicCliente`)
    REFERENCES `sibd09`.`cliente` (`nic`))
ENGINE = InnoDB
DEFAULT CHARACTER SET = utf8mb4
COLLATE = utf8mb4_0900_ai_ci;


-- -----------------------------------------------------
-- Table `sibd09`.`departamento`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `sibd09`.`departamento` (
  `codigo` INT NOT NULL AUTO_INCREMENT,
  `rua` VARCHAR(100) NOT NULL,
  `porta` INT NOT NULL,
  `codigoPostal` INT NOT NULL,
  PRIMARY KEY (`codigo`),
  INDEX `codigoPostal_idx` (`codigoPostal` ASC) VISIBLE,
  CONSTRAINT `codigoPostal`
    FOREIGN KEY (`codigoPostal`)
    REFERENCES `sibd09`.`codigopostais` (`codigoPostal`))
ENGINE = InnoDB
DEFAULT CHARACTER SET = utf8mb4
COLLATE = utf8mb4_0900_ai_ci;


-- -----------------------------------------------------
-- Table `sibd09`.`funcionario`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `sibd09`.`funcionario` (
  `nic` INT NOT NULL,
  `primeiroNome` VARCHAR(100) NOT NULL,
  `ultimoNome` VARCHAR(100) NOT NULL,
  `endereco` VARCHAR(100) NOT NULL,
  `dataNascimento` DATE NOT NULL,
  `salario` DECIMAL(10,2) NOT NULL,
  `sexo` VARCHAR(100) NOT NULL,
  `codigoDepartamento` INT NOT NULL,
  `numeroFilial` INT NOT NULL,
  PRIMARY KEY (`nic`),
  INDEX `codigoDepartamento_idx` (`codigoDepartamento` ASC) VISIBLE,
  INDEX `numeroFilial_idx` (`numeroFilial` ASC) VISIBLE,
  CONSTRAINT `codigoDepartamento`
    FOREIGN KEY (`codigoDepartamento`)
    REFERENCES `sibd09`.`departamento` (`codigo`),
  CONSTRAINT `numeroFilial`
    FOREIGN KEY (`numeroFilial`)
    REFERENCES `sibd09`.`filial` (`numero`))
ENGINE = InnoDB
DEFAULT CHARACTER SET = utf8mb4
COLLATE = utf8mb4_0900_ai_ci;



## DML

### Tabela Funcionário

INSERT INTO `funcionario` (nic, primeiroNome, ultimoNome, sexo, endereco, salario, dataNascimento) VALUES 
('1', 'Antonio', 'Mendes' , 'masculino','antoniom@gmail.com','700','10/10/1980' ),
('2', 'Barbara', 'Mendonça' , 'feminino','barbaramends@gmail.com','600','2/7/1998' ),
('3', 'Carlos', 'Joel' , 'masculino','carlitosjoel@hotmail.com','600','1/1/1970' ),
('4', 'Diogo', 'Silva' , 'masculino','daizergamer@gmail.com','700','4/5/1994' ),
('5', 'Deolinda', 'Castro' , 'feminino','deolindinha@gmail.com','700','9/2/1989' ),
('6', 'Estrela', 'Novais' , 'feminino','atuaestrela909@hotmail.com','700','4/7/1999' ),
('7', 'Fernando', 'Alonso' , 'masculino','fernandinhos@gmail.com','700','9/8/1978' ),
('8', 'Joaquim', 'Albuquerque' , 'masculino','juaquindelpasso@gmail.com','700','4/3/1979' ),
('9', 'Telma', 'Barros' , 'feminino','telmaluca@gmail.com','600','1/9/1995' ),

INSERT INTO `cliente` (nic, telefone, email, cartaconducao, primeironome, ultimonome) VALUES 
('1', '960000001', 'joseantonio@gmail.com','100000001', 'José', 'Antonio'),
('comesticos', '2'),
('perfumaria', '3'),
('caixa', '4'),
('reposiçao', '5'),
('gerencia', '6'),
('limpeza', '7'),
('fornecedores', '8');


INSERT INTO `fornecedor` (nome, id, telefonepessoal, telefoneempresa) VALUES
('nome1', ' 1', '960000017', '200000017'),
('nome3', ' 3', '2960000018', '200000018'),
('nome5', '5', '960000019', '200000019');


INSERT INTO `horario` (id,horafim,horainicio, diasemana ) VALUES
('1', '10:00', '21:00', 'segundafeira'),
('2', '10:00', '21:00', 'terçafeira'),
('3', '10:00', '21:00', 'quartafeira'),
('4', '10:00', '21:00', 'quintafeira'),
('5' , '10:00', '22:00', 'sextafeira'),
('6', '10:00', '21:00', 'sabado'),
('7', '10:00', '18:00', 'domingo');

INSERT INTO `entrega` (nentrega, validade, reserva , quantidade) VALUES
('1', '21/03/2023', '45854833', '57'),
('2', '20/09/2023', '4585454', '34'),
('3', '10/02/2023', '21:00', '67');

INSERT INTO `produto` (nome, tipoproduto, codigo , validade) VALUES
('nome1 ', 'maquilhagem', '25894', '10/02/2024'),
('nome2', 'comestico', '5849', '10/02/2024'),
('nome3 ', 'perfumes', '94924', '15/06/2024'),
('nome4 ', 'maquilhagem', '67324', '15/06/2024'),
('nome5 ', 'perfumes', '53224', '20/01/2025'),
('nome6 ', 'comestico', '9524', '28/06/2024'),
('nome7 ', 'perfumes', '94924', '19/04/2024'),
('nome8 ', 'maquilhagem', '22524', '03/11/2024'),
('nome9 ', 'comesticos', '58424', '15/06/2024'),
('nome10 ', 'perfumes', '94924', '15/11/2024'),
('nome11 ', 'perfumes', '94924', '12/10/2024'),
('nome12 ', 'comesticos', '64334', '01/02/2024'),
('nome13 ', 'perfumes', '32114', '02/03/2024'),
('nome14 ', 'maquilhagem', '785334', '08/08/2024'),
('nome15 ', 'perfumes', '235753', '1/09/2025'),
('nome16 ', 'perfumes', '5632', '12/09/2024'),
('nome17 ', 'comesticos', '49493', '15/06/2024'),
('nome18 ', 'comesticos', '34532', '02/06/2024'),
('nome19 ', 'perfumes', '753432', '11/12/2024');

INSERT INTO `turno` (id, partedia, hora) VALUES
('1', 'manha', '09:30'),
('2', 'tarde', '13:00'),
('3', 'tarde', '17:00'),
('4', 'noite', '19:00'),
('5', 'noite', '21:00');

INSERT INTO `formaçao` (nome, tipoformaçao) VALUES
('nome1', 'maquilhagem'),
('nome2', 'cosmestica'),
('nome3', 'perfumaria');

#### Mencione o nome do funcionário com o número Id 10:

SELECT nome

FROM Funcionarios

WHERE Id= “10”

#### Mencione todos os funcionários da filial Porto:

SELECT nome

FROM funcionarios

Where Filial= “Porto”

#### Mencione os funcionários com a função gerente:

SELECT nome

FROM funcionarios

WHERE Função= "Gerente"

---
[< Previous](rebd04.md) | [^ Main](https://github.com/exemploTrabalho/reportSIBD/) | Next >
:--- | :---: | ---: 
