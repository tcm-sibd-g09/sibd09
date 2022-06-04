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

CREATE TABLE [dbo].[alugar](

    [codigo] [int] IDENTITY(1,1) NOT NULL,
    
    [dataInicial] [date] NOT NULL,
    
    [dataFinal] [date] NOT NULL,
    
    [custo] [numeric](10, 2) NOT NULL,
    
    [caucao] [numeric](10, 2) NOT NULL,
    
    [idCliente] [int] NOT NULL,
    
    [idServico] [int] NULL,
    
    [matriculaVeiculo] [varchar](30) NULL,
    
    [idFilial] [int] NOT NULL,
    
 CONSTRAINT [PK_alugar] PRIMARY KEY CLUSTERED 
 
(

    [codigo] ASC
    
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON, OPTIMIZE_FOR_SEQUENTIAL_KEY = OFF) ON

[PRIMARY]
) ON [PRIMARY]

GO

ALTER TABLE [dbo].[alugar]  WITH CHECK ADD  CONSTRAINT [FK_alugar_clientes] FOREIGN KEY([idCliente])

REFERENCES [dbo].[clientes] ([nic])

GO

ALTER TABLE [dbo].[alugar] CHECK CONSTRAINT [FK_alugar_clientes]

GO

ALTER TABLE [dbo].[alugar]  WITH CHECK ADD  CONSTRAINT [FK_alugar_filial] FOREIGN KEY([idFilial])

REFERENCES [dbo].[filial] ([numero])

GO

ALTER TABLE [dbo].[alugar] CHECK CONSTRAINT [FK_alugar_filial]

GO

ALTER TABLE [dbo].[alugar]  WITH CHECK ADD  CONSTRAINT [FK_alugar_Servico] FOREIGN KEY([idServico])

REFERENCES [dbo].[Servico] ([idServico])

GO

ALTER TABLE [dbo].[alugar] CHECK CONSTRAINT [FK_alugar_Servico]

GO

ALTER TABLE [dbo].[alugar]  WITH CHECK ADD  CONSTRAINT [FK_alugar_veiculos] FOREIGN KEY([matriculaVeiculo])

REFERENCES [dbo].[veiculos] ([matricula])

GO

ALTER TABLE [dbo].[alugar] CHECK CONSTRAINT [FK_alugar_veiculos]

GO

CREATE TABLE [dbo].[clientes](

    [nic] [int] IDENTITY(1,1) NOT NULL,
    
    [telefone] [bigint] NOT NULL,
    
    [email] [varchar](100) NOT NULL,
    
    [cartaConducao] [bigint] NOT NULL,
    
    [PrimeiroNome] [varchar](100) NOT NULL,
    
    [SegundoNome] [varchar](100) NOT NULL,
    
    [codPostal] [int] NOT NULL,
    
 CONSTRAINT [PK_clientes] PRIMARY KEY CLUSTERED 

(

    [nic] ASC
    
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON, OPTIMIZE_FOR_SEQUENTIAL_KEY = OFF) ON

[PRIMARY]

) ON [PRIMARY]

GO

ALTER TABLE [dbo].[clientes]  WITH CHECK ADD  CONSTRAINT [FK_clientes_codPostais] FOREIGN KEY([codPostal])

REFERENCES [dbo].[codPostais] ([codPostal])

GO

ALTER TABLE [dbo].[clientes] CHECK CONSTRAINT [FK_clientes_codPostais]

GO

CREATE TABLE [dbo].[codPostais](

    [codPostal] [int] NOT NULL,
    
    [localidade] [varchar](100) NOT NULL,
    
 CONSTRAINT [PK_codPostais] PRIMARY KEY CLUSTERED 
 
(

    [codPostal] ASC
    
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON, OPTIMIZE_FOR_SEQUENTIAL_KEY = OFF) ON 

[PRIMARY]
) ON [PRIMARY]

GO

CREATE TABLE [dbo].[departamento](

    [codigo] [int] IDENTITY(1,1) NOT NULL,
    
    [codpostal] [int] NOT NULL,
    
    [rua] [varchar](100) NOT NULL,
    
    [porta] [int] NOT NULL,
    
 CONSTRAINT [PK_departamento] PRIMARY KEY CLUSTERED
 
(

    [codigo] ASC
    
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON, OPTIMIZE_FOR_SEQUENTIAL_KEY = OFF) ON 

[PRIMARY]
) ON [PRIMARY]

GO

ALTER TABLE [dbo].[departamento]  WITH CHECK ADD  CONSTRAINT [FK_departamento_codPostais] FOREIGN KEY([codpostal])

REFERENCES [dbo].[codPostais] ([codPostal])

GO

ALTER TABLE [dbo].[departamento] CHECK CONSTRAINT [FK_departamento_codPostais]
GO

CREATE TABLE [dbo].[filial](

    [numero] [int] NOT NULL,
    
    [codPostal] [int] NOT NULL,
    
    [rua] [varchar](100) NOT NULL,
    
    [porta] [int] NOT NULL,
    
    [idDepartamento] [int] IDENTITY(1,1) NOT NULL,
    
 CONSTRAINT [PK_filial] PRIMARY KEY CLUSTERED 
 
(

    [numero] ASC
    
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON, OPTIMIZE_FOR_SEQUENTIAL_KEY = OFF) ON 

[PRIMARY]

) ON [PRIMARY]

GO

ALTER TABLE [dbo].[filial]  WITH CHECK ADD  CONSTRAINT [FK_filial_codPostais] FOREIGN KEY([codPostal])

REFERENCES [dbo].[codPostais] ([codPostal])

GO

ALTER TABLE [dbo].[filial] CHECK CONSTRAINT [FK_filial_codPostais]

GO

ALTER TABLE [dbo].[filial]  WITH CHECK ADD  CONSTRAINT [FK_filial_departamento] FOREIGN KEY([idDepartamento])

REFERENCES [dbo].[departamento] ([codigo])

GO

ALTER TABLE [dbo].[filial] CHECK CONSTRAINT [FK_filial_departamento]

GO

CREATE TABLE [dbo].[funcionario](

    [nic] [int] NOT NULL,
    
    [email] [varchar](100) NOT NULL,
    
    [dataNascimento] [date] NOT NULL,
    
    [salario] [numeric](10, 2) NOT NULL,
    
    [idFilial] [int] NOT NULL,
    
    [primeiroNome] [varchar](100) NOT NULL,
    
    [ultimoNome] [varchar](100) NOT NULL,
    
    [idDepartamento] [int] NOT NULL,
    
 CONSTRAINT [PK_funcionario] PRIMARY KEY CLUSTERED 
 
(

    [nic] ASC
    
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON, OPTIMIZE_FOR_SEQUENTIAL_KEY = OFF) ON 

[PRIMARY]

) ON [PRIMARY]

GO

ALTER TABLE [dbo].[funcionario]  WITH CHECK ADD  CONSTRAINT [FK_funcionario_departamento] FOREIGN KEY([idDepartamento])

REFERENCES [dbo].[departamento] ([codigo])

GO

ALTER TABLE [dbo].[funcionario] CHECK CONSTRAINT [FK_funcionario_departamento]

GO

ALTER TABLE [dbo].[funcionario]  WITH CHECK ADD  CONSTRAINT [FK_funcionario_filial] FOREIGN KEY([idFilial])

REFERENCES [dbo].[filial] ([numero])

GO

ALTER TABLE [dbo].[funcionario] CHECK CONSTRAINT [FK_funcionario_filial]

GO

CREATE TABLE [dbo].[modelos](

    [modelo] [varchar](100) NOT NULL,
    
    [marca] [varchar](100) NOT NULL,
    
 CONSTRAINT [PK_modelos] PRIMARY KEY CLUSTERED 
 
(

    [modelo] ASC
    
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON, OPTIMIZE_FOR_SEQUENTIAL_KEY = OFF) ON 

[PRIMARY]

) ON [PRIMARY]

GO

CREATE TABLE [dbo].[Servico](

    [idServico] [int] IDENTITY(1,1) NOT NULL,
    
    [valor] [numeric](10, 2) NOT NULL,
    
    [nDias] [int] NOT NULL,
    
 CONSTRAINT [PK_Servico] PRIMARY KEY CLUSTERED 
 
(

    [idServico] ASC
    
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON, OPTIMIZE_FOR_SEQUENTIAL_KEY = OFF) ON 

[PRIMARY]

) ON [PRIMARY]

GO

CREATE TABLE [dbo].[tipoVeiculo](

    [codigo] [int] IDENTITY(1,1) NOT NULL,
    
    [nome] [varchar](100) NOT NULL,
    
    [valorHora] [float] NOT NULL,
    
 CONSTRAINT [PK_tipoVeiculo] PRIMARY KEY CLUSTERED 
 
(

    [codigo] ASC
    
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON, OPTIMIZE_FOR_SEQUENTIAL_KEY = OFF) ON 

[PRIMARY]

) ON [PRIMARY]

GO

CREATE TABLE [dbo].[veiculos](

    [matricula] [varchar](30) NOT NULL,
    
    [stock] [int] NOT NULL,
    
    [modelo] [varchar](100) NOT NULL,
    
    [idTipoVeiculo] [int] NOT NULL,
    
 CONSTRAINT [PK_veiculos] PRIMARY KEY CLUSTERED 
 
(

    [matricula] ASC
    
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON, OPTIMIZE_FOR_SEQUENTIAL_KEY = OFF) ON 

[PRIMARY]

) ON [PRIMARY]

GO

ALTER TABLE [dbo].[veiculos]  WITH CHECK ADD  CONSTRAINT [FK_veiculos_modelos] FOREIGN KEY([modelo])

REFERENCES [dbo].[modelos] ([modelo])

GO

ALTER TABLE [dbo].[veiculos] CHECK CONSTRAINT [FK_veiculos_modelos]

GO

ALTER TABLE [dbo].[veiculos]  WITH CHECK ADD  CONSTRAINT [FK_veiculos_tipoVeiculo] FOREIGN KEY([idTipoVeiculo])

REFERENCES [dbo].[tipoVeiculo] ([codigo])

GO

ALTER TABLE [dbo].[veiculos] CHECK CONSTRAINT [FK_veiculos_tipoVeiculo]

GO

SET SQL_MODE=@OLD_SQL_MODE;

SET FOREIGN_KEY_CHECKS=@OLD_FOREIGN_KEY_CHECKS;

SET UNIQUE_CHECKS=@OLD_UNIQUE_CHECKS;

SET FOREIGN_KEY_CHECKS=1;
COMMIT;

## DML

### Tabela Funcionário

![TabelaFuncionário](https://user-images.githubusercontent.com/96230913/171994002-0e521eea-a3b4-4a1f-a067-b132a630d61d.png)

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
