# C3 : SQL

## DDL

SET FOREIGN_KEY_CHECKS=0;

SET SQL_MODE="NO_AUTO_VALUE_ON_ZERO";

SET AUTOCOMMIT=0;

USE `test`;

DROP TABLE IF EXISTS `Veiculo`;

DROP TABLE IF EXISTS `Cliente`;

DROP TABLE IF EXISTS `Alugar`;

DROP TABLE IF EXISTS `Filial`;

DROP TABLE IF EXISTS `Funcionário`;

DROP TABLE IF EXISTS `TipoVeiculo`;

DROP TABLE IF EXISTS `Departamento`;

DROP TABLE IF EXISTS `Serviço`;

DROP TABLE IF EXISTS `CódigoPostais`;

DROP TABLE IF EXISTS `Modelos`;

CREATE TABLE IF NOT EXISTS `Veiculo` (

  `matricula` int(4) unsigned NOT NULL,
  
  `stock` int(4) unsigned NOT NULL,
  
  PRIMARY KEY (`matricula`)
  
) ENGINE=InnoDB DEFAULT CHARSET=latin1 COLLATE=latin1_bin;

CREATE TABLE IF NOT EXISTS `Cliente` (

  `nic` int(4) unsigned NOT NULL,
  
  `telefone` int(4) unsigned NOT NULL,
  
  `email` varchar(3) COLLATE latin1_bin NOT NULL,
  
  `cartacondução` float unsigned NOT NULL,
  
  `PrimeiroNome` varchar(3) COLLATE latin1_bin NOT NULL,
  
  `UltimoNome` varchar(3) COLLATE latin1_bin NOT NULL,
  
  PRIMARY KEY (`nic`)
  
) ENGINE=InnoDB DEFAULT CHARSET=latin1 COLLATE=latin1_bin;

CREATE TABLE IF NOT EXISTS `alugar` (

  `código` int(4) unsigned NOT NULL,
  
  `DataInicial` tinyint(1) NOT NULL,
  
  `DataFinal` int(10) unsigned NOT NULL,
  
  `Custo` int(10) unsigned NOT NULL,
  
  `Caução` int(10) unsigned NOT NULL,
  
  PRIMARY KEY (`código`)
  
) ENGINE=InnoDB DEFAULT CHARSET=latin1 COLLATE=latin1_bin;

CREATE TABLE IF NOT EXISTS `Filial` (

  `numero` int(4) unsigned NOT NULL,
  
  `rua` ,varchar(2) COLLATE latin1_bin NOT NULL,
  
  `porta` varchar(8) COLLATE latin1_bin NOT NULL,
  
  PRIMARY KEY (`numero`),
  
) ENGINE=InnoDB DEFAULT CHARSET=latin1 COLLATE=latin1_bin;

CREATE TABLE IF NOT EXISTS `Funcionário` (

  `nic` int(4) unsigned NOT NULL,
  
  `endereço` varchar(2) COLLATE latin1_bin NOT NULL,
  
  `dn` int(4) unsigned NOT NULL,
  
  `sexo` varchar(2) COLLATE latin1_bin NOT NULL,
  
  `PrimeiroNome` varchar(2) COLLATE latin1_bin NOT NULL,
  
  `UltimoNome` varchar(2) COLLATE latin1_bin NOT NULL,
  
  PRIMARY KEY (`nic`),
  
) ENGINE=InnoDB DEFAULT CHARSET=latin1 COLLATE=latin1_bin;

CREATE TABLE IF NOT EXISTS `TipoVeiculo` (

  `código` int(4) unsigned NOT NULL,
  
  `Nome` varchar(2) COLLATE latin1_bin NOT NULL,
  
  `ValorHora` int(4) unsigned NOT NULL,
  
  PRIMARY KEY (`código`),
  
) ENGINE=InnoDB DEFAULT CHARSET=latin1 COLLATE=latin1_bin;

CREATE TABLE IF NOT EXISTS `Departamento` (

  `código` int(4) unsigned NOT NULL,
  
  `rua` varchar(2) COLLATE latin1_bin NOT NULL,
  
  `porta` int(4) unsigned NOT NULL,
  
  PRIMARY KEY (`código`),
  
) ENGINE=InnoDB DEFAULT CHARSET=latin1 COLLATE=latin1_bin;

CREATE TABLE IF NOT EXISTS `Serviço` (

  `idserviço` int(4) unsigned NOT NULL,
  
  `valor` int(4) unsigned NOT NULL,
  
  `ndias` int(4) unsigned NOT NULL,
  
  PRIMARY KEY (`idserviço`),
  
) ENGINE=InnoDB DEFAULT CHARSET=latin1 COLLATE=latin1_bin;

CREATE TABLE IF NOT EXISTS `CódigoPostais` (

  `códigoPostal` int(4) unsigned NOT NULL,
  
  `Localidade` varchar(2) COLLATE latin1_bin NOT NULL,
  
  PRIMARY KEY (`códigoPostal`),
  
) ENGINE=InnoDB DEFAULT CHARSET=latin1 COLLATE=latin1_bin;

CREATE TABLE IF NOT EXISTS `Modelos` (

  `Modelo` varchar(2) COLLATE latin1_bin NOT NULL,
  
  `Marca` varchar(2) COLLATE latin1_bin NOT NULL,
  
  PRIMARY KEY (`Modelo`),
  
) ENGINE=InnoDB DEFAULT CHARSET=latin1 COLLATE=latin1_bin;


SET FOREIGN_KEY_CHECKS=1;
COMMIT;

## DML

### Tabela Funcionário

![TabelaFuncionário](https://user-images.githubusercontent.com/96230913/171994002-0e521eea-a3b4-4a1f-a067-b132a630d61d.png)


---
[< Previous](rebd04.md) | [^ Main](https://github.com/exemploTrabalho/reportSIBD/) | Next >
:--- | :---: | ---: 
