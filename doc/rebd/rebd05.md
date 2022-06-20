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
('10', 'Goncalo', 'Carvalho' , 'masculino','goncacarvalho@gmail.com','800','5/4/1990' ),
('11', 'Rosário', 'Graça' , 'feminino','rosariog@gmail.com','750','10/9/1985' ),
('12', 'Bruna', 'Silva' , 'feminino','brunas@gmail.com','600','20/2/1980' ),
('13', 'Pedro', 'Cardoso' , 'masculino','pedrocardoso@gmail.com','800','2/1/1993' ),
('14', 'Joel', 'Costa' , 'masculino','joelcosta@gmail.com','600','7/10/1998' ),
('15', 'Tatiana', 'Barbosa' , 'feminino','tatianabarbosa@gmail.com','650','15/9/1982' ),
('16', 'Tiago', 'Teixeira' , 'masculino','tiagoteixeirinha@gmail.com','800','10/4/1995' ),
('17', 'Rafael', 'Goncalves' , 'masculino','rafagoncalves@gmail.com','800','18/3/1990' ),
('18', 'César', 'Novais' , 'masculino','cesarn@gmail.com','600','17/8/1993' ),
('19', 'Sara', 'Miranda' , 'feminino','saramiranda@gmail.com','700','1/1/1984' ),
('20', 'Gustavo', 'Assunção' , 'masculino','gustavoassuncao@gmail.com','700','25/4/1975' ),

INSERT INTO `cliente` (nic, telefone, email, cartaconducao, primeironome, ultimonome) VALUES 
('960500001', 'joseantonio@hotmail.com','100000001', 'José', 'Antonio'),
('960300002', 'amonteiro@gmail.com','100500002', 'Augusto', 'Monteiro'),
('960200003', 'arnaldocosta@gmail.com','100040003', 'Arnaldo', 'Costa'),
('960000504', 'pteixeira@hotmail.com','100000704', 'Pedro', 'Teixeira'),
('960060005', 'jojoteixeira@gmail.com','100009005', 'Joana', 'Amaro'),
('960070006', 'joaquimal@gmail.com','160008006', 'Joaquim', 'Alberto'),
('960090007', 'anibalfernandes@gmail.com','100050007', 'Anibal', 'Fernandes'),
('960100008', 'xaviera@gmail.com','103000008', 'Xavier', 'Angélico'),
('960003009', 'catarinabarbosa@hotmail.com','100040009', 'Catarina','Barbosa'),
('964000010', 'dcardoso@gmail.com','102000010', 'Daniela','Cardoso'),

INSERT INTO `alugar` (codigo, datainicial, datafinal, custo, caucao) VALUES
('5/7/2022', '10/7/2022', '200', '15'),
('13/7/2022', '20/7/2022', '300', '25'),
('17/7/2022', '24/7/2022', '350', '20'),
('25/7/2022', '2/8/2022', '400', '30'),
('29/7/2022', '8/8/2022', '600', '35'),

INSERT INTO `filial` (numero, codigopostal, localidade, rua, porta) VALUES
('1', '4400-395', 'VilaNovaDeGaia', 'rua Antonio Ferreira', '25'),
('2', '4000-35', 'Porto', 'rua Ruben Castro', '10'),
('3', '4700-200', 'Braga', 'rua Pessoa', '5'),
('4', '2400-395', 'Leria', 'rua Miranda', '30'),
('5', '8000-395', 'Faro', 'rua Isabel Sousa', '50'),
('6', '1000-395', 'Lisboa', 'rua Pinheiro bravo', '40'),
('7', '5300-395', 'Bragança', 'rua de bustes', '75'),
('8', '7300-395', 'Portalegre', 'rua Orlando texeira', '60'),
('9', '7000-395', 'Évora', 'rua Arlindo fonseca', '3'),

INSERT INTO `TipoVeiculo` (codigo, nome, valorHora) VALUES
('1', transportepessoas, 15/h),
('2', transportemercadoria, 30/h),
('3', transportemercadoria, 10/h),
('4', transportepessoas, 20/h),

INSERT INTO `departamento` (codigopostal, localidade , rua, porta) VALUES
('4200-200', 'Porto', 'rua Jose pereira', '20'),
('2000-100', 'Lisboa', 'rua Amaro fernandes', '50'),

INSERT INTO `veiculo` (matricula, marca, modelo) VALUES
('N4FG85', 'Audi', 'A2'),
('N4FG85', 'Mercedes', 'Classe A'),
('N4FG85', 'Fiat', '500'),
('N4FG85', 'Renault', 'Clio'),
('N4FG85', 'Peugeot', '2008'),
('N4FG85', 'Mini', 'Cooper'),
('N4FG85', 'Audi', 'A4'),
('N4FG85', 'BMW', 'X2'),

INSERT INTO `serviço` (idservico, valor, ndias) VALUES
('500', '10'),
('300', '5'),
('700', '15'),
('200', '4'),
('500', '8'),
('800', '18'),
('250', '4'),
('300', '7'),
('450', '10'),
('400', '9'),


---
[< Previous](rebd04.md) | [^ Main](https://github.com/exemploTrabalho/reportSIBD/) | Next >
:--- | :---: | ---: 
