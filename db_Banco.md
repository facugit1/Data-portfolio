# Sistema de gestión Bancaria

El siguiente proyecto consiste en un sistema de gestión bancario, inspirado y adaptado del proyecto propuesto por la web [geeksforgeeks](https://www.geeksforgeeks.org/python/bank-management-system-using-python-mysql-connectivity/)

El proyecto propuesto por la web adjunta arriba esta hecho con python y utilizando la libreria de mysql. Lo que me propuse fue adaptarlo a SQL Server, adaptando las funciones 
de python a procedimientos. 
El sistema de gestión bancario es un sistema del tipo CRUD, permite crear nuevos usuarios, realizar consultas, actualizar datos de  usuarios y eliminar registros. A su vez permite realizar transacciones bancarias, llevando un registro en la tabla Transacciones el tipo de transacción, el id del cliente que la realizó, el monto y la fecha. Según el tipo de transacción a realizar, el registro "balance" de la Tabla cuenta se actualiza, incrementando su valor en caso de realizar transacciones del tipo "Deposito" o disminuyendo de ser del tipo "Extracción". Estos procesos se pretenden automatizar mediante Triggers, los cuales se detallan más adelante en el presente documento.

Para empezar, se realizó el siguiente diagrama ER para observar las tablas a trabajar y las relaciones entre claves primarias y foraneas


<img width="957" height="530" alt="image" src="https://github.com/user-attachments/assets/5f0fa712-5838-4b8e-8134-16833fa24eb8" />

En base al diagrama ER, se procede a la creación de la base de datos nombrada "Banco" y a las tablas necesarios.

CREATE DATABASE Banco;

USE Banco;

Una vez creada la base de datos, se procede a crear las tablas necesarias

CREATE TABLE Clientes(
	ID_cliente INT PRIMARY KEY IDENTITY (1,1) NOT NULL,
	nombre  VARCHAR(50) NOT NULL,
	apellido VARCHAR(50) NOT NULL,
	telefono VARCHAR(20),
	direccion VARCHAR (100)
); 

CREATE TABLE Cuenta(
	ID_cuenta INT PRIMARY KEY IDENTITY (1,1) NOT NULL,	
	tipo_cuenta VARCHAR(20),
	balance DECIMAL(10,2),
	ID_cliente INT NOT NULL
	FOREIGN KEY(ID_cliente) REFERENCES Clientes(ID_cliente)
);

CREATE TABLE Transacciones(
	ID_transaccion INT PRIMARY KEY IDENTITY (1,1) NOT NULL,
	tipo_transaccion VARCHAR(20),
	cantidad DECIMAL(10,2),
	fecha_transaccion DATE,
	ID_cuenta INT NOT NULL
	FOREIGN KEY(ID_cuenta) REFERENCES Cuenta(ID_cuenta)
);

Con esto se crean las tablas y se definen sus claves primarias y claves foráneas, estas últimas para realizar consultas de mayor complejidad.
Se ingresaron registros mediante la clausula INSERT INTO en las tablas Cliente y Cuenta.

INSERT INTO Clientes(nombre, apellido, telefono, direccion)
Values ('Nahuel', 'Torrez', '4202-4447', 'Avenida de los Corrales 1985')
		('Roberto', 'Torres', '4234-4567', 'Avenida del Pairo 87'),
		('Ceferino' , 'Namuncu' , '4356-1234' , 'Laprida 234'),
		('Alfonso','Rodriguez','2234-4567','Peña 36'),
		('Casandra','Clare','5678-4732','Poncho 452'),
		('Luisiana','Lopez','9847-3754','Rossi 7345'),
		('Mario','Rojas','87399-0013','Jujuy 23');

INSERT INTO Cuenta(tipo_cuenta, balance, ID_cliente)
VALUES ('Caja de ahorro', 10000.00, 1),
		('Cuenta Sueldo', 5000.00,2),
		('Cuenta Corriente', 12000.00, 3),
		('Cuenta Corriente', 4500.00, 4),
		('Caja de ahorro', 200000.00 , 5),
		('Cuenta sueldo', 54900.00, 6),
		('Cuenta sueldo' , 39675.00 , 7);
