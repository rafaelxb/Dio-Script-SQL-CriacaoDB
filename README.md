# Dio-Script-SQL-CriacaoDB

Script realizado em uma atividade da DIO que consiste na criação de um banco de dados para controle de tráfego de naves da Estrela da Morte de Star Wars.

O script postado abaixo foi testado e todas as tabelas foram criadas de acordo com o especificado.

Conforme orientação da atividade, segue script abaixo:

CREATE DATABASE EstrelaDaMorte
GO
USE EstrelaDaMorte
GO
CREATE TABLE Planetas(
	IdPlaneta int NOT NULL,
	Nome varchar(50) NOT NULL,
	Rotacao float NOT NULL,
	Orbita float NOT NULL,
	Diametro float NOT NULL,
	Clima varchar(50) NOT NULL,
	Populacao int NOT NULL
)
GO
ALTER TABLE Planetas ADD CONSTRAINT PK_Planetas PRIMARY KEY (IdPlaneta);
GO
CREATE TABLE Naves(
	IdNave int NOT NULL,
	Nome varchar(100) NOT NULL,
	Modelo varchar(100) NOT NULL,
	Passageiros int NOT NULL,
	Carga float NOT NULL,
	Classe varchar(100)
)
GO
ALTER TABLE Naves ADD CONSTRAINT PK_Naves PRIMARY KEY (IdNave);
GO
CREATE TABLE Pilotos(
	IdPiloto int NOT NULL,
	Nome varchar(200) NOT NULL,
	AnoNascimento varchar(10) NOT NULL,
	IdPlaneta int NOT NULL
)
GO
ALTER TABLE Pilotos ADD CONSTRAINT PK_Pilotos PRIMARY KEY (IdPiloto);
GO
ALTER TABLE Pilotos ADD CONSTRAINT FK_Pilotos_Planetas FOREIGN KEY (IdPlaneta)
REFERENCES Planetas (IdPlaneta)
GO
CREATE TABLE PilotosNaves(
	IdPiloto int NOT NULL,
	IdNave int NOT NULL,
	FlagAutorizado bit NOT NULL
)
GO
ALTER TABLE PilotosNaves ADD CONSTRAINT PK_PilotosNaves PRIMARY KEY (IdPiloto, IdNave) 
GO
ALTER TABLE PilotosNaves ADD CONSTRAINT FK_PilotosNaves_Pilotos FOREIGN KEY (IdPiloto)
REFERENCES Pilotos (IdPiloto)
GO
ALTER TABLE PilotosNaves ADD CONSTRAINT FK_PilotosNaves_Naves FOREIGN KEY (IdNave)
REFERENCES Naves (IdNave)
GO 
ALTER TABLE PilotosNaves ADD CONSTRAINT DF_PilotosNaves_FlagAutorizado DEFAULT (1) FOR FlagAutorizado
GO
CREATE TABLE HistoricoViagens(
	IdNave int NOT NULL,
	IdPiloto int NOT NULL,
	DtSaida datetime NOT NULL,
	DtChegada datetime NULL
)
GO
ALTER TABLE HistoricoViagens ADD CONSTRAINT FK_HistoricoViagens_PilotosNaves FOREIGN KEY (IdPiloto, IdNave)
REFERENCES PilotosNaves (IdPiloto, IdNave)
GO
ALTER TABLE HistoricoViagens CHECK CONSTRAINT FK_HistoricoViagens_PilotosNaves

Abaixo segue imagem do diagrama das tabelas após a criação:

![image](https://user-images.githubusercontent.com/79547368/137219614-086f09c8-32f1-4570-b5eb-5fc4ec2f3cf9.png)
