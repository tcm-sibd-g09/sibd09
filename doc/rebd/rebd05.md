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
AUTO_INCREMENT = 31
DEFAULT CHARACTER SET = utf8mb4
COLLATE = utf8mb4_0900_ai_ci;


-- -----------------------------------------------------
-- Table `sibd09`.`filial`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `sibd09`.`filial` (
  `numero` INT NOT NULL AUTO_INCREMENT,
  `rua` VARCHAR(100) NOT NULL,
  `porta` INT NOT NULL,
  `codigoPostalFilial` INT NOT NULL,
  `codigoDepartamento` INT NOT NULL,
  PRIMARY KEY (`numero`),
  INDEX `codigoPostalFilial_idx` (`codigoPostalFilial` ASC) VISIBLE,
  INDEX `codFilial_idx` (`codigoDepartamento` ASC) VISIBLE,
  CONSTRAINT `codFilial`
    FOREIGN KEY (`codigoDepartamento`)
    REFERENCES `sibd09`.`departamento` (`codigo`),
  CONSTRAINT `codigoPostalFilial`
    FOREIGN KEY (`codigoPostalFilial`)
    REFERENCES `sibd09`.`codigopostais` (`codigoPostal`))
ENGINE = InnoDB
AUTO_INCREMENT = 61
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
AUTO_INCREMENT = 8
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
  `codigoPostal` INT NOT NULL,
  PRIMARY KEY (`nic`),
  INDEX `codPostal_idx` (`codigoPostal` ASC) VISIBLE,
  CONSTRAINT `codPostal`
    FOREIGN KEY (`codigoPostal`)
    REFERENCES `sibd09`.`codigopostais` (`codigoPostal`))
ENGINE = InnoDB
AUTO_INCREMENT = 41
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
AUTO_INCREMENT = 121
DEFAULT CHARACTER SET = utf8mb4
COLLATE = utf8mb4_0900_ai_ci;


-- -----------------------------------------------------
-- Table `sibd09`.`funcionario`
-- -----------------------------------------------------
CREATE TABLE IF NOT EXISTS `sibd09`.`funcionario` (
  `nic` INT NOT NULL AUTO_INCREMENT,
  `primeiroNome` VARCHAR(100) NOT NULL,
  `ultimoNome` VARCHAR(100) NOT NULL,
  `endereco` VARCHAR(100) NOT NULL,
  `dataNascimento` DATE NOT NULL,
  `salario` DECIMAL(10,2) NOT NULL,
  `sexo` VARCHAR(100) NOT NULL,
  `codigoDepartamento` INT NOT NULL,
  `codigoFilial` INT NOT NULL,
  PRIMARY KEY (`nic`),
  INDEX `codigoDepartamento_idx` (`codigoDepartamento` ASC) VISIBLE,
  INDEX `codigoFilial_idx` (`codigoFilial` ASC) VISIBLE,
  CONSTRAINT `codigoDepartamento`
    FOREIGN KEY (`codigoDepartamento`)
    REFERENCES `sibd09`.`departamento` (`codigo`),
  CONSTRAINT `codigoFilial2`
    FOREIGN KEY (`codigoFilial`)
    REFERENCES `sibd09`.`filial` (`numero`))
ENGINE = InnoDB
AUTO_INCREMENT = 121
DEFAULT CHARACTER SET = utf8mb4
COLLATE = utf8mb4_0900_ai_ci;


SET SQL_MODE=@OLD_SQL_MODE;
SET FOREIGN_KEY_CHECKS=@OLD_FOREIGN_KEY_CHECKS;
SET UNIQUE_CHECKS=@OLD_UNIQUE_CHECKS;


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

### Tabela Filial

insert into filial (rua, porta, codigoPostalFilial, codigoDepartamento) values ('Sherman', '55', 10, 1);

insert into filial (rua, porta, codigoPostalFilial, codigoDepartamento) values ('Hagan', '27', 20, 2);

insert into filial (rua, porta, codigoPostalFilial, codigoDepartamento) values ('Kenwood', '84', 30, 3);

insert into filial (rua, porta, codigoPostalFilial, codigoDepartamento) values ('Bowman', '10291', 40, 4);

insert into filial (rua, porta, codigoPostalFilial, codigoDepartamento) values ('Di Loreto', '5', 50, 5);

insert into filial (rua, porta, codigoPostalFilial, codigoDepartamento) values ('Vidon', '167', 60, 6);

insert into filial (rua, porta, codigoPostalFilial, codigoDepartamento) values ('Hansons', '0', 70, 7);

insert into filial (rua, porta, codigoPostalFilial, codigoDepartamento) values ('Upham', '44632', 80, 8);

insert into filial (rua, porta, codigoPostalFilial, codigoDepartamento) values ('Village', '71', 90, 9);

insert into filial (rua, porta, codigoPostalFilial, codigoDepartamento) values ('Melrose', '9247', 100, 10);

insert into filial (rua, porta, codigoPostalFilial, codigoDepartamento) values ('Kenwood', '7694', 10, 11);

insert into filial (rua, porta, codigoPostalFilial, codigoDepartamento) values ('Oak', '8634', 20, 12);

insert into filial (rua, porta, codigoPostalFilial, codigoDepartamento) values ('Sauthoff', '6', 30, 13);

insert into filial (rua, porta, codigoPostalFilial, codigoDepartamento) values ('Westridge', '428', 40, 14);

insert into filial (rua, porta, codigoPostalFilial, codigoDepartamento) values ('Melrose', '35671', 50, 15);

insert into filial (rua, porta, codigoPostalFilial, codigoDepartamento) values ('Victoria', '9196', 60, 16);

insert into filial (rua, porta, codigoPostalFilial, codigoDepartamento) values ('Coolidge', '682', 70, 17);

insert into filial (rua, porta, codigoPostalFilial, codigoDepartamento) values ('Ridgeview', '657', 80, 18);

insert into filial (rua, porta, codigoPostalFilial, codigoDepartamento) values ('Kinsman', '34', 90, 19);

insert into filial (rua, porta, codigoPostalFilial, codigoDepartamento) values ('Sloan', '15', 100, 20);

insert into filial (rua, porta, codigoPostalFilial, codigoDepartamento) values ('Hoepker', '139', 10, 21);

insert into filial (rua, porta, codigoPostalFilial, codigoDepartamento) values ('Waxwing', '94432', 20, 22);

insert into filial (rua, porta, codigoPostalFilial, codigoDepartamento) values ('Cherokee', '20717', 30, 23);

insert into filial (rua, porta, codigoPostalFilial, codigoDepartamento) values ('Shasta', '69', 40, 24);

insert into filial (rua, porta, codigoPostalFilial, codigoDepartamento) values ('Donald', '79', 50, 25);

insert into filial (rua, porta, codigoPostalFilial, codigoDepartamento) values ('Morningstar', '5769', 60, 26);

insert into filial (rua, porta, codigoPostalFilial, codigoDepartamento) values ('Jenifer', '9628', 70, 27);

insert into filial (rua, porta, codigoPostalFilial, codigoDepartamento) values ('Armistice', '8511', 80, 28);

insert into filial (rua, porta, codigoPostalFilial, codigoDepartamento) values ('Surrey', '1', 90, 29);

insert into filial (rua, porta, codigoPostalFilial, codigoDepartamento) values ('Pepper Wood', '590', 100, 30);

insert into filial (rua, porta, codigoPostalFilial, codigoDepartamento) values ('Elmside', '927', 10, 1);

insert into filial (rua, porta, codigoPostalFilial, codigoDepartamento) values ('Vahlen', '694', 20, 2);

insert into filial (rua, porta, codigoPostalFilial, codigoDepartamento) values ('Del Mar', '48062', 30, 3);

insert into filial (rua, porta, codigoPostalFilial, codigoDepartamento) values ('Burning Wood', '62', 40, 4);

insert into filial (rua, porta, codigoPostalFilial, codigoDepartamento) values ('5th', '00', 50, 5);

insert into filial (rua, porta, codigoPostalFilial, codigoDepartamento) values ('Eastwood', '090', 60, 6);

insert into filial (rua, porta, codigoPostalFilial, codigoDepartamento) values ('Gerald', '5688', 70, 7);

insert into filial (rua, porta, codigoPostalFilial, codigoDepartamento) values ('Bay', '62126', 80, 8);

insert into filial (rua, porta, codigoPostalFilial, codigoDepartamento) values ('Hovde', '10', 90, 9);

insert into filial (rua, porta, codigoPostalFilial, codigoDepartamento) values ('Graceland', '429', 100, 10);

insert into filial (rua, porta, codigoPostalFilial, codigoDepartamento) values ('Everett', '22081', 10, 11);

insert into filial (rua, porta, codigoPostalFilial, codigoDepartamento) values ('Starling', '436', 20, 12);

insert into filial (rua, porta, codigoPostalFilial, codigoDepartamento) values ('Ridge Oak', '185', 30, 13);

insert into filial (rua, porta, codigoPostalFilial, codigoDepartamento) values ('Hintze', '29', 40, 14);

insert into filial (rua, porta, codigoPostalFilial, codigoDepartamento) values ('Londonderry', '825', 50, 15);

insert into filial (rua, porta, codigoPostalFilial, codigoDepartamento) values ('Lunder', '9220', 60, 16);

insert into filial (rua, porta, codigoPostalFilial, codigoDepartamento) values ('Sunbrook', '741', 70, 17);

insert into filial (rua, porta, codigoPostalFilial, codigoDepartamento) values ('Sunnyside', '930', 80, 18);

insert into filial (rua, porta, codigoPostalFilial, codigoDepartamento) values ('Susan', '531', 90, 19);

insert into filial (rua, porta, codigoPostalFilial, codigoDepartamento) values ('Riverside', '2903', 100, 20);

insert into filial (rua, porta, codigoPostalFilial, codigoDepartamento) values ('Tennessee', '769', 10, 21);

insert into filial (rua, porta, codigoPostalFilial, codigoDepartamento) values ('Weeping Birch', '550', 20, 22);

insert into filial (rua, porta, codigoPostalFilial, codigoDepartamento) values ('Talmadge', '9751', 30, 23);

insert into filial (rua, porta, codigoPostalFilial, codigoDepartamento) values ('Vernon', '67', 40, 24);

insert into filial (rua, porta, codigoPostalFilial, codigoDepartamento) values ('Killdeer', '339', 50, 25);

insert into filial (rua, porta, codigoPostalFilial, codigoDepartamento) values ('Texas', '5944', 60, 26);

insert into filial (rua, porta, codigoPostalFilial, codigoDepartamento) values ('Mesta', '396', 70, 27);

insert into filial (rua, porta, codigoPostalFilial, codigoDepartamento) values ('Annamark', '49959', 80, 28);

insert into filial (rua, porta, codigoPostalFilial, codigoDepartamento) values ('Chinook', '481', 90, 29);

insert into filial (rua, porta, codigoPostalFilial, codigoDepartamento) values ('Cody', '162', 100, 30);


### Tabela Funcionario

insert into funcionario (primeiroNome, ultimoNome, endereco, dataNascimento, salario, sexo, codigoDepartamento, codigoFilial) values ('Weidar', 'MacAree', 'wmacaree0@hexun.com', '2022-06-20', '1456', 'masculino', 1, 1);

insert into funcionario (primeiroNome, ultimoNome, endereco, dataNascimento, salario, sexo, codigoDepartamento, codigoFilial) values ('Aurora', 'Whitwam', 'awhitwam1@gizmodo.com', '2017-05-17', '95895', 'feminino', 2, 2);

insert into funcionario (primeiroNome, ultimoNome, endereco, dataNascimento, salario, sexo, codigoDepartamento, codigoFilial) values ('Dag', 'Julien', 'djulien2@weebly.com', '2019-04-13', '80', 'masculino', 3, 3);

insert into funcionario (primeiroNome, ultimoNome, endereco, dataNascimento, salario, sexo, codigoDepartamento, codigoFilial) values ('Rubi', 'Hrynczyk', 'rhrynczyk3@ning.com', '2022-03-27', '06051', 'feminino', 4, 4);

insert into funcionario (primeiroNome, ultimoNome, endereco, dataNascimento, salario, sexo, codigoDepartamento, codigoFilial) values ('Lars', 'Gaiter', 'lgaiter4@tiny.cc', '2017-04-02', '9539', 'masculino', 5, 5);

insert into funcionario (primeiroNome, ultimoNome, endereco, dataNascimento, salario, sexo, codigoDepartamento, codigoFilial) values ('Aubrie', 'Heasman', 'aheasman5@noaa.gov', '2019-06-23', '90', 'feminino', 6, 6);

insert into funcionario (primeiroNome, ultimoNome, endereco, dataNascimento, salario, sexo, codigoDepartamento, codigoFilial) values ('Emmye', 'Sutworth', 'esutworth6@google.com.au', '2017-07-29', '7123', 'masculino', 7, 7);

insert into funcionario (primeiroNome, ultimoNome, endereco, dataNascimento, salario, sexo, codigoDepartamento, codigoFilial) values ('Rowen', 'Durdle', 'rdurdle7@blog.com', '2018-03-06', '01', 'feminino', 8, 8);

insert into funcionario (primeiroNome, ultimoNome, endereco, dataNascimento, salario, sexo, codigoDepartamento, codigoFilial) values ('Temp', 'Tiery', 'ttiery8@ameblo.jp', '2022-05-31', '490', 'masculino', 9, 9);

insert into funcionario (primeiroNome, ultimoNome, endereco, dataNascimento, salario, sexo, codigoDepartamento, codigoFilial) values ('Norby', 'Philot', 'nphilot9@thetimes.co.uk', '2018-01-23', '98', 'feminino', 10, 10);

insert into funcionario (primeiroNome, ultimoNome, endereco, dataNascimento, salario, sexo, codigoDepartamento, codigoFilial) values ('Sher', 'Allkins', 'sallkinsa@cloudflare.com', '2022-03-11', '16', 'masculino', 11, 11);

insert into funcionario (primeiroNome, ultimoNome, endereco, dataNascimento, salario, sexo, codigoDepartamento, codigoFilial) values ('Harmonia', 'Innot', 'hinnotb@noaa.gov', '2017-05-31', '81', 'feminino', 12, 12);

insert into funcionario (primeiroNome, ultimoNome, endereco, dataNascimento, salario, sexo, codigoDepartamento, codigoFilial) values ('Domini', 'Van Driel', 'dvandrielc@google.de', '2021-12-25', '8', 'masculino', 13, 13);

insert into funcionario (primeiroNome, ultimoNome, endereco, dataNascimento, salario, sexo, codigoDepartamento, codigoFilial) values ('Kassie', 'Taysbil', 'ktaysbild@yellowpages.com', '2018-06-14', '80', 'feminino', 14, 14);

insert into funcionario (primeiroNome, ultimoNome, endereco, dataNascimento, salario, sexo, codigoDepartamento, codigoFilial) values ('Gerhardine', 'Dobel', 'gdobele@tamu.edu', '2019-06-21', '40233', 'masculino', 15, 15);

insert into funcionario (primeiroNome, ultimoNome, endereco, dataNascimento, salario, sexo, codigoDepartamento, codigoFilial) values ('Aleda', 'Coneley', 'aconeleyf@sciencedaily.com', '2017-12-02', '2837', 'feminino', 16, 16);

insert into funcionario (primeiroNome, ultimoNome, endereco, dataNascimento, salario, sexo, codigoDepartamento, codigoFilial) values ('Nealon', 'Gulleford', 'ngullefordg@dailymotion.com', '2022-03-21', '6740', 'masculino', 17, 17);

insert into funcionario (primeiroNome, ultimoNome, endereco, dataNascimento, salario, sexo, codigoDepartamento, codigoFilial) values ('Jerrine', 'Hollingby', 'jhollingbyh@reuters.com', '2018-07-29', '4', 'feminino', 18, 18);

insert into funcionario (primeiroNome, ultimoNome, endereco, dataNascimento, salario, sexo, codigoDepartamento, codigoFilial) values ('Milo', 'Butterfield', 'mbutterfieldi@ovh.net', '2017-08-25', '81', 'masculino', 19, 19);

insert into funcionario (primeiroNome, ultimoNome, endereco, dataNascimento, salario, sexo, codigoDepartamento, codigoFilial) values ('Bram', 'Fawthrop', 'bfawthropj@ihg.com', '2021-02-25', '9410', 'feminino', 20, 20);

insert into funcionario (primeiroNome, ultimoNome, endereco, dataNascimento, salario, sexo, codigoDepartamento, codigoFilial) values ('Lion', 'Laurand', 'llaurandk@homestead.com', '2017-11-01', '60', 'masculino', 21, 21);

insert into funcionario (primeiroNome, ultimoNome, endereco, dataNascimento, salario, sexo, codigoDepartamento, codigoFilial) values ('Marjy', 'Rebeiro', 'mrebeirol@people.com.cn', '2022-03-19', '73', 'feminino', 22, 22);

insert into funcionario (primeiroNome, ultimoNome, endereco, dataNascimento, salario, sexo, codigoDepartamento, codigoFilial) values ('Barby', 'Kantor', 'bkantorm@chicagotribune.com', '2017-08-09', '9', 'masculino', 23, 23);

insert into funcionario (primeiroNome, ultimoNome, endereco, dataNascimento, salario, sexo, codigoDepartamento, codigoFilial) values ('Bibbie', 'Roderick', 'broderickn@google.com.au', '2017-08-28', '4247', 'feminino', 24, 24);

insert into funcionario (primeiroNome, ultimoNome, endereco, dataNascimento, salario, sexo, codigoDepartamento, codigoFilial) values ('Steward', 'felip', 'sfelipo@youtu.be', '2020-10-14', '68', 'masculino', 25, 25);

insert into funcionario (primeiroNome, ultimoNome, endereco, dataNascimento, salario, sexo, codigoDepartamento, codigoFilial) values ('Giovanni', 'Rizziello', 'grizziellop@friendfeed.com', '2020-08-31', '66540', 'feminino', 26, 26);

insert into funcionario (primeiroNome, ultimoNome, endereco, dataNascimento, salario, sexo, codigoDepartamento, codigoFilial) values ('Laurene', 'Challener', 'lchallenerq@123-reg.co.uk', '2019-03-01', '190', 'masculino', 27, 27);

insert into funcionario (primeiroNome, ultimoNome, endereco, dataNascimento, salario, sexo, codigoDepartamento, codigoFilial) values ('Hildagard', 'Bebis', 'hbebisr@msu.edu', '2021-11-25', '13', 'feminino', 28, 28);

insert into funcionario (primeiroNome, ultimoNome, endereco, dataNascimento, salario, sexo, codigoDepartamento, codigoFilial) values ('Marilee', 'Esley', 'mesleys@odnoklassniki.ru', '2017-04-06', '8', 'masculino', 29, 29);

insert into funcionario (primeiroNome, ultimoNome, endereco, dataNascimento, salario, sexo, codigoDepartamento, codigoFilial) values ('Hermine', 'Ferretti', 'hferrettit@dailymail.co.uk', '2022-01-12', '33353', 'feminino', 30, 30);

insert into funcionario (primeiroNome, ultimoNome, endereco, dataNascimento, salario, sexo, codigoDepartamento, codigoFilial) values ('Barry', 'Maitland', 'bmaitlandu@phoca.cz', '2017-09-30', '0', 'masculino', 1, 31);

insert into funcionario (primeiroNome, ultimoNome, endereco, dataNascimento, salario, sexo, codigoDepartamento, codigoFilial) values ('Kim', 'Houlson', 'khoulsonv@cpanel.net', '2019-01-20', '993', 'feminino', 2, 32);

insert into funcionario (primeiroNome, ultimoNome, endereco, dataNascimento, salario, sexo, codigoDepartamento, codigoFilial) values ('Steven', 'Bromage', 'sbromagew@list-manage.com', '2022-06-20', '2', 'masculino', 3, 33);

insert into funcionario (primeiroNome, ultimoNome, endereco, dataNascimento, salario, sexo, codigoDepartamento, codigoFilial) values ('Joanna', 'Farnes', 'jfarnesx@github.io', '2021-03-23', '749', 'feminino', 4, 34);

insert into funcionario (primeiroNome, ultimoNome, endereco, dataNascimento, salario, sexo, codigoDepartamento, codigoFilial) values ('Cybil', 'Blaisdell', 'cblaisdelly@people.com.cn', '2020-04-20', '9', 'masculino', 5, 35);

insert into funcionario (primeiroNome, ultimoNome, endereco, dataNascimento, salario, sexo, codigoDepartamento, codigoFilial) values ('Tymothy', 'Treweela', 'ttreweelaz@irs.gov', '2021-08-15', '88519', 'feminino', 6, 36);

insert into funcionario (primeiroNome, ultimoNome, endereco, dataNascimento, salario, sexo, codigoDepartamento, codigoFilial) values ('Ingram', 'Aymes', 'iaymes10@hatena.ne.jp', '2019-05-30', '315', 'masculino', 7, 37);

insert into funcionario (primeiroNome, ultimoNome, endereco, dataNascimento, salario, sexo, codigoDepartamento, codigoFilial) values ('Gaby', 'Daughtry', 'gdaughtry11@nhs.uk', '2019-11-01', '369', 'feminino', 8, 38);

insert into funcionario (primeiroNome, ultimoNome, endereco, dataNascimento, salario, sexo, codigoDepartamento, codigoFilial) values ('Lotty', 'Pontin', 'lpontin12@fc2.com', '2018-07-16', '5', 'masculino', 9, 39);

insert into funcionario (primeiroNome, ultimoNome, endereco, dataNascimento, salario, sexo, codigoDepartamento, codigoFilial) values ('Dill', 'McGiff', 'dmcgiff13@dagondesign.com', '2019-03-13', '28605', 'feminino', 10, 40);

insert into funcionario (primeiroNome, ultimoNome, endereco, dataNascimento, salario, sexo, codigoDepartamento, codigoFilial) values ('Mireille', 'Chaffin', 'mchaffin14@t.co', '2020-06-27', '240', 'masculino', 11, 41);

insert into funcionario (primeiroNome, ultimoNome, endereco, dataNascimento, salario, sexo, codigoDepartamento, codigoFilial) values ('Karla', 'Bernolet', 'kbernolet15@symantec.com', '2021-09-19', '153', 'feminino', 12, 42);

insert into funcionario (primeiroNome, ultimoNome, endereco, dataNascimento, salario, sexo, codigoDepartamento, codigoFilial) values ('Enrica', 'Lafond', 'elafond16@pagesperso-orange.fr', '2021-10-11', '7', 'masculino', 13, 43);

insert into funcionario (primeiroNome, ultimoNome, endereco, dataNascimento, salario, sexo, codigoDepartamento, codigoFilial) values ('Cyndy', 'Rown', 'crown17@stumbleupon.com', '2019-03-19', '06903', 'feminino', 14, 44);

insert into funcionario (primeiroNome, ultimoNome, endereco, dataNascimento, salario, sexo, codigoDepartamento, codigoFilial) values ('Camala', 'Raddenbury', 'craddenbury18@geocities.jp', '2021-05-19', '133', 'masculino', 15, 45);

insert into funcionario (primeiroNome, ultimoNome, endereco, dataNascimento, salario, sexo, codigoDepartamento, codigoFilial) values ('Tabbitha', 'McGragh', 'tmcgragh19@hostgator.com', '2019-08-22', '1614', 'feminino', 16, 46);

insert into funcionario (primeiroNome, ultimoNome, endereco, dataNascimento, salario, sexo, codigoDepartamento, codigoFilial) values ('Abagael', 'Cooch', 'acooch1a@google.ca', '2022-05-15', '59', 'masculino', 17, 47);

insert into funcionario (primeiroNome, ultimoNome, endereco, dataNascimento, salario, sexo, codigoDepartamento, codigoFilial) values ('Cheston', 'Quiney', 'cquiney1b@time.com', '2020-06-12', '7108', 'feminino', 18, 48);

insert into funcionario (primeiroNome, ultimoNome, endereco, dataNascimento, salario, sexo, codigoDepartamento, codigoFilial) values ('Sallyann', 'Hounihan', 'shounihan1c@1688.com', '2018-09-16', '70026', 'masculino', 19, 49);

insert into funcionario (primeiroNome, ultimoNome, endereco, dataNascimento, salario, sexo, codigoDepartamento, codigoFilial) values ('Ethelda', 'Tibols', 'etibols1d@blogs.com', '2019-06-10', '97', 'feminino', 20, 50);

insert into funcionario (primeiroNome, ultimoNome, endereco, dataNascimento, salario, sexo, codigoDepartamento, codigoFilial) values ('Harrie', 'Wasling', 'hwasling1e@si.edu', '2017-11-21', '24417', 'masculino', 21, 51);

insert into funcionario (primeiroNome, ultimoNome, endereco, dataNascimento, salario, sexo, codigoDepartamento, codigoFilial) values ('Lyn', 'Evesque', 'levesque1f@usatoday.com', '2019-08-30', '211', 'feminino', 22, 52);

insert into funcionario (primeiroNome, ultimoNome, endereco, dataNascimento, salario, sexo, codigoDepartamento, codigoFilial) values ('Natalie', 'Sangar', 'nsangar1g@tinyurl.com', '2019-10-16', '4', 'masculino', 23, 53);

insert into funcionario (primeiroNome, ultimoNome, endereco, dataNascimento, salario, sexo, codigoDepartamento, codigoFilial) values ('Arnold', 'Ivetts', 'aivetts1h@homestead.com', '2017-07-31', '660', 'feminino', 24, 54);

insert into funcionario (primeiroNome, ultimoNome, endereco, dataNascimento, salario, sexo, codigoDepartamento, codigoFilial) values ('Abelard', 'Heare', 'aheare1i@yahoo.com', '2020-05-22', '43', 'masculino', 25, 55);

insert into funcionario (primeiroNome, ultimoNome, endereco, dataNascimento, salario, sexo, codigoDepartamento, codigoFilial) values ('Ulberto', 'McIndrew', 'umcindrew1j@domainmarket.com', '2019-09-13', '3339', 'feminino', 26, 56);

insert into funcionario (primeiroNome, ultimoNome, endereco, dataNascimento, salario, sexo, codigoDepartamento, codigoFilial) values ('Eric', 'Dumsday', 'edumsday1k@independent.co.uk', '2017-07-19', '9006', 'masculino', 27, 57);

insert into funcionario (primeiroNome, ultimoNome, endereco, dataNascimento, salario, sexo, codigoDepartamento, codigoFilial) values ('Jesse', 'Sefton', 'jsefton1l@behance.net', '2019-06-20', '167', 'feminino', 28, 58);

insert into funcionario (primeiroNome, ultimoNome, endereco, dataNascimento, salario, sexo, codigoDepartamento, codigoFilial) values ('Jori', 'Oldnall', 'joldnall1m@virginia.edu', '2018-03-30', '8694', 'masculino', 29, 59);

insert into funcionario (primeiroNome, ultimoNome, endereco, dataNascimento, salario, sexo, codigoDepartamento, codigoFilial) values ('Natty', 'Cooch', 'ncooch1n@patch.com', '2020-10-08', '710', 'feminino', 30, 60);

insert into funcionario (primeiroNome, ultimoNome, endereco, dataNascimento, salario, sexo, codigoDepartamento, codigoFilial) values ('Kippie', 'Gehrels', 'kgehrels1o@zdnet.com', '2020-06-02', '453', 'masculino', 1, 1);

insert into funcionario (primeiroNome, ultimoNome, endereco, dataNascimento, salario, sexo, codigoDepartamento, codigoFilial) values ('Jacquenette', 'Fackney', 'jfackney1p@trellian.com', '2017-04-15', '710', 'feminino', 2, 2);

insert into funcionario (primeiroNome, ultimoNome, endereco, dataNascimento, salario, sexo, codigoDepartamento, codigoFilial) values ('Hayden', 'Beevor', 'hbeevor1q@auda.org.au', '2019-12-23', '97', 'masculino', 3, 3);

insert into funcionario (primeiroNome, ultimoNome, endereco, dataNascimento, salario, sexo, codigoDepartamento, codigoFilial) values ('Pen', 'Yelland', 'pyelland1r@adobe.com', '2021-05-01', '9546', 'feminino', 4, 4);

insert into funcionario (primeiroNome, ultimoNome, endereco, dataNascimento, salario, sexo, codigoDepartamento, codigoFilial) values ('Kyle', 'Reuss', 'kreuss1s@blogtalkradio.com', '2019-02-24', '4', 'masculino', 5, 5);

insert into funcionario (primeiroNome, ultimoNome, endereco, dataNascimento, salario, sexo, codigoDepartamento, codigoFilial) values ('Pru', 'Ponter', 'pponter1t@technorati.com', '2017-11-26', '339', 'feminino', 6, 6);

insert into funcionario (primeiroNome, ultimoNome, endereco, dataNascimento, salario, sexo, codigoDepartamento, codigoFilial) values ('Hinze', 'Forcade', 'hforcade1u@sohu.com', '2018-09-05', '52461', 'masculino', 7, 7);

insert into funcionario (primeiroNome, ultimoNome, endereco, dataNascimento, salario, sexo, codigoDepartamento, codigoFilial) values ('Rosella', 'Rolph', 'rrolph1v@sitemeter.com', '2019-09-13', '15444', 'feminino', 8, 8);

insert into funcionario (primeiroNome, ultimoNome, endereco, dataNascimento, salario, sexo, codigoDepartamento, codigoFilial) values ('Maurizia', 'Mallia', 'mmallia1w@sun.com', '2017-11-02', '1', 'masculino', 9, 9);

insert into funcionario (primeiroNome, ultimoNome, endereco, dataNascimento, salario, sexo, codigoDepartamento, codigoFilial) values ('Horton', 'MacGiffin', 'hmacgiffin1x@51.la', '2019-07-13', '64598', 'feminino', 10, 10);

insert into funcionario (primeiroNome, ultimoNome, endereco, dataNascimento, salario, sexo, codigoDepartamento, codigoFilial) values ('Eadie', 'Beeble', 'ebeeble1y@ezinearticles.com', '2017-10-31', '88172', 'masculino', 11, 11);

insert into funcionario (primeiroNome, ultimoNome, endereco, dataNascimento, salario, sexo, codigoDepartamento, codigoFilial) values ('Hi', 'Maginn', 'hmaginn1z@globo.com', '2018-02-01', '0', 'feminino', 12, 12);

insert into funcionario (primeiroNome, ultimoNome, endereco, dataNascimento, salario, sexo, codigoDepartamento, codigoFilial) values ('Hilary', 'Jancik', 'hjancik20@sphinn.com', '2022-04-11', '1', 'masculino', 13, 13);

insert into funcionario (primeiroNome, ultimoNome, endereco, dataNascimento, salario, sexo, codigoDepartamento, codigoFilial) values ('Leena', 'Izachik', 'lizachik21@addtoany.com', '2021-06-14', '0226', 'feminino', 14, 14);

insert into funcionario (primeiroNome, ultimoNome, endereco, dataNascimento, salario, sexo, codigoDepartamento, codigoFilial) values ('Helenelizabeth', 'Wilden', 'hwilden22@blog.com', '2020-03-04', '715', 'masculino', 15, 15);

insert into funcionario (primeiroNome, ultimoNome, endereco, dataNascimento, salario, sexo, codigoDepartamento, codigoFilial) values ('Olympia', 'Sneezem', 'osneezem23@cbsnews.com', '2020-04-16', '341', 'feminino', 16, 16);

insert into funcionario (primeiroNome, ultimoNome, endereco, dataNascimento, salario, sexo, codigoDepartamento, codigoFilial) values ('Biddie', 'MacCombe', 'bmaccombe24@friendfeed.com', '2021-12-21', '0', 'masculino', 17, 17);

insert into funcionario (primeiroNome, ultimoNome, endereco, dataNascimento, salario, sexo, codigoDepartamento, codigoFilial) values ('Brett', 'Routley', 'broutley25@netscape.com', '2021-01-17', '6', 'feminino', 18, 18);

insert into funcionario (primeiroNome, ultimoNome, endereco, dataNascimento, salario, sexo, codigoDepartamento, codigoFilial) values ('Sayers', 'Lickorish', 'slickorish26@google.es', '2019-04-02', '30', 'masculino', 19, 19);

insert into funcionario (primeiroNome, ultimoNome, endereco, dataNascimento, salario, sexo, codigoDepartamento, codigoFilial) values ('Cointon', 'Redish', 'credish27@facebook.com', '2019-07-26', '4', 'feminino', 20, 20);

insert into funcionario (primeiroNome, ultimoNome, endereco, dataNascimento, salario, sexo, codigoDepartamento, codigoFilial) values ('Delmore', 'Braam', 'dbraam28@nps.gov', '2018-01-30', '5363', 'masculino', 21, 21);

insert into funcionario (primeiroNome, ultimoNome, endereco, dataNascimento, salario, sexo, codigoDepartamento, codigoFilial) values ('Emanuele', 'Jeays', 'ejeays29@over-blog.com', '2019-12-08', '892', 'feminino', 22, 22);

insert into funcionario (primeiroNome, ultimoNome, endereco, dataNascimento, salario, sexo, codigoDepartamento, codigoFilial) values ('Kesley', 'Scotting', 'kscotting2a@guardian.co.uk', '2020-01-20', '85', 'masculino', 23, 23);

insert into funcionario (primeiroNome, ultimoNome, endereco, dataNascimento, salario, sexo, codigoDepartamento, codigoFilial) values ('Harvey', 'Della Scala', 'hdellascala2b@arstechnica.com', '2021-01-02', '0', 'feminino', 24, 24);

insert into funcionario (primeiroNome, ultimoNome, endereco, dataNascimento, salario, sexo, codigoDepartamento, codigoFilial) values ('Neill', 'Candish', 'ncandish2c@shareasale.com', '2020-07-26', '86', 'masculino', 25, 25);

insert into funcionario (primeiroNome, ultimoNome, endereco, dataNascimento, salario, sexo, codigoDepartamento, codigoFilial) values ('Dotty', 'Bangiard', 'dbangiard2d@stumbleupon.com', '2020-01-12', '6', 'feminino', 26, 26);

insert into funcionario (primeiroNome, ultimoNome, endereco, dataNascimento, salario, sexo, codigoDepartamento, codigoFilial) values ('Salvidor', 'Maxstead', 'smaxstead2e@friendfeed.com', '2018-10-27', '466', 'masculino', 27, 27);

insert into funcionario (primeiroNome, ultimoNome, endereco, dataNascimento, salario, sexo, codigoDepartamento, codigoFilial) values ('Calli', 'Baggett', 'cbaggett2f@youtube.com', '2019-01-27', '54', 'feminino', 28, 28);

insert into funcionario (primeiroNome, ultimoNome, endereco, dataNascimento, salario, sexo, codigoDepartamento, codigoFilial) values ('Ingmar', 'Carvilla', 'icarvilla2g@addthis.com', '2017-07-28', '44', 'masculino', 29, 29);

insert into funcionario (primeiroNome, ultimoNome, endereco, dataNascimento, salario, sexo, codigoDepartamento, codigoFilial) values ('Rabi', 'Dorgon', 'rdorgon2h@dailymotion.com', '2018-07-02', '72', 'feminino', 30, 30);

insert into funcionario (primeiroNome, ultimoNome, endereco, dataNascimento, salario, sexo, codigoDepartamento, codigoFilial) values ('Mickey', 'Matkovic', 'mmatkovic2i@devhub.com', '2018-04-13', '212', 'masculino', 1, 31);

insert into funcionario (primeiroNome, ultimoNome, endereco, dataNascimento, salario, sexo, codigoDepartamento, codigoFilial) values ('Gracia', 'Lamberts', 'glamberts2j@economist.com', '2021-02-25', '21341', 'feminino', 2, 32);

insert into funcionario (primeiroNome, ultimoNome, endereco, dataNascimento, salario, sexo, codigoDepartamento, codigoFilial) values ('Sollie', 'Lewins', 'slewins2k@illinois.edu', '2017-05-16', '12438', 'masculino', 3, 33);

insert into funcionario (primeiroNome, ultimoNome, endereco, dataNascimento, salario, sexo, codigoDepartamento, codigoFilial) values ('Reinold', 'Coghill', 'rcoghill2l@smugmug.com', '2020-08-25', '24159', 'feminino', 4, 34);

insert into funcionario (primeiroNome, ultimoNome, endereco, dataNascimento, salario, sexo, codigoDepartamento, codigoFilial) values ('Fara', 'Blew', 'fblew2m@unc.edu', '2017-08-04', '5537', 'masculino', 5, 35);

insert into funcionario (primeiroNome, ultimoNome, endereco, dataNascimento, salario, sexo, codigoDepartamento, codigoFilial) values ('Parsifal', 'De Benedetti', 'pdebenedetti2n@google.cn', '2017-04-27', '904', 'feminino', 6, 36);

insert into funcionario (primeiroNome, ultimoNome, endereco, dataNascimento, salario, sexo, codigoDepartamento, codigoFilial) values ('Lorain', 'Smorfit', 'lsmorfit2o@wix.com', '2019-11-20', '3', 'masculino', 7, 37);

insert into funcionario (primeiroNome, ultimoNome, endereco, dataNascimento, salario, sexo, codigoDepartamento, codigoFilial) values ('Celinda', 'Praundl', 'cpraundl2p@php.net', '2020-05-27', '8354', 'feminino', 8, 38);

insert into funcionario (primeiroNome, ultimoNome, endereco, dataNascimento, salario, sexo, codigoDepartamento, codigoFilial) values ('Jesselyn', 'Szymonowicz', 'jszymonowicz2q@w3.org', '2018-11-23', '03119', 'masculino', 9, 39);

insert into funcionario (primeiroNome, ultimoNome, endereco, dataNascimento, salario, sexo, codigoDepartamento, codigoFilial) values ('Matthieu', 'Backler', 'mbackler2r@youku.com', '2022-04-09', '645', 'feminino', 10, 40);

insert into funcionario (primeiroNome, ultimoNome, endereco, dataNascimento, salario, sexo, codigoDepartamento, codigoFilial) values ('Alexi', 'Crellim', 'acrellim2s@over-blog.com', '2020-03-11', '53670', 'masculino', 11, 41);

insert into funcionario (primeiroNome, ultimoNome, endereco, dataNascimento, salario, sexo, codigoDepartamento, codigoFilial) values ('Tanney', 'Simkins', 'tsimkins2t@businessweek.com', '2020-06-19', '04', 'feminino', 12, 42);

insert into funcionario (primeiroNome, ultimoNome, endereco, dataNascimento, salario, sexo, codigoDepartamento, codigoFilial) values ('Lizzie', 'Sima', 'lsima2u@creativecommons.org', '2020-05-15', '59', 'masculino', 13, 43);

insert into funcionario (primeiroNome, ultimoNome, endereco, dataNascimento, salario, sexo, codigoDepartamento, codigoFilial) values ('Arda', 'Sheekey', 'asheekey2v@webs.com', '2021-07-11', '11735', 'feminino', 14, 44);

insert into funcionario (primeiroNome, ultimoNome, endereco, dataNascimento, salario, sexo, codigoDepartamento, codigoFilial) values ('Kerwin', 'Jecock', 'kjecock2w@un.org', '2020-05-11', '127', 'masculino', 15, 45);

insert into funcionario (primeiroNome, ultimoNome, endereco, dataNascimento, salario, sexo, codigoDepartamento, codigoFilial) values ('Darya', 'Uccello', 'duccello2x@indiatimes.com', '2020-11-02', '40', 'feminino', 16, 46);

insert into funcionario (primeiroNome, ultimoNome, endereco, dataNascimento, salario, sexo, codigoDepartamento, codigoFilial) values ('Adelle', 'Harewood', 'aharewood2y@flickr.com', '2018-04-17', '871', 'masculino', 17, 47);

insert into funcionario (primeiroNome, ultimoNome, endereco, dataNascimento, salario, sexo, codigoDepartamento, codigoFilial) values ('Griffin', 'Hugland', 'ghugland2z@epa.gov', '2019-03-15', '75', 'feminino', 18, 48);

insert into funcionario (primeiroNome, ultimoNome, endereco, dataNascimento, salario, sexo, codigoDepartamento, codigoFilial) values ('Claudia', 'Naisey', 'cnaisey30@ted.com', '2021-03-12', '82', 'masculino', 19, 49);

insert into funcionario (primeiroNome, ultimoNome, endereco, dataNascimento, salario, sexo, codigoDepartamento, codigoFilial) values ('Moritz', 'Petera', 'mpetera31@joomla.org', '2018-12-04', '15367', 'feminino', 20, 50);

insert into funcionario (primeiroNome, ultimoNome, endereco, dataNascimento, salario, sexo, codigoDepartamento, codigoFilial) values ('Genevieve', 'Bedow', 'gbedow32@indiatimes.com', '2018-12-21', '3390', 'masculino', 21, 51);

insert into funcionario (primeiroNome, ultimoNome, endereco, dataNascimento, salario, sexo, codigoDepartamento, codigoFilial) values ('Teodoro', 'Stollberger', 'tstollberger33@fema.gov', '2017-05-01', '07906', 'feminino', 22, 52);

insert into funcionario (primeiroNome, ultimoNome, endereco, dataNascimento, salario, sexo, codigoDepartamento, codigoFilial) values ('Elane', 'Corstorphine', 'ecorstorphine34@indiatimes.com', '2019-01-29', '40', 'masculino', 23, 53);

insert into funcionario (primeiroNome, ultimoNome, endereco, dataNascimento, salario, sexo, codigoDepartamento, codigoFilial) values ('Dallis', 'Jorgensen', 'djorgensen35@utexas.edu', '2021-10-12', '7', 'feminino', 24, 54);

insert into funcionario (primeiroNome, ultimoNome, endereco, dataNascimento, salario, sexo, codigoDepartamento, codigoFilial) values ('Floris', 'La Wille', 'flawille36@smugmug.com', '2021-04-14', '28153', 'masculino', 25, 55);

insert into funcionario (primeiroNome, ultimoNome, endereco, dataNascimento, salario, sexo, codigoDepartamento, codigoFilial) values ('Eden', 'Stiff', 'estiff37@china.com.cn', '2020-03-13', '9', 'feminino', 26, 56);

insert into funcionario (primeiroNome, ultimoNome, endereco, dataNascimento, salario, sexo, codigoDepartamento, codigoFilial) values ('Augustin', 'Fessions', 'afessions38@hubpages.com', '2019-12-03', '7', 'masculino', 27, 57);

insert into funcionario (primeiroNome, ultimoNome, endereco, dataNascimento, salario, sexo, codigoDepartamento, codigoFilial) values ('Bancroft', 'Cowburn', 'bcowburn39@qq.com', '2020-04-29', '2002', 'feminino', 28, 58);

insert into funcionario (primeiroNome, ultimoNome, endereco, dataNascimento, salario, sexo, codigoDepartamento, codigoFilial) values ('Junie', 'Wiffler', 'jwiffler3a@lycos.com', '2020-11-11', '8', 'masculino', 29, 59);

insert into funcionario (primeiroNome, ultimoNome, endereco, dataNascimento, salario, sexo, codigoDepartamento, codigoFilial) values ('Massimiliano', 'Swatradge', 'mswatradge3b@intel.com', '2019-02-07', '8957', 'feminino', 30, 60);


### Tabela Alugar


insert into alugar (dataInicial, dataFinal, custo, caucao, nicCliente, idServicoAluguer, matriculaVeiculo, codigoFilial) values ('2020-10-03', '2022-04-15', 215.26, 97.28, 1, 1, 1, 1);

insert into alugar (dataInicial, dataFinal, custo, caucao, nicCliente, idServicoAluguer, matriculaVeiculo, codigoFilial) values ('2020-12-27', '2022-06-13', 47.06, 46.81, 2, 2, 2, 2);

insert into alugar (dataInicial, dataFinal, custo, caucao, nicCliente, idServicoAluguer, matriculaVeiculo, codigoFilial) values ('2020-09-27', '2021-11-18', 38.89, 42.67, 3, 3, 3, 3);

insert into alugar (dataInicial, dataFinal, custo, caucao, nicCliente, idServicoAluguer, matriculaVeiculo, codigoFilial) values ('2020-09-18', '2022-02-11', 157.1, 41.15, 4, 4, 4, 4);

insert into alugar (dataInicial, dataFinal, custo, caucao, nicCliente, idServicoAluguer, matriculaVeiculo, codigoFilial) values ('2020-08-12', '2021-12-21', 83.42, 41.51, 5, 5, 5, 5);

insert into alugar (dataInicial, dataFinal, custo, caucao, nicCliente, idServicoAluguer, matriculaVeiculo, codigoFilial) values ('2020-11-13', '2022-02-19', 278.12, 67.27, 6, 6, 6, 6);

insert into alugar (dataInicial, dataFinal, custo, caucao, nicCliente, idServicoAluguer, matriculaVeiculo, codigoFilial) values ('2020-07-27', '2022-02-05', 114.0, 98.54, 7, 7, 7, 7);

insert into alugar (dataInicial, dataFinal, custo, caucao, nicCliente, idServicoAluguer, matriculaVeiculo, codigoFilial) values ('2020-07-13', '2021-06-20', 39.53, 59.91, 8, 1, 8, 8);

insert into alugar (dataInicial, dataFinal, custo, caucao, nicCliente, idServicoAluguer, matriculaVeiculo, codigoFilial) values ('2020-07-22', '2021-08-02', 233.56, 94.75, 9, 2, 9, 9);

insert into alugar (dataInicial, dataFinal, custo, caucao, nicCliente, idServicoAluguer, matriculaVeiculo, codigoFilial) values ('2020-07-07', '2021-08-20', 5.14, 55.32, 10, 3, 10, 10);

insert into alugar (dataInicial, dataFinal, custo, caucao, nicCliente, idServicoAluguer, matriculaVeiculo, codigoFilial) values ('2020-07-31', '2022-05-19', 179.6, 85.9, 11, 4, 1, 11);

insert into alugar (dataInicial, dataFinal, custo, caucao, nicCliente, idServicoAluguer, matriculaVeiculo, codigoFilial) values ('2020-10-11', '2021-11-22', 28.06, 83.87, 12, 5, 2, 12);

insert into alugar (dataInicial, dataFinal, custo, caucao, nicCliente, idServicoAluguer, matriculaVeiculo, codigoFilial) values ('2020-07-17', '2021-11-03', 133.37, 74.36, 13, 6, 3, 13);

insert into alugar (dataInicial, dataFinal, custo, caucao, nicCliente, idServicoAluguer, matriculaVeiculo, codigoFilial) values ('2020-07-12', '2022-01-02', 111.05, 41.93, 14, 7, 4, 14);

insert into alugar (dataInicial, dataFinal, custo, caucao, nicCliente, idServicoAluguer, matriculaVeiculo, codigoFilial) values ('2021-01-04', '2021-11-27', 43.71, 80.84, 15, 1, 5, 15);

insert into alugar (dataInicial, dataFinal, custo, caucao, nicCliente, idServicoAluguer, matriculaVeiculo, codigoFilial) values ('2020-12-20', '2022-05-09', 184.16, 35.83, 16, 2, 6, 16);

insert into alugar (dataInicial, dataFinal, custo, caucao, nicCliente, idServicoAluguer, matriculaVeiculo, codigoFilial) values ('2020-10-15', '2022-03-30', 43.22, 56.07, 17, 3, 7, 17);

insert into alugar (dataInicial, dataFinal, custo, caucao, nicCliente, idServicoAluguer, matriculaVeiculo, codigoFilial) values ('2020-09-11', '2022-01-08', 166.08, 35.36, 18, 4, 8, 18);

insert into alugar (dataInicial, dataFinal, custo, caucao, nicCliente, idServicoAluguer, matriculaVeiculo, codigoFilial) values ('2020-08-27', '2022-05-09', 186.76, 8.56, 19, 5, 9, 19);

insert into alugar (dataInicial, dataFinal, custo, caucao, nicCliente, idServicoAluguer, matriculaVeiculo, codigoFilial) values ('2020-06-24', '2021-07-13', 101.68, 24.03, 20, 6, 10, 20);

insert into alugar (dataInicial, dataFinal, custo, caucao, nicCliente, idServicoAluguer, matriculaVeiculo, codigoFilial) values ('2020-12-10', '2021-08-25', 13.51, 13.93, 21, 7, 1, 21);

insert into alugar (dataInicial, dataFinal, custo, caucao, nicCliente, idServicoAluguer, matriculaVeiculo, codigoFilial) values ('2020-08-31', '2021-07-12', 241.53, 36.75, 22, 1, 2, 22);

insert into alugar (dataInicial, dataFinal, custo, caucao, nicCliente, idServicoAluguer, matriculaVeiculo, codigoFilial) values ('2020-11-20', '2022-05-11', 240.66, 78.85, 23, 2, 3, 23);

insert into alugar (dataInicial, dataFinal, custo, caucao, nicCliente, idServicoAluguer, matriculaVeiculo, codigoFilial) values ('2020-10-17', '2021-06-29', 15.63, 28.55, 24, 3, 4, 24);

insert into alugar (dataInicial, dataFinal, custo, caucao, nicCliente, idServicoAluguer, matriculaVeiculo, codigoFilial) values ('2020-09-22', '2022-05-15', 51.34, 97.45, 25, 4, 5, 25);

insert into alugar (dataInicial, dataFinal, custo, caucao, nicCliente, idServicoAluguer, matriculaVeiculo, codigoFilial) values ('2020-08-13', '2021-12-17', 42.08, 49.33, 26, 5, 6, 26);

insert into alugar (dataInicial, dataFinal, custo, caucao, nicCliente, idServicoAluguer, matriculaVeiculo, codigoFilial) values ('2020-11-13', '2022-02-12', 267.48, 77.42, 27, 6, 7, 27);

insert into alugar (dataInicial, dataFinal, custo, caucao, nicCliente, idServicoAluguer, matriculaVeiculo, codigoFilial) values ('2020-11-11', '2021-12-31', 47.51, 29.85, 28, 7, 8, 28);

insert into alugar (dataInicial, dataFinal, custo, caucao, nicCliente, idServicoAluguer, matriculaVeiculo, codigoFilial) values ('2020-12-18', '2021-11-08', 19.78, 16.69, 29, 1, 9, 29);

insert into alugar (dataInicial, dataFinal, custo, caucao, nicCliente, idServicoAluguer, matriculaVeiculo, codigoFilial) values ('2020-07-04', '2021-12-01', 74.29, 45.58, 30, 2, 10, 30);

insert into alugar (dataInicial, dataFinal, custo, caucao, nicCliente, idServicoAluguer, matriculaVeiculo, codigoFilial) values ('2020-10-10', '2022-04-10', 253.0, 89.63, 31, 3, 1, 31);

insert into alugar (dataInicial, dataFinal, custo, caucao, nicCliente, idServicoAluguer, matriculaVeiculo, codigoFilial) values ('2020-11-18', '2022-01-04', 41.19, 23.98, 32, 4, 2, 32);

insert into alugar (dataInicial, dataFinal, custo, caucao, nicCliente, idServicoAluguer, matriculaVeiculo, codigoFilial) values ('2020-12-27', '2022-03-29', 237.09, 44.81, 33, 5, 3, 33);

insert into alugar (dataInicial, dataFinal, custo, caucao, nicCliente, idServicoAluguer, matriculaVeiculo, codigoFilial) values ('2020-08-22', '2022-04-26', 105.61, 89.61, 34, 6, 4, 34);

insert into alugar (dataInicial, dataFinal, custo, caucao, nicCliente, idServicoAluguer, matriculaVeiculo, codigoFilial) values ('2020-07-03', '2021-07-03', 238.33, 31.38, 35, 7, 5, 35);

insert into alugar (dataInicial, dataFinal, custo, caucao, nicCliente, idServicoAluguer, matriculaVeiculo, codigoFilial) values ('2020-12-11', '2021-07-25', 199.24, 42.21, 36, 1, 6, 36);

insert into alugar (dataInicial, dataFinal, custo, caucao, nicCliente, idServicoAluguer, matriculaVeiculo, codigoFilial) values ('2021-01-03', '2022-05-18', 125.88, 40.63, 37, 2, 7, 37);

insert into alugar (dataInicial, dataFinal, custo, caucao, nicCliente, idServicoAluguer, matriculaVeiculo, codigoFilial) values ('2020-07-09', '2022-01-27', 42.16, 21.1, 38, 3, 8, 38);

insert into alugar (dataInicial, dataFinal, custo, caucao, nicCliente, idServicoAluguer, matriculaVeiculo, codigoFilial) values ('2020-09-15', '2022-06-10', 89.46, 72.05, 39, 4, 9, 39);

insert into alugar (dataInicial, dataFinal, custo, caucao, nicCliente, idServicoAluguer, matriculaVeiculo, codigoFilial) values ('2020-08-22', '2022-03-11', 233.24, 70.86, 40, 5, 10, 40);

insert into alugar (dataInicial, dataFinal, custo, caucao, nicCliente, idServicoAluguer, matriculaVeiculo, codigoFilial) values ('2020-07-31', '2021-12-31', 228.05, 94.61, 1, 6, 1, 41);

insert into alugar (dataInicial, dataFinal, custo, caucao, nicCliente, idServicoAluguer, matriculaVeiculo, codigoFilial) values ('2020-11-27', '2022-06-04', 282.51, 50.94, 2, 7, 2, 42);

insert into alugar (dataInicial, dataFinal, custo, caucao, nicCliente, idServicoAluguer, matriculaVeiculo, codigoFilial) values ('2020-08-30', '2022-02-22', 241.25, 69.9, 3, 1, 3, 43);

insert into alugar (dataInicial, dataFinal, custo, caucao, nicCliente, idServicoAluguer, matriculaVeiculo, codigoFilial) values ('2020-10-06', '2021-06-27', 12.45, 14.36, 4, 2, 4, 44);

insert into alugar (dataInicial, dataFinal, custo, caucao, nicCliente, idServicoAluguer, matriculaVeiculo, codigoFilial) values ('2020-09-30', '2021-06-08', 2.4, 49.99, 5, 3, 5, 45);

insert into alugar (dataInicial, dataFinal, custo, caucao, nicCliente, idServicoAluguer, matriculaVeiculo, codigoFilial) values ('2020-12-06', '2021-10-08', 216.04, 3.22, 6, 4, 6, 46);

insert into alugar (dataInicial, dataFinal, custo, caucao, nicCliente, idServicoAluguer, matriculaVeiculo, codigoFilial) values ('2020-12-25', '2022-04-20', 9.96, 75.57, 7, 5, 7, 47);

insert into alugar (dataInicial, dataFinal, custo, caucao, nicCliente, idServicoAluguer, matriculaVeiculo, codigoFilial) values ('2020-09-07', '2021-08-24', 270.14, 26.76, 8, 6, 8, 48);

insert into alugar (dataInicial, dataFinal, custo, caucao, nicCliente, idServicoAluguer, matriculaVeiculo, codigoFilial) values ('2020-08-14', '2021-11-12', 230.43, 36.47, 9, 7, 9, 49);

insert into alugar (dataInicial, dataFinal, custo, caucao, nicCliente, idServicoAluguer, matriculaVeiculo, codigoFilial) values ('2020-07-20', '2021-06-26', 1.69, 5.19, 10, 1, 10, 50);

insert into alugar (dataInicial, dataFinal, custo, caucao, nicCliente, idServicoAluguer, matriculaVeiculo, codigoFilial) values ('2020-11-13', '2021-11-03', 217.8, 77.02, 11, 2, 1, 51);

insert into alugar (dataInicial, dataFinal, custo, caucao, nicCliente, idServicoAluguer, matriculaVeiculo, codigoFilial) values ('2020-08-22', '2022-02-05', 211.33, 30.52, 12, 3, 2, 52);

insert into alugar (dataInicial, dataFinal, custo, caucao, nicCliente, idServicoAluguer, matriculaVeiculo, codigoFilial) values ('2020-08-29', '2022-03-25', 181.51, 64.86, 13, 4, 3, 53);

insert into alugar (dataInicial, dataFinal, custo, caucao, nicCliente, idServicoAluguer, matriculaVeiculo, codigoFilial) values ('2020-10-13', '2022-05-11', 195.84, 93.33, 14, 5, 4, 54);

insert into alugar (dataInicial, dataFinal, custo, caucao, nicCliente, idServicoAluguer, matriculaVeiculo, codigoFilial) values ('2020-11-30', '2021-09-17', 147.5, 13.84, 15, 6, 5, 55);

insert into alugar (dataInicial, dataFinal, custo, caucao, nicCliente, idServicoAluguer, matriculaVeiculo, codigoFilial) values ('2020-11-27', '2021-08-30', 31.94, 81.01, 16, 7, 6, 56);

insert into alugar (dataInicial, dataFinal, custo, caucao, nicCliente, idServicoAluguer, matriculaVeiculo, codigoFilial) values ('2020-11-02', '2022-02-07', 164.18, 55.3, 17, 1, 7, 57);

insert into alugar (dataInicial, dataFinal, custo, caucao, nicCliente, idServicoAluguer, matriculaVeiculo, codigoFilial) values ('2020-08-30', '2022-01-26', 68.92, 40.65, 18, 2, 8, 58);

insert into alugar (dataInicial, dataFinal, custo, caucao, nicCliente, idServicoAluguer, matriculaVeiculo, codigoFilial) values ('2020-09-28', '2022-01-25', 293.99, 41.83, 19, 3, 9, 59);

insert into alugar (dataInicial, dataFinal, custo, caucao, nicCliente, idServicoAluguer, matriculaVeiculo, codigoFilial) values ('2020-10-08', '2022-06-22', 162.9, 29.29, 20, 4, 10, 60);

insert into alugar (dataInicial, dataFinal, custo, caucao, nicCliente, idServicoAluguer, matriculaVeiculo, codigoFilial) values ('2020-07-07', '2021-07-11', 111.22, 43.67, 21, 5, 1, 1);

insert into alugar (dataInicial, dataFinal, custo, caucao, nicCliente, idServicoAluguer, matriculaVeiculo, codigoFilial) values ('2020-07-01', '2022-01-03', 268.47, 53.55, 22, 6, 2, 2);

insert into alugar (dataInicial, dataFinal, custo, caucao, nicCliente, idServicoAluguer, matriculaVeiculo, codigoFilial) values ('2020-11-10', '2021-06-10', 65.11, 16.75, 23, 7, 3, 3);

insert into alugar (dataInicial, dataFinal, custo, caucao, nicCliente, idServicoAluguer, matriculaVeiculo, codigoFilial) values ('2020-08-31', '2021-10-10', 238.4, 75.83, 24, 1, 4, 4);

insert into alugar (dataInicial, dataFinal, custo, caucao, nicCliente, idServicoAluguer, matriculaVeiculo, codigoFilial) values ('2020-09-11', '2022-01-30', 95.09, 47.37, 25, 2, 5, 5);

insert into alugar (dataInicial, dataFinal, custo, caucao, nicCliente, idServicoAluguer, matriculaVeiculo, codigoFilial) values ('2020-09-24', '2021-10-11', 217.51, 73.06, 26, 3, 6, 6);

insert into alugar (dataInicial, dataFinal, custo, caucao, nicCliente, idServicoAluguer, matriculaVeiculo, codigoFilial) values ('2020-07-22', '2022-04-27', 38.4, 6.91, 27, 4, 7, 7);

insert into alugar (dataInicial, dataFinal, custo, caucao, nicCliente, idServicoAluguer, matriculaVeiculo, codigoFilial) values ('2020-10-03', '2022-04-09', 280.78, 37.19, 28, 5, 8, 8);

insert into alugar (dataInicial, dataFinal, custo, caucao, nicCliente, idServicoAluguer, matriculaVeiculo, codigoFilial) values ('2020-11-24', '2022-06-23', 290.16, 71.76, 29, 6, 9, 9);

insert into alugar (dataInicial, dataFinal, custo, caucao, nicCliente, idServicoAluguer, matriculaVeiculo, codigoFilial) values ('2020-09-26', '2021-07-19', 125.5, 15.7, 30, 7, 10, 10);

insert into alugar (dataInicial, dataFinal, custo, caucao, nicCliente, idServicoAluguer, matriculaVeiculo, codigoFilial) values ('2020-07-14', '2021-11-22', 70.27, 75.97, 31, 1, 1, 11);

insert into alugar (dataInicial, dataFinal, custo, caucao, nicCliente, idServicoAluguer, matriculaVeiculo, codigoFilial) values ('2020-12-19', '2021-11-10', 246.78, 55.27, 32, 2, 2, 12);

insert into alugar (dataInicial, dataFinal, custo, caucao, nicCliente, idServicoAluguer, matriculaVeiculo, codigoFilial) values ('2020-12-23', '2021-09-25', 64.35, 13.89, 33, 3, 3, 13);

insert into alugar (dataInicial, dataFinal, custo, caucao, nicCliente, idServicoAluguer, matriculaVeiculo, codigoFilial) values ('2020-10-05', '2022-03-13', 118.77, 92.37, 34, 4, 4, 14);

insert into alugar (dataInicial, dataFinal, custo, caucao, nicCliente, idServicoAluguer, matriculaVeiculo, codigoFilial) values ('2020-06-25', '2021-12-07', 80.63, 96.8, 35, 5, 5, 15);

insert into alugar (dataInicial, dataFinal, custo, caucao, nicCliente, idServicoAluguer, matriculaVeiculo, codigoFilial) values ('2020-08-27', '2022-01-16', 280.69, 69.59, 36, 6, 6, 16);

insert into alugar (dataInicial, dataFinal, custo, caucao, nicCliente, idServicoAluguer, matriculaVeiculo, codigoFilial) values ('2020-10-26', '2022-04-09', 54.41, 79.93, 37, 7, 7, 17);

insert into alugar (dataInicial, dataFinal, custo, caucao, nicCliente, idServicoAluguer, matriculaVeiculo, codigoFilial) values ('2020-11-22', '2022-04-26', 187.78, 26.1, 38, 1, 8, 18);

insert into alugar (dataInicial, dataFinal, custo, caucao, nicCliente, idServicoAluguer, matriculaVeiculo, codigoFilial) values ('2020-12-02', '2022-03-27', 186.88, 5.06, 39, 2, 9, 19);

insert into alugar (dataInicial, dataFinal, custo, caucao, nicCliente, idServicoAluguer, matriculaVeiculo, codigoFilial) values ('2020-10-01', '2021-10-24', 115.97, 24.89, 40, 3, 10, 20);

insert into alugar (dataInicial, dataFinal, custo, caucao, nicCliente, idServicoAluguer, matriculaVeiculo, codigoFilial) values ('2020-08-14', '2021-08-14', 100.23, 54.43, 1, 4, 1, 21);

insert into alugar (dataInicial, dataFinal, custo, caucao, nicCliente, idServicoAluguer, matriculaVeiculo, codigoFilial) values ('2020-08-26', '2021-12-14', 59.93, 67.21, 2, 5, 2, 22);

insert into alugar (dataInicial, dataFinal, custo, caucao, nicCliente, idServicoAluguer, matriculaVeiculo, codigoFilial) values ('2020-12-07', '2021-10-28', 78.13, 98.89, 3, 6, 3, 23);

insert into alugar (dataInicial, dataFinal, custo, caucao, nicCliente, idServicoAluguer, matriculaVeiculo, codigoFilial) values ('2020-09-30', '2021-11-21', 149.02, 94.78, 4, 7, 4, 24);

insert into alugar (dataInicial, dataFinal, custo, caucao, nicCliente, idServicoAluguer, matriculaVeiculo, codigoFilial) values ('2020-09-02', '2022-06-27', 192.21, 4.61, 5, 1, 5, 25);

insert into alugar (dataInicial, dataFinal, custo, caucao, nicCliente, idServicoAluguer, matriculaVeiculo, codigoFilial) values ('2020-09-15', '2021-12-12', 96.98, 73.47, 6, 2, 6, 26);

insert into alugar (dataInicial, dataFinal, custo, caucao, nicCliente, idServicoAluguer, matriculaVeiculo, codigoFilial) values ('2020-07-19', '2022-03-16', 201.21, 47.3, 7, 3, 7, 27);

insert into alugar (dataInicial, dataFinal, custo, caucao, nicCliente, idServicoAluguer, matriculaVeiculo, codigoFilial) values ('2020-12-27', '2022-04-01', 185.33, 76.81, 8, 4, 8, 28);

insert into alugar (dataInicial, dataFinal, custo, caucao, nicCliente, idServicoAluguer, matriculaVeiculo, codigoFilial) values ('2020-09-23', '2021-08-19', 135.82, 89.0, 9, 5, 9, 29);

insert into alugar (dataInicial, dataFinal, custo, caucao, nicCliente, idServicoAluguer, matriculaVeiculo, codigoFilial) values ('2020-12-26', '2021-07-13', 286.16, 81.25, 10, 6, 10, 30);

insert into alugar (dataInicial, dataFinal, custo, caucao, nicCliente, idServicoAluguer, matriculaVeiculo, codigoFilial) values ('2020-11-25', '2022-04-20', 221.7, 75.51, 11, 7, 1, 31);

insert into alugar (dataInicial, dataFinal, custo, caucao, nicCliente, idServicoAluguer, matriculaVeiculo, codigoFilial) values ('2020-12-24', '2022-01-15', 76.01, 60.85, 12, 1, 2, 32);

insert into alugar (dataInicial, dataFinal, custo, caucao, nicCliente, idServicoAluguer, matriculaVeiculo, codigoFilial) values ('2020-12-21', '2021-12-09', 286.61, 10.71, 13, 2, 3, 33);

insert into alugar (dataInicial, dataFinal, custo, caucao, nicCliente, idServicoAluguer, matriculaVeiculo, codigoFilial) values ('2020-08-03', '2021-09-12', 80.09, 61.84, 14, 3, 4, 34);

insert into alugar (dataInicial, dataFinal, custo, caucao, nicCliente, idServicoAluguer, matriculaVeiculo, codigoFilial) values ('2020-12-15', '2022-02-04', 181.45, 10.96, 15, 4, 5, 35);

insert into alugar (dataInicial, dataFinal, custo, caucao, nicCliente, idServicoAluguer, matriculaVeiculo, codigoFilial) values ('2020-11-15', '2022-05-22', 190.36, 48.02, 16, 5, 6, 36);

insert into alugar (dataInicial, dataFinal, custo, caucao, nicCliente, idServicoAluguer, matriculaVeiculo, codigoFilial) values ('2020-10-26', '2022-06-22', 97.92, 48.97, 17, 6, 7, 37);

insert into alugar (dataInicial, dataFinal, custo, caucao, nicCliente, idServicoAluguer, matriculaVeiculo, codigoFilial) values ('2020-07-04', '2021-09-24', 196.77, 6.15, 18, 7, 8, 38);

insert into alugar (dataInicial, dataFinal, custo, caucao, nicCliente, idServicoAluguer, matriculaVeiculo, codigoFilial) values ('2020-06-24', '2022-02-22', 139.15, 65.99, 19, 1, 9, 39);

insert into alugar (dataInicial, dataFinal, custo, caucao, nicCliente, idServicoAluguer, matriculaVeiculo, codigoFilial) values ('2020-06-24', '2021-11-17', 237.52, 96.39, 20, 2, 10, 40);

insert into alugar (dataInicial, dataFinal, custo, caucao, nicCliente, idServicoAluguer, matriculaVeiculo, codigoFilial) values ('2020-09-16', '2021-10-27', 137.79, 79.58, 21, 3, 1, 41);

insert into alugar (dataInicial, dataFinal, custo, caucao, nicCliente, idServicoAluguer, matriculaVeiculo, codigoFilial) values ('2020-06-23', '2022-04-04', 228.47, 39.24, 22, 4, 2, 42);

insert into alugar (dataInicial, dataFinal, custo, caucao, nicCliente, idServicoAluguer, matriculaVeiculo, codigoFilial) values ('2020-09-23', '2022-05-06', 50.89, 87.31, 23, 5, 3, 43);

insert into alugar (dataInicial, dataFinal, custo, caucao, nicCliente, idServicoAluguer, matriculaVeiculo, codigoFilial) values ('2020-11-14', '2021-12-14', 16.13, 19.68, 24, 6, 4, 44);

insert into alugar (dataInicial, dataFinal, custo, caucao, nicCliente, idServicoAluguer, matriculaVeiculo, codigoFilial) values ('2020-09-03', '2021-07-11', 243.42, 45.51, 25, 7, 5, 45);

insert into alugar (dataInicial, dataFinal, custo, caucao, nicCliente, idServicoAluguer, matriculaVeiculo, codigoFilial) values ('2020-06-20', '2022-03-29', 278.4, 53.85, 26, 1, 6, 46);

insert into alugar (dataInicial, dataFinal, custo, caucao, nicCliente, idServicoAluguer, matriculaVeiculo, codigoFilial) values ('2020-07-14', '2022-03-20', 243.49, 90.85, 27, 2, 7, 47);

insert into alugar (dataInicial, dataFinal, custo, caucao, nicCliente, idServicoAluguer, matriculaVeiculo, codigoFilial) values ('2020-11-28', '2022-02-08', 34.84, 7.29, 28, 3, 8, 48);

insert into alugar (dataInicial, dataFinal, custo, caucao, nicCliente, idServicoAluguer, matriculaVeiculo, codigoFilial) values ('2020-09-23', '2022-02-09', 76.78, 28.66, 29, 4, 9, 49);

insert into alugar (dataInicial, dataFinal, custo, caucao, nicCliente, idServicoAluguer, matriculaVeiculo, codigoFilial) values ('2020-09-22', '2022-01-07', 151.15, 60.59, 30, 5, 10, 50);

insert into alugar (dataInicial, dataFinal, custo, caucao, nicCliente, idServicoAluguer, matriculaVeiculo, codigoFilial) values ('2020-09-27', '2021-09-23', 184.95, 46.98, 31, 6, 1, 51);

insert into alugar (dataInicial, dataFinal, custo, caucao, nicCliente, idServicoAluguer, matriculaVeiculo, codigoFilial) values ('2020-10-21', '2021-08-07', 30.06, 87.39, 32, 7, 2, 52);

insert into alugar (dataInicial, dataFinal, custo, caucao, nicCliente, idServicoAluguer, matriculaVeiculo, codigoFilial) values ('2020-09-11', '2022-02-18', 118.31, 10.06, 33, 1, 3, 53);

insert into alugar (dataInicial, dataFinal, custo, caucao, nicCliente, idServicoAluguer, matriculaVeiculo, codigoFilial) values ('2020-11-25', '2021-12-08', 214.1, 11.7, 34, 2, 4, 54);

insert into alugar (dataInicial, dataFinal, custo, caucao, nicCliente, idServicoAluguer, matriculaVeiculo, codigoFilial) values ('2020-07-12', '2022-05-21', 288.06, 4.82, 35, 3, 5, 55);

insert into alugar (dataInicial, dataFinal, custo, caucao, nicCliente, idServicoAluguer, matriculaVeiculo, codigoFilial) values ('2020-09-10', '2022-04-07', 148.46, 55.13, 36, 4, 6, 56);

insert into alugar (dataInicial, dataFinal, custo, caucao, nicCliente, idServicoAluguer, matriculaVeiculo, codigoFilial) values ('2021-01-05', '2021-09-05', 91.29, 65.23, 37, 5, 7, 57);

insert into alugar (dataInicial, dataFinal, custo, caucao, nicCliente, idServicoAluguer, matriculaVeiculo, codigoFilial) values ('2020-12-16', '2021-11-05', 158.38, 82.13, 38, 6, 8, 58);

insert into alugar (dataInicial, dataFinal, custo, caucao, nicCliente, idServicoAluguer, matriculaVeiculo, codigoFilial) values ('2020-10-08', '2021-07-26', 64.0, 83.54, 39, 7, 9, 59);

insert into alugar (dataInicial, dataFinal, custo, caucao, nicCliente, idServicoAluguer, matriculaVeiculo, codigoFilial) values ('2020-10-21', '2021-08-30', 155.35, 50.38, 40, 1, 10, 60);







### Menciona 
---
[< Previous](rebd04.md) | [^ Main](https://github.com/exemploTrabalho/reportSIBD/) | Next >
:--- | :---: | ---: 
