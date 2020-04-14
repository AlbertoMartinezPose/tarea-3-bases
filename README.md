## CREACIÓN BASE DE DATOS ##

A continuación crearemos la ##### base de datos Investigación ##### desde la terminal de comandos de Linux. Para acceder a la aplicación utilizamos el siguiente comando 
~~~~
sudo mysql
~~~~

Con este comando ya estamos listos para crear nuestra base de datos.
Primero eliminamos cualquiera base de datos que tengo el mismo nombre que la que vamos crear para que no haya ningún conflico.
-captura0.1
![imagen](direccion)

La creamos y me diante el comando:
~~~~
use <nombredatabase>
~~~~
Nos introducimos dentro y ya podemos crear tablas.
-captura0.2

Y así con todas las tablas que el siguiente código:
~~~~sql

CREATE TABLE Departamento (
	Nome_Departamento Nome_válido,
	Teléfono char(9) NOT NULL,
	Director Nome_válido,
	CONSTRAINT PK_Departamento
		PRIMARY KEY(Nome_Departamento)
)
CREATE TABLE Ubicacion (
	Nome_Sede Nome_válido,
	Nome_Departamento Nome_válido,
	PRIMARY KEY(Nome_Sede,Nome_Departamento),
	CONSTRAINT FK_Sede_Ubicacion
		FOREIGN KEY(Nome_Sede) 
		REFERENCES "proxectoClase".sede (Nome_Sede),
		ON DELETE CASCADE
		ON UPDATE CASCADE
	CONSTRAINT FK_Departamento_Ubicacion
		FOREIGN KEY(Nome_Departamento)
		REFERENCES "proxectoClase".departamento (Nome_Departamento)
ON DELETE CASCADE
		ON UPDATE CASCADE
);
CREATE TABLE Grupo (
	Nome_Grupo Nome_válido,
	Nome_Departamento Nome_válido,
	Area Nome_válido NOT NULL,
	Líder Tipo_DNI,
	PRIMARY KEY(Nome_Grupo,Nome_Departamento),
	CONSTRAINT FK_Departamento_Grupo
		FOREIGN KEY(Nome_Departamento)
		REFERENCES "proxectoClase".departamento (Nome_Departamento)
		ON DELETE CASCADE
		ON UPDATE CASCADE
);
ALTER TABLE Proxecto ADD FOREIGN KEY (Nome_Grupo, Nome_Departamento)
REFERENCES Grupo (Nome_Grupo, Nome_Departamento) ON DELETE SET NULL ON UPDATE CASCADE;

ALTER TABLE Profesor ADD FOREIGN KEY (Nome_Grupo, Nome_Departamento)
REFERENCES Grupo (Nome_Grupo, Nome_Departamento) ON DELETE SET NULL ON UPDATE CASCADE;

ALTER TABLE Departamento
ADD CONSTRAINT fk_profesor_departamento
	FOREIGN KEY (Director) 
	REFERENCES "proxectoClase".profesor (DNI)
	ON DELETE SET NULL
	ON UPDATE CASCADE;
	
CREATE TABLE Participa (
	DNI Tipo_DNI,
	Código_Proxecto Tipo_Código,
	Data_Inicio date NOT NULL,
	Data_Cese date,
	Dedicación char(20) NOT NULL,
	PRIMARY KEY(DNI,Código_Proxecto),
	CHECK (Data_Inicio < Data_Cese)
);

CREATE TABLE Financia(
	Nome_Programa VARCHAR(30),
	Codigo_Proxecto INTEGER,
	Numero_Proxecto INTEGER NOT NULL,
	Cantidade_Financiada DECIMAL NOT NULL,
	PRIMARY KEY (Nome_Programa, Codigo_Proxecto)
);
ALTER TABLE Financia ADD FOREIGN KEY (Nome_Programa)
REFERENCES Programa (Nome_Programa) ON UPDATE CASCADE ON DELETE CASCADE;

ALTER TABLE Financia ADD FOREIGN KEY (Codigo_Proxecto)
REFERENCES Proxecto (Codigo_Proxecto) ON DELETE CASCADE ON UPDATE CASCADE;
~~~~

Una vez creada la base de datos introducirnos dentro para ver sus elementos, por ejemplo para ver las tablas creadas utilizaremos el comando:
~~~~
SHOW TABLES;
~~~~
-captura 0.3

Si queremos ver en profundidad cada tabla utilizaremos el siguiente comando:
~~~~
DESC <nombre_de_la_tabla>
~~~~
-captura 0.4


