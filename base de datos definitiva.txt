#DDL Y DML DE LA BASE DE DATOS 
/*----------------------------------------------------------------------------------------------------------------*/
#CREACIÓN, ELIMINACIÓN Y USO DE LA BASE DE DATOS
create database Tienda_De_Ropav2;
drop database if exists Tienda_De_Ropa;
use Tienda_De_Ropa;
/*----------------------------------------------------------------------------------------------------------------*/
#CREACIÓN DE LA TABLA PERSONA
create table Persona (
id_persona int(2) AUTO_INCREMENT primary key,
nombre varchar(50),
apellidos varchar(80),
sexo char(1),
direccion varchar(80),
telefono int(15),
correo_electronico varchar(80));
#INSERTAR DATOS EN LA TABLA PERSONA
#CLIENTES
insert into Persona values 
(01, 'Maria', 'Rodriguez Mejia', 'F', 'Cochabamba', 75593112, 'mariarm@gmail.com'),
(02, 'Alejandra Jhenifer', 'Chaves Flores', 'F', 'Beni', 66623112, 'alejandrajh@gmail.com'),
(03, 'Ximena', 'Vallejos Zoe', 'F', 'La Paz', 67723112, 'ximenavz@gmail.com');
#VENDEDORES
insert into Persona values 
(04, 'Moises', 'Rueda Mojica', 'M', 'Santa Cruz de la Sierra', 73293176, 'moisesrm@gmail.com'),
(05, 'Antonio', 'Perez Dominguez', 'M', 'Cochabamba', 75223112, 'antoniopd@gmail.com');
#PROVEEDORES
insert into Persona values 
(06, 'Alejandro', 'Flores Claros', 'M', 'Sucre', 72323112, 'alejandrofcl@gmail.com'),
(07, 'Luis Enrique', 'Quinteros Claros', 'M', 'Sucre', 65593112, 'luisqcl@gmail.com');
#MOSTRAR TODA LA TABLA PERSONA
select * from Persona;
/*----------------------------------------------------------------------------------------------------------------*/
#CREACION DE LA TABLA CLIENTE
create table Cliente (
  id_cliente int(2) AUTO_INCREMENT primary key,
  id_persona int(2),
  estado_cliente char(1),
  fecha_de_visita date,
  foreign key (id_persona) references Persona(id_persona));
#INSERTAR DATOS EN LA TABLA CLIENTE
insert into cliente values 
(01,01,'N','2023-11-15'),
(02,02,'A','2020-06-01'),
(03,03,'N','2023-10-29');
#MOSTRAR TODA LA TABLA CLIENTE
select * from Cliente;
/*----------------------------------------------------------------------------------------------------------------*/
#CREACION DE LA TABLA VENDEDOR
create table Vendedor (
id_vendedor int(2) AUTO_INCREMENT primary key,
id_persona int(2),
fecha_de_contratacion date,
foreign key (id_persona) references Persona(id_persona));
#INSERTAR DATOS EN LA TABLA VENDEDOR
insert into vendedor values 
(01,04,'20 de septiembre 2020'),
(02,05,'25 de septiembre 2020');
#ACTUALIZACIÓN DE DATOS EN FECHA DE LA TABLA VENDEDOR
UPDATE Vendedor
SET fecha_de_contratacion = '2020-09-20'
WHERE id_vendedor = 01;
#ACTUALIZACIÓN DE DATOS EN FECHA DE LA TABLA VENDEDOR
UPDATE Vendedor
SET fecha_de_contratacion = '2020-09-25'
WHERE id_vendedor = 02;
#MOSTRAR TODA LA TABLA VENDEDOR
select * from Vendedor;
/*----------------------------------------------------------------------------------------------------------------*/
#CREACION DE LA TABLA PROVEEDOR
create table Proveedor (
id_proveedor int(2) AUTO_INCREMENT primary key,
id_vendedor int(2),
id_persona int(2),
nombre_empresa_Marca varchar(20),
foreign key (id_vendedor) references Vendedor(id_vendedor),
foreign key (id_persona) references Persona(id_persona));
#INSERTAR DATOS EN LA TABLA PROVEEDOR
insert into proveedor values 
(01,01,06, 'ADIDAS'),
(02,02,07, 'DEVIS');
#MOSTRAR TODA LA TABLA PROVEEDOR
select * from Proveedor;
/*----------------------------------------------------------------------------------------------------------------*/
#CREACION DE LA TABLA CATEGORIA
create table Categoria (
id_categoria int(2) AUTO_INCREMENT primary key,
nombre_cat varchar(20));
#INSERTAR DATOS EN LA TABLA PRODUCTO
insert into categoria values
(01,'pantalones'),
(02,'camisetas'),
(03,'poleras');
#MOSTRAR TODA LA TABLA CATEGORIA
select * from categoria;
/*----------------------------------------------------------------------------------------------------------------*/
#CREACION DE LA TABLA PRODUCTO(AGREGAR id_categoria por foreign key)
CREATE TABLE Producto (
    id_producto INT(3) AUTO_INCREMENT PRIMARY KEY,
    nombre_producto VARCHAR(30),
    descripcion VARCHAR(150),
    precio FLOAT(10),
    cantidad INT(10),
    id_proveedor INT(2),
    talla CHAR(20),
    color VARCHAR(20),
    id_categoria int(2),
    foreign key (id_categoria) references Categoria(id_categoria),
    FOREIGN KEY (id_proveedor) REFERENCES Proveedor(id_proveedor)
);
#INSERTAR DATOS EN LA TABLA PRODUCTO
insert into producto values
(1,'jeans','pantalones jeans sin agujeros de la rmarca DEVIS,talla M',80.99,13,02,'M','azul',1), 
(2,'jeans','pantalones jeans con agujeros de la marca DEVIS,talla M',70.99,10,02,'M','azul',1),
(3,'jeans','pantalones jeans sin agujeros de la marca DEVIS,talla L',95.99,8,02,'L','azul',1),
(4,'jeans','pantalones jeans con agujeros de la marca DEVIS,talla L',100.99,3,02,'L','azul',1), 
(5,'jeans','pantalones jeans sin agujeros de la marca DEVIS,talla XL',112.99,10,02,'XL','azul',1),
(6,'jeans','pantalones jeans con agujeros de la marca DEVIS,talla XL',102.99,4,02,'XL','azul',1),
(7,'jeans','pantalones jeans sin agujeros de la marca DEVIS,talla XXL',122.99,2,02,'XXL','azul',1),
(8,'jeans','pantalones jeans con agujeros de la marca DEVIS,talla XXL',120.99,23,02,'XXL','azul',1),
(9,'jeans','pantalones jeans sin agujeros de la marca DEVIS,talla XXXL',130.99,1,02,'XXXL','azul',1),
(10,'jeans','pantalones jeans con agujeros de la marca DEVIS,talla XXXL',125.99,2,02,'XXXL','azul',1);
#MOSTRAR TODA LA TABLA PRODUCTO
select * from PRODUCTO;
/*----------------------------------------------------------------------------------------------------------------*/
#CREACION DE LA TABLA VENTA
create table Venta (
id_venta int(2) AUTO_INCREMENT primary key,
fecha_de_venta date,
id_cliente int(2),
id_vendedor int(2),
foreign key (id_cliente) references cliente(id_cliente),
foreign key (id_vendedor) references vendedor(id_vendedor));
#INSERTAR DATOS EN LA TABLA PRODUCTO
insert into Venta values
(11,'2023-11-15',01,01),
(12,'2020-06-01',02,02),
(13,'2023-10-29',03,02);
#MOSTRAR TODA LA TABLA VENTA
select * from Venta;
/*----------------------------------------------------------------------------------------------------------------*/
#CREACION DE LA TABLA DETALLE_DE_VENTA
create table Detalle_de_Venta (
id_detalle int(2) AUTO_INCREMENT primary key,
id_producto int(2),
id_venta int(2),
cantidad_vendida int(5),
precio_total_de_venta float(10),
foreign key (id_producto) references producto(id_producto),
foreign key (id_venta) references Venta(id_venta));
#INSERTAR DATOS EN LA TABLA PRODUCTO
insert into detalle_de_venta values
(11,01,11,1,80.99),
(12,04,12,3,403.96),
(13,10,13,2,251.98);
#MOSTRAR TODA LA TABLA DETALLE_DE_VENTA
select * from detalle_de_venta;
/*----------------------------------------------------------------------------------------------------------------*/
/*ELIMINAR TABLA DETALLE_DE_VENTA*/
drop TABLE Detalle_de_Venta;

/*ELIMINAR TABLA VENTA*/
DROP TABLE Venta;

/*ELIMINAR TABLA CATEGORIA*/
DROP TABLE Categoria;

/*ELIMINAR TABLA PRODUCTO*/
DROP TABLE Producto;

/*ELIMINAR TABLA PROVEEDOR*/
DROP TABLE Proveedor;

/*ELIMINAR TABLA VENDEDOR*/
DROP TABLE Vendedor;

/*ELIMINAR TABLA CLIENTE*/
DROP TABLE Cliente;

/*ELIMINAR TABLA PERSONA*/
DROP TABLE Persona;

/*VACIAR TABLA DETALLE_DE_VENTA*/
TRUNCATE TABLE Detalle_de_Venta;

/*VACIAR TABLA VENTA*/
TRUNCATE TABLE Venta;

/*VACIAR TABLA CATEGORIA*/
TRUNCATE TABLE Categoria;

/*VACIAR TABLA PRODUCTO*/
TRUNCATE TABLE Producto;

/*VACIAR TABLA PROVEEDOR*/
TRUNCATE TABLE Proveedor;

/*VACIAR TABLA VENDEDOR*/
TRUNCATE TABLE Vendedor;

/*VACIAR TABLA CLIENTES*/
TRUNCATE TABLE Cliente;

/*VACIAR TABLA PERSONA*/
TRUNCATE TABLE Persona;

-- Búsqueda de patrones en la tabla Persona
SELECT * FROM Persona
WHERE nombre LIKE 'A%';


-- Búsqueda de patrones regexp en la tabla Persona
SELECT * FROM Persona
WHERE nombre REGEXP '^[AEIOU].*$';



-- Uso de alias para cambiar el nombre de la columna
SELECT nombre AS NombresP, apellidos AS ApellidosP FROM Persona;



-- Uso de operadores lógicos en la tabla Cliente
SELECT * FROM Cliente
WHERE estado_cliente = 'N' AND fecha_de_visita > '2023-01-01';



-- Uso de JOIN para combinar información de las tablas Cliente y Persona
SELECT Cliente.id_cliente, Persona.nombre, Persona.apellidos
FROM Cliente
JOIN Persona ON Cliente.id_persona = Persona.id_persona;


-- Crear un usuario con privilegios a la base de datos
CREATE USER 'moises'@'localhost' IDENTIFIED BY '123456789';

-- Asignar privilegios a una base de datos
GRANT ALL PRIVILEGES ON Tienda_De_Ropav2.* TO 'moises'@'localhost';

-- Actualizar los privilegios
FLUSH PRIVILEGES;


-- Crear un usuario de solo lectura a una sola tabla
CREATE USER 'moises2'@'localhost' IDENTIFIED BY '987654321';

-- Asignar privilegios de solo lectura a una tabla específica
GRANT SELECT ON Tienda_De_Ropav2.producto TO 'moises2'@'localhost';

-- Actualizar los privilegios
FLUSH PRIVILEGES;



-- Mostrar usuarios disponibles
SELECT user, host FROM mysql.user;



-- Mostrar privilegios de usuario moises
SHOW GRANTS FOR 'moises'@'localhost';


-- Mostrar privilegios de usuario moises2
SHOW GRANTS FOR 'moises2'@'localhost';


#Procedimiento Almacenado 1: Actualizar Estado de Cliente
DELIMITER //
CREATE PROCEDURE ActualizarEstadoCliente(
    IN cliente_id INT,
    IN nuevo_estado CHAR(1)
)
BEGIN
    UPDATE Cliente
    SET estado_cliente = nuevo_estado
    WHERE id_cliente = cliente_id;
END //
DELIMITER ;
/*---------------------------------------------------------------*/

#Procedimiento Almacenado 2: Obtener Stock de Producto
DELIMITER //

CREATE PROCEDURE ObtenerStockProducto(
    IN producto_id INT,
    OUT stock_actual INT
)
BEGIN
    SELECT cantidad INTO stock_actual
    FROM Producto
    WHERE id_producto = producto_id;
END //

DELIMITER ;
/*---------------------------------------------------------------*/

#Función: Calcular Precio Total de Venta
DELIMITER //

CREATE FUNCTION CalcularPrecioTotal(
    cantidad INT,
    precio_unitario FLOAT
) RETURNS FLOAT
BEGIN
    DECLARE total FLOAT;
    SET total = cantidad * precio_unitario;
    RETURN total;
END //

DELIMITER ;
/*---------------------------------------------------------------*/

#Trigger: Actualizar Stock después de una Venta
DELIMITER //

CREATE TRIGGER AfterVenta
AFTER INSERT ON Detalle_de_Venta
FOR EACH ROW
BEGIN
    DECLARE cantidad_vendida INT;
    DECLARE producto_id INT;
    
    SET cantidad_vendida = NEW.cantidad_vendida;
    SET producto_id = NEW.id_producto;
    
    UPDATE Producto
    SET stock = stock - cantidad_vendida
    WHERE id_producto = producto_id;
END //

DELIMITER ;
/*---------------------------------------------------------------*/

#Vista 1: Clientes Activos
CREATE VIEW ClientesActivos AS
SELECT id_cliente, id_persona, estado_cliente, fecha_de_visita
FROM Cliente
WHERE estado_cliente = 'A';
/*---------------------------------------------------------------*/

#Vista 2: Ventas Recientes
CREATE VIEW VentasRecientes AS
SELECT id_venta, fecha_de_venta, id_cliente, id_vendedor
FROM Venta
WHERE fecha_de_venta >= CURDATE() - INTERVAL 30 DAY;
/*---------------------------------------------------------------*/

#Llamada al Procedimiento Almacenado 1: Actualizar Estado de Cliente
CALL ActualizarEstadoCliente(1, 'A');
/*---------------------------------------------------------------*/

#Llamada al Procedimiento Almacenado 2: Obtener Stock de Producto
DELIMITER //

SET @stock_actual_resultado = 0;
CALL ObtenerStockProducto(1, @stock_actual_resultado);
SELECT @stock_actual_resultado AS stock_actual;

DELIMITER ;
/*---------------------------------------------------------------*/

#Llamada a la Función: Calcular Precio Total de Venta
SET @total_venta = CalcularPrecioTotal(3, 50.99);
SELECT @total_venta AS total_venta;
/*---------------------------------------------------------------*/

#Llamada a la Vista 1: Clientes Activos
SELECT * FROM ClientesActivos;
/*---------------------------------------------------------------*/

#Llamada a la Vista 2: Ventas Recientes
SELECT * FROM VentasRecientes;
/*---------------------------------------------------------------*/
