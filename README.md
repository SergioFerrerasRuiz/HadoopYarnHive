# Cluster de Hadoop+YARN+Hive

Para poder desplegar un clúster de Hadoop, con YARN y Hive, sigue los siguientes pasos:

## Requisitos Previos

- Tener **Docker** y **Docker Compose** instalados.
- Un directorio de trabajo local donde estén todos los archivos necesarios, incluyendo el archivo `docker-compose.yml`, `Dockerfile` y `hadoop-hive.env` (se encuentra en este mismo repositorio de github).

## Paso a Paso para Ejecutar el Ejemplo

### 0. Preparacion

Primero situate en una direccion valida local como puede ser /user/home

```bash
cd
```
Comprueba que estas en el directorio esperado
```bash
pwd
```
Crea un directorio para guardar los archivos necesarios citados anteriormente en requisitos Previos
```bash
mkdir directorio
```
Úbicate dentro del directorio
```bash
cd directorio
```
Comprueba que estas en el directorio esperado
```bash
pwd
```
Crea los archivos necesarios con (VS) para copiar su contenido dentro:
```bash
code docker-compose.yml
```
```bash
code Dockerfile
```
```bash
code hadoop-hive.env
```

"Preparativos terminados"

### 1. Crea el Clúster de Hadoop
Asegurate de estar en el directorio esperado (directorio en el que tienes tus archivos en este caso /home/user/directorio)
```bash
pwd
```
Ejecuta el comando `docker-compose up` para crear los servicios del clúster de Hadoop. Utiliza el flag `-d` para ejecutarlos en segundo plano:

```bash
docker-compose up -d
```

### 2. Verifica que los Servicios Están Corriendo

Asegúrate de que todos los servicios necesarios estén activos:

```bash
docker ps
```

Deberías ver los contenedores en la lista (en caso de no verlos, repite los pasos y busca el error concreto).

#### En el caso de que los contenedores no corran:
verifica que el contenedor existe y esta apagado:
```bash
docker ps -a
```

Inicia el contenedor 
```bash
docker start <nombreContenedor>
```

### 3. Ejecuta el contenedor de hive para poder acceder al bash del contendor
En mi caso, "mi carpeta de contenedores" se llama hadoophive y el nodo que quiero ejecutar hive-server-1, entonces:
```bash
docker exec -it hadoophive-hive-server-1 bash
```
### 4.Acceder a sus servicios
En esta nueva terminal de bash, escribiremos hive para poder acceder a sus servicios.
```bash
hive
```

### 5. Creacion y uso de BBDD
Cremaos la BBDD
```bash
CREATE DATABASE libros;
```
Usamos la BBDD
```bash
USE libros;
```
### 6. Creacion tabla
Creamos la tbla en la BBDD
```bash
CREATE TABLE catalogo_libros (
    id INT,
    titulo STRING,
    autor STRING,
    anio_publicacion INT,
    genero STRING,
    paginas INT
);
```
### 7. Insercion Datos
Insertamos datos en la tabla
```bash
INSERT INTO catalogo_libros VALUES (1, 'Cien años de soledad', 'Gabriel García Márquez', 1967, 'Ficción', 417);
INSERT INTO catalogo_libros VALUES (2, 'Don Quijote de la Mancha', 'Miguel de Cervantes', 1605, 'Ficción', 863);
INSERT INTO catalogo_libros VALUES (3, 'El Principito', 'Antoine de Saint-Exupéry', 1943, 'Ficción', 96);
INSERT INTO catalogo_libros VALUES (4, '1984', 'George Orwell', 1949, 'Ciencia Ficción', 328);
INSERT INTO catalogo_libros VALUES (5, 'La guerra de los mundos', 'H.G. Wells', 1898, 'Ciencia Ficción', 192);
```
### 8. Consultas
Ahora realizamos algunas consultas para comprobar que Hive nos funciona.
Ver todos los libros
```bash
SELECT * FROM catalogo_libros;

```
 Contar el número total de libros
```bash
SELECT COUNT(*) AS total_libros FROM catalogo_libros;

```
Filtrar libros por género (por ejemplo, "Ficción")
```bash
SELECT * FROM catalogo_libros WHERE genero = 'Ficción';

```
Filtrar libros publicados después de 1950
```bash
SELECT * FROM catalogo_libros WHERE anio_publicacion > 1950;

```
Obtener libros ordenados por el número de páginas (de mayor a menor)
```bash
SELECT * FROM catalogo_libros ORDER BY paginas DESC;

```

# Comando para copiar un directorio de /home/usr a C:/Users/user/Desktop:
```bash
cp -r hadoopHive/ /mnt/c/Users/user/Desktop

```
Nota: user se cambia por tu nombre de usuario# HadoopYarnHive
# HadoopYarnHive
# HadoopYarnHive
