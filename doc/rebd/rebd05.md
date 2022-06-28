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

### Tabela Modelos

insert into modelos (modelo, marca) values (1, 'Mercedes');

insert into modelos (modelo, marca) values (2, 'Volvo');

insert into modelos (modelo, marca) values (3, 'Ferrari');

insert into modelos (modelo, marca) values (4, 'Bmw');

insert into modelos (modelo, marca) values (5, 'Audi');


### Tabela tipoVeiculo

insert into tipoveiculo (codigo, nome, valorHora) values (1, 'Pesado passageiros', 10);


insert into tipoveiculo (codigo, nome, valorHora) values (2, 'Pesado mercadorias', 20);

insert into tipoveiculo (codigo, nome, valorHora) values (3, 'Ligeiro mercadorias', 15);

insert into tipoveiculo (codigo, nome, valorHora) values (4, 'Ligeiro passageiros', 16);

insert into tipoveiculo (codigo, nome, valorHora) values (5, 'Pesado passageiros', 10);

### Tabela Veiculos

insert into veiculos (matricula, modelo, codigo) values (1, 1, 1);

insert into veiculos (matricula, modelo, codigo) values (2, 3, 2);

insert into veiculos (matricula, modelo, codigo) values (3, 2, 3);

insert into veiculos (matricula, modelo, codigo) values (4, 4, 4);

insert into veiculos (matricula, modelo, codigo) values (5, 5, 5);

insert into veiculos (matricula, modelo, codigo) values (6, 5, 1);

insert into veiculos (matricula, modelo, codigo) values (7, 5, 2);

insert into veiculos (matricula, modelo, codigo) values (8, 3, 3);

insert into veiculos (matricula, modelo, codigo) values (9, 1, 4);

insert into veiculos (matricula, modelo, codigo) values (10, 3, 5);

### Tabela Servico

insert into servico (valor, nDias) values (10, 3);

insert into servico (valor, nDias) values (12, 4);

insert into servico (valor, nDias) values (15, 6);

insert into servico (valor, nDias) values (17, 8);

insert into servico (valor, nDias) values (4, 1);

insert into servico (valor, nDias) values (7, 9);

insert into servico (valor, nDias) values (15, 15);

### Tabela codigoPostais

insert into codigopostais (codigoPostal, localidade) values (10, 'Mariz');

insert into codigopostais (codigoPostal, localidade) values (20, 'Perelhal');

insert into codigopostais (codigoPostal, localidade) values (30, 'Cossourado');

insert into codigopostais (codigoPostal, localidade) values (40, 'Vila Frescainha');

insert into codigopostais (codigoPostal, localidade) values (50, 'Creixomil');

insert into codigopostais (codigoPostal, localidade) values (60, 'São Pedro');

insert into codigopostais (codigoPostal, localidade) values (70, 'Vila Boa');

insert into codigopostais (codigoPostal, localidade) values (80, 'Esposende');

insert into codigopostais (codigoPostal, localidade) values (90, 'Fão');

insert into codigopostais (codigoPostal, localidade) values (100, 'Roriz');

### Tabela Cliente

insert into cliente (primeiroNome, ultimoNome, cartaConduçao, telefone, email, codigoPostal) values ('Lanae', 'Churly', '9642973901', '3083748920', 'lchurly0@wikia.com', 50);

insert into cliente (primeiroNome, ultimoNome, cartaConduçao, telefone, email, codigoPostal) values ('Farra', 'Dupey', '9208776387', '9725623804', 'fdupey1@ted.com', 30);

insert into cliente (primeiroNome, ultimoNome, cartaConduçao, telefone, email, codigoPostal) values ('Tomas', 'Shilburne', '1108237576', '6265351275', 'tshilburne2@cmu.edu', 70);

insert into cliente (primeiroNome, ultimoNome, cartaConduçao, telefone, email, codigoPostal) values ('Ephrem', 'Pauleit', '2997896533', '1595456694', 'epauleit3@cmu.edu', 70);

insert into cliente (primeiroNome, ultimoNome, cartaConduçao, telefone, email, codigoPostal) values ('Lucais', 'Schwanden', '1099724341', '3449090548', 'lschwanden4@so-net.ne.jp', 100);

insert into cliente (primeiroNome, ultimoNome, cartaConduçao, telefone, email, codigoPostal) values ('Cozmo', 'Farnall', '6052349581', '6599863239', 'cfarnall5@ning.com', 30);

insert into cliente (primeiroNome, ultimoNome, cartaConduçao, telefone, email, codigoPostal) values ('Dalton', 'Lineen', '3827645719', '5366986709', 'dlineen6@last.fm', 70);

insert into cliente (primeiroNome, ultimoNome, cartaConduçao, telefone, email, codigoPostal) values ('Sheelah', 'Wille', '7298622935', '1046526645', 'swille7@unicef.org', 40);

insert into cliente (primeiroNome, ultimoNome, cartaConduçao, telefone, email, codigoPostal) values ('Harri', 'Krale', '3603593774', '4229671895', 'hkrale8@t.co', 30);

insert into cliente (primeiroNome, ultimoNome, cartaConduçao, telefone, email, codigoPostal) values ('Cherry', 'Hunnaball', '7710629121', '9493371911', 'chunnaball9@tuttocitta.it', 90);

insert into cliente (primeiroNome, ultimoNome, cartaConduçao, telefone, email, codigoPostal) values ('Marris', 'I''anson', '5466443417', '2385750115', 'miansona@pen.io', 70);

insert into cliente (primeiroNome, ultimoNome, cartaConduçao, telefone, email, codigoPostal) values ('Devlin', 'Wigan', '8947316237', '7738161972', 'dwiganb@myspace.com', 20);

insert into cliente (primeiroNome, ultimoNome, cartaConduçao, telefone, email, codigoPostal) values ('Arabelle', 'Batcheldor', '2417746549', '3017144192', 'abatcheldorc@rambler.ru', 100);

insert into cliente (primeiroNome, ultimoNome, cartaConduçao, telefone, email, codigoPostal) values ('Charita', 'Phillps', '0306185318', '3788924268', 'cphillpsd@fema.gov', 100);

insert into cliente (primeiroNome, ultimoNome, cartaConduçao, telefone, email, codigoPostal) values ('Jo-anne', 'Lloyd-Williams', '6130095597', '1033167154', 'jlloydwilliamse@barnesandnoble.com', 30);

insert into cliente (primeiroNome, ultimoNome, cartaConduçao, telefone, email, codigoPostal) values ('Harwilll', 'Blenkharn', '0824610040', '4116700808', 'hblenkharnf@businessweek.com', 100);

insert into cliente (primeiroNome, ultimoNome, cartaConduçao, telefone, email, codigoPostal) values ('Katrinka', 'McGuggy', '9953867879', '7007823382', 'kmcguggyg@npr.org', 10);

insert into cliente (primeiroNome, ultimoNome, cartaConduçao, telefone, email, codigoPostal) values ('Grace', 'Pays', '2165003059', '8394984583', 'gpaysh@bigcartel.com', 80);

insert into cliente (primeiroNome, ultimoNome, cartaConduçao, telefone, email, codigoPostal) values ('Karie', 'Hemerijk', '0756837715', '8635506363', 'khemerijki@liveinternet.ru', 80);

insert into cliente (primeiroNome, ultimoNome, cartaConduçao, telefone, email, codigoPostal) values ('Janka', 'Dunston', '9320060320', '5658585669', 'jdunstonj@last.fm', 30);

insert into cliente (primeiroNome, ultimoNome, cartaConduçao, telefone, email, codigoPostal) values ('Annnora', 'Bontein', '7583265967', '8902185542', 'abonteink@exblog.jp', 20);

insert into cliente (primeiroNome, ultimoNome, cartaConduçao, telefone, email, codigoPostal) values ('Mallory', 'Withinshaw', '3810397628', '3466082285', 'mwithinshawl@engadget.com', 70);

insert into cliente (primeiroNome, ultimoNome, cartaConduçao, telefone, email, codigoPostal) values ('Charyl', 'Andover', '6745494736', '2563217105', 'candoverm@gnu.org', 30);

insert into cliente (primeiroNome, ultimoNome, cartaConduçao, telefone, email, codigoPostal) values ('Delaney', 'Braunton', '6361585034', '5374516691', 'dbrauntonn@usda.gov', 70);

insert into cliente (primeiroNome, ultimoNome, cartaConduçao, telefone, email, codigoPostal) values ('Anjela', 'Chettle', '3816701035', '6174769129', 'achettleo@psu.edu', 40);

insert into cliente (primeiroNome, ultimoNome, cartaConduçao, telefone, email, codigoPostal) values ('Adaline', 'Wait', '7307152983', '7075106832', 'awaitp@phpbb.com', 20);

insert into cliente (primeiroNome, ultimoNome, cartaConduçao, telefone, email, codigoPostal) values ('Norrie', 'Chamberlayne', '3359943732', '6004386687', 'nchamberlayneq@trellian.com', 30);

insert into cliente (primeiroNome, ultimoNome, cartaConduçao, telefone, email, codigoPostal) values ('Casper', 'Shearme', '0539490717', '9541001522', 'cshearmer@globo.com', 30);

insert into cliente (primeiroNome, ultimoNome, cartaConduçao, telefone, email, codigoPostal) values ('Davida', 'Rathe', '0433482737', '8159417433', 'drathes@tuttocitta.it', 100);

insert into cliente (primeiroNome, ultimoNome, cartaConduçao, telefone, email, codigoPostal) values ('Lester', 'Hardinge', '5744606289', '2251958555', 'lhardinget@imageshack.us', 50);

insert into cliente (primeiroNome, ultimoNome, cartaConduçao, telefone, email, codigoPostal) values ('Happy', 'Wearden', '9179691196', '1526177953', 'hweardenu@cnbc.com', 40);

insert into cliente (primeiroNome, ultimoNome, cartaConduçao, telefone, email, codigoPostal) values ('Dalli', 'Parradine', '9383894016', '1095194693', 'dparradinev@technorati.com', 80);

insert into cliente (primeiroNome, ultimoNome, cartaConduçao, telefone, email, codigoPostal) values ('Alejandra', 'Powder', '7674181693', '7679409628', 'apowderw@123-reg.co.uk', 70);

insert into cliente (primeiroNome, ultimoNome, cartaConduçao, telefone, email, codigoPostal) values ('Darline', 'Ambroz', '1953735665', '2274237427', 'dambrozx@simplemachines.org', 90);

insert into cliente (primeiroNome, ultimoNome, cartaConduçao, telefone, email, codigoPostal) values ('Hilton', 'Taaffe', '5478089052', '9668084654', 'htaaffey@bluehost.com', 80);

insert into cliente (primeiroNome, ultimoNome, cartaConduçao, telefone, email, codigoPostal) values ('Hart', 'Hambling', '7626680030', '8032419357', 'hhamblingz@businessinsider.com', 20);

insert into cliente (primeiroNome, ultimoNome, cartaConduçao, telefone, email, codigoPostal) values ('Marcos', 'Ferrie', '2571326589', '8894376619', 'mferrie10@networksolutions.com', 60);

insert into cliente (primeiroNome, ultimoNome, cartaConduçao, telefone, email, codigoPostal) values ('Marcos', 'Pursglove', '3364029156', '9786161652', 'mpursglove11@uiuc.edu', 90);

insert into cliente (primeiroNome, ultimoNome, cartaConduçao, telefone, email, codigoPostal) values ('Nicolea', 'Rameaux', '1589241010', '3117469784', 'nrameaux12@narod.ru', 70);

insert into cliente (primeiroNome, ultimoNome, cartaConduçao, telefone, email, codigoPostal) values ('Stefanie', 'Philbrook', '6877245369', '9629087528', 'sphilbrook13@issuu.com', 70);

### Tabela Departamento

insert into Departamento (rua, porta, codigoPostal) values ('Anhalt', '07503', 60);

insert into Departamento (rua, porta, codigoPostal) values ('Montana', '8', 30);

insert into Departamento (rua, porta, codigoPostal) values ('Vahlen', '4620', 50);

insert into Departamento (rua, porta, codigoPostal) values ('Brentwood', '07', 30);

insert into Departamento (rua, porta, codigoPostal) values ('Eagle Crest', '321', 80);

insert into Departamento (rua, porta, codigoPostal) values ('Brown', '54185', 100);

insert into Departamento (rua, porta, codigoPostal) values ('Caliangt', '82', 10);

insert into Departamento (rua, porta, codigoPostal) values ('Forest Dale', '0', 50);

insert into Departamento (rua, porta, codigoPostal) values ('Barby', '5', 60);

insert into Departamento (rua, porta, codigoPostal) values ('Monica', '6', 40);

insert into Departamento (rua, porta, codigoPostal) values ('Toban', '2258', 50);

insert into Departamento (rua, porta, codigoPostal) values ('Golf Course', '469', 50);

insert into Departamento (rua, porta, codigoPostal) values ('Rockefeller', '5', 70);

insert into Departamento (rua, porta, codigoPostal) values ('Moland', '966', 30);

insert into Departamento (rua, porta, codigoPostal) values ('Havey', '86127', 50);

insert into Departamento (rua, porta, codigoPostal) values ('Thackeray', '4', 80);

insert into Departamento (rua, porta, codigoPostal) values ('Chive', '977', 60);

insert into Departamento (rua, porta, codigoPostal) values ('Hudson', '6', 50);

insert into Departamento (rua, porta, codigoPostal) values ('Carpenter', '5388', 20);

insert into Departamento (rua, porta, codigoPostal) values ('International', '3', 20);

insert into Departamento (rua, porta, codigoPostal) values ('Beilfuss', '3', 70);

insert into Departamento (rua, porta, codigoPostal) values ('Algoma', '397', 10);

insert into Departamento (rua, porta, codigoPostal) values ('Columbus', '80', 50);

insert into Departamento (rua, porta, codigoPostal) values ('Towne', '55590', 80);

insert into Departamento (rua, porta, codigoPostal) values ('Morning', '830', 30);

insert into Departamento (rua, porta, codigoPostal) values ('Pennsylvania', '8577', 50);

insert into Departamento (rua, porta, codigoPostal) values ('Dexter', '96044', 90);

insert into Departamento (rua, porta, codigoPostal) values ('Luster', '20479', 80);

insert into Departamento (rua, porta, codigoPostal) values ('American Ash', '628', 10);

insert into Departamento (rua, porta, codigoPostal) values ('Graedel', '06427', 30);


---
[< Previous](rebd04.md) | [^ Main](https://github.com/exemploTrabalho/reportSIBD/) | Next >
:--- | :---: | ---: 
