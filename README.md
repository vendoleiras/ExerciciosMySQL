 # Naves Espaciales
 **1.** Hacemos login mediante el comando `mysql -u root -p` , nos pedirá la contraseña y la introducimos.
 
![Imaxe 1](https://raw.githubusercontent.com/vendoleiras/ExerciciosMySQL/master/images/1.PNG)

 **2.** Creamos la base de datos.
 
![Imaxe 2](https://raw.githubusercontent.com/vendoleiras/ExerciciosMySQL/master/images/2.PNG)

 **3.** Ponemos el siguiente comando para usarla.
 
![Imaxe 3](https://raw.githubusercontent.com/vendoleiras/ExerciciosMySQL/master/images/3.PNG)

 **4.** A partir de ahora tenemos que crear todas las tablas.
 
![Imaxe 4](https://raw.githubusercontent.com/vendoleiras/ExerciciosMySQL/master/images/4.PNG)

![Imaxe 5](https://raw.githubusercontent.com/vendoleiras/ExerciciosMySQL/master/images/5.PNG)

![Imaxe 6](https://raw.githubusercontent.com/vendoleiras/ExerciciosMySQL/master/images/6.PNG)

![Imaxe 7](https://raw.githubusercontent.com/vendoleiras/ExerciciosMySQL/master/images/7.PNG)

![Imaxe 8](https://raw.githubusercontent.com/vendoleiras/ExerciciosMySQL/master/images/8.PNG)

![Imaxe 9](https://raw.githubusercontent.com/vendoleiras/ExerciciosMySQL/master/images/9.PNG)

![Imaxe 10](https://raw.githubusercontent.com/vendoleiras/ExerciciosMySQL/master/images/10.PNG)

![Imaxe 11](https://raw.githubusercontent.com/vendoleiras/ExerciciosMySQL/master/images/1b.PNG)

![Imaxe 12](https://raw.githubusercontent.com/vendoleiras/ExerciciosMySQL/master/images/11.PNG)

 **5.** En caso de que nos olvidemos de algo podemos usar `ALTER TABLE` para añadirlo.
 
![Imaxe 6B](https://raw.githubusercontent.com/vendoleiras/ExerciciosMySQL/master/images/1c.PNG)

**6.** `show tables`

![Imaxe 13](https://raw.githubusercontent.com/vendoleiras/ExerciciosMySQL/master/images/12.PNG)

# Proxectos de Investigación
Ahora veremos otro ejemplo, para así tener más opciones. Usamos directamente un editor de texto, creamos un nuevo archivo y en él añadimos los comandos necesarios. Lo guardamos como un archivo `.sql`. Esto nos facilitará mucho el proceso.
A continuación el código que emplearemos.

``` SQL
CREATE DATABASE Proxecto_Investigacion;

USE Proxecto_Investigacion;

CREATE TABLE Sede (
Nome_Sede VARCHAR(30) PRIMARY KEY,
Campus VARCHAR(30) NOT NULL
);

CREATE TABLE Departamento (
Nome_Departamento VARCHAR(30) PRIMARY KEY,
Telefono CHAR(9) NOT NULL,
Director CHAR(9)
);

CREATE TABLE Ubicacion (
Nome_Sede VARCHAR(30),
Nome_Departamento VARCHAR(30),
PRIMARY KEY (Nome_Sede, Nome_Departamento),
CONSTRAINT FK_Sede
FOREIGN KEY (Nome_Sede)
REFERENCES Sede (Nome_Sede)
ON DELETE CASCADE
ON UPDATE CASCADE,
CONSTRAINT FK_Departamento
FOREIGN KEY (Nome_Departamento)
REFERENCES Departamento (Nome_Departamento)
ON DELETE CASCADE
ON UPDATE CASCADE
);

CREATE TABLE Grupo (
Nome_Grupo VARCHAR(30),
Nome_Departamento VARCHAR(30),
Area VARCHAR(30) NOT NULL,
Lider CHAR(9),
PRIMARY KEY (Nome_Grupo, Nome_Departamento),
FOREIGN KEY (Nome_Departamento) 
REFERENCES Departamento (Nome_Departamento)
ON DELETE CASCADE
ON UPDATE CASCADE
);

CREATE TABLE Profesor (
DNI CHAR(9) PRIMARY KEY,
Nome_Profesor VARCHAR(30) NOT NULL,
Titulacion VARCHAR(20) NOT NULL,
Experiencia INTEGER,
Nome_Grupo VARCHAR(30),
Nome_Departamento VARCHAR(30),
FOREIGN KEY (Nome_Grupo, Nome_Departamento)
REFERENCES Grupo (Nome_Grupo, Nome_Departamento)
ON DELETE SET NULL
ON UPDATE NO ACTION
);

CREATE TABLE Proxecto (
Codigo_Proxecto CHAR(5) PRIMARY KEY,
Nome_Proxecto VARCHAR(30) NOT NULL,
Orzamento DECIMAL NOT NULL,
Data_Inicio DATE NOT NULL,
Data_Fin DATE,
Nome_Grupo VARCHAR(30),
Nome_Departamento VARCHAR(30),
UNIQUE (Nome_Proxecto),
CONSTRAINT Check_Datas
CHECK (Data_Inicio < Data_Fin),
CONSTRAINT FK_Grupo_Proxecto
FOREIGN KEY (Nome_Grupo, Nome_Departamento)
REFERENCES Grupo (Nome_Grupo, Nome_Departamento)
ON DELETE SET NULL
ON UPDATE CASCADE
);

ALTER TABLE Departamento
ADD CONSTRAINT FK_Profesor_Departamento
FOREIGN KEY (Director)
REFERENCES Profesor (DNI)
ON DELETE SET NULL
ON UPDATE CASCADE;

ALTER TABLE Grupo
ADD CONSTRAINT FK_Profesor_Grupo
FOREIGN KEY (Lider)
REFERENCES Profesor (DNI)
ON DELETE SET NULL
ON UPDATE CASCADE;

CREATE TABLE Participa (
DNI CHAR(9),
Codigo_Proxecto CHAR(5),
Data_Inicio DATE NOT NULL,
Data_Cese DATE,
Dedicacion INTEGER NOT NULL,
PRIMARY KEY (DNI, Codigo_Proxecto),
CHECK (Data_Inicio < Data_Cese),
FOREIGN KEY (DNI)
REFERENCES Profesor (DNI)
ON DELETE NO ACTION
ON UPDATE CASCADE,
FOREIGN KEY (Codigo_Proxecto)
REFERENCES Proxecto (Codigo_Proxecto)
ON DELETE NO ACTION
ON UPDATE CASCADE
);

CREATE TABLE Programa (
Nome_Programa VARCHAR(30) PRIMARY KEY
);

CREATE TABLE Financia (
Nome_Programa VARCHAR(30),
Codigo_Proxecto CHAR(5),
Numero_Programa CHAR(5) NOT NULL,
Cantidade_Financiada DECIMAL NOT NULL,
PRIMARY KEY (Nome_Programa, Codigo_Proxecto)
);

ALTER TABLE Financia
ADD FOREIGN KEY (Codigo_Proxecto)
REFERENCES Proxecto (Codigo_Proxecto)
ON DELETE CASCADE
ON UPDATE CASCADE;

ALTER TABLE Financia
ADD FOREIGN KEY (Nome_Programa)
REFERENCES Programa (Nome_Programa)
ON DELETE CASCADE
ON UPDATE CASCADE;
````
![Imaxe 14](https://raw.githubusercontent.com/vendoleiras/ExerciciosMySQL/master/images/1_1.PNG)

![Imaxe 15](https://raw.githubusercontent.com/vendoleiras/ExerciciosMySQL/master/images/2_2.PNG)

![Imaxe 16](https://raw.githubusercontent.com/vendoleiras/ExerciciosMySQL/master/images/3_3.PNG)

![Imaxe 17](https://raw.githubusercontent.com/vendoleiras/ExerciciosMySQL/master/images/4_4.PNG)
