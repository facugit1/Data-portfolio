El siguiente proyecto consiste en un sistema de gestión bancario, inspirado y adaptado del proyecto propuesto por la web [geeksforgeeks](https://www.geeksforgeeks.org/python/bank-management-system-using-python-mysql-connectivity/)

El proyecto propuesto por la web adjunta arriba esta hecho con python y utilizando la libreria de mysql. Lo que me propuse fue adaptarlo a SQL Server, adaptando las funciones 
de python a procedimientos. 
El sistema de gestión bancario es un sistema del tipo CRUD, permite crear nuevos usuarios, realizar consultas, actualizar datos de  usuarios y eliminar registros. A su vez permite realizar transacciones bancarias, llevando un registro en la tabla Transacciones el tipo de transacción, el id del cliente que la realizó, el monto y la fecha. Según el tipo de transacción a realizar, el registro "balance" de la Tabla cuenta se actualiza, incrementando su valor en caso de realizar transacciones del tipo "Deposito" o disminuyendo de ser del tipo "Extracción". Estos procesos se pretenden automatizar mediante Triggers, los cuales se detallan más adelante en el presente documento.

Para empezar, se realizó el siguiente diagrama ER para observar las tablas a trabajar y las relaciones entre claves primarias y foraneas


<img width="957" height="530" alt="image" src="https://github.com/user-attachments/assets/5f0fa712-5838-4b8e-8134-16833fa24eb8" />

En base al diagrama ER, se procede a la creación de la base de datos nombrada "Banco" y a las tablas necesarios.

CREATE DATABASE Banco; --se crea la base de datos Banco

USE Banco;
