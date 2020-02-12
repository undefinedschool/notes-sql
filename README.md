> El siguiente contenido fue elaborado por [@_nhsz](https://twitter.com/_nhsz) como guía para las clases de [undefined school](https://twitter.com/undefinedSchool)

> Son bienvenidos los _issues_ y _PRs_ para mejorar el contenido, corregir errores, etc

# [WIP] Notas sobre SQL

**SQL** (**S**tructured **Q**uery **L**anguage), es un lenguaje que utilizamos para interactuar con una base de datos relacional y realizar operaciones de tipo _CRUD_ (**C**reate, **R**ead, **U**pdate, **D**elete), como crear bases de datos, crear tablas, insertar datos en estas tablas, seleccionar datos específicos que cumplan con ciertos criterios, combinar datos, eliminar datos, etc, es decir, _consultar, manipular y transformar datos de una base de datos relacional_.

👉 **SQL nos permite entonces, responder preguntas específicas sobre los datos almacenados en la DB**.

> A las _bases de datos relacionales_ también se las conoce coloquialmente como _bases de datos SQL_. Existen muchas,     SQLite, MySQL, Postgres, Oracle, Microsoft SQL Server, etc. Todas estas tienen soporte para el **standard SQL** (que es lo que  vamos   a utilizar) y además, cada implementación o _engine_ agrega sus propias features y tipos de datos (no standard).

⚠️ **Nota:** las instrucciones deben siempre terminar con `;`. Es indiferente si las escribimos en una sola línea o en varias, utilizando indentación para que resulte más legible.

Vamos a llamar _consulta_ o **_query_** a cada instrucción que termina con `;`. 

Una _query_ está compuesta por _comandos_ y _cláusulas_. 

- **Comandos:** son los que utilizamos para crear y definir nuevas bases de datos, campos e índices. También para seleccionar, insertar, eliminar y actualizar datos, generar consultas para ordenar, filtrar y extraer datos de la base de datos.
- **Cláusulas:** son condiciones de modificación utilizadas para definir los datos que desea seleccionar o manipular.

## Comandos para modificar el _schema_

### `CREATE DATABASE`

Es el _comando_ que utilizamos para crear una nueva base de datos.

```sql
CREATE DATABASE testingdb;
```

También podríamos escribir la instrucción en 2 líneas, porque lo importante es el `;`.

```sql
CREATE DATABASE 
  testingdb;
```

### `CREATE TABLE`

Es el _comando_ que utilizamos para crear una nueva tabla.

```sql
CREATE TABLE movies (
  id SERIAL PRIMARY KEY,
  title VARCHAR(100),
  overview VARCHAR,
  release_date DATE,
  remove_this CHAR(1)
);
```

### `ALTER`

Es un _comando_ que nos permite modificar una tabla.

Para **agregar una nueva columna**, usamos `ALTER` con `ADD`

```sql
ALTER TABLE
  movies
ADD
  rate DECIMAL(4, 2);
```

Para **eliminar una columna**, usamos `ALTER` con `DROP COLUMN`

```sql
ALTER TABLE
  movies
DROP COLUMN
  remove_this;
```

### `DROP`

Es un _comando_ que nos permite eliminar tablas o la base de datos entera.

Para **eliminar una tabla**, usamos `DROP TABLE`

```sql
DROP TABLE movies;
```

Para **eliminar una db**, usamos `DROP DATABASE`

```sql
DROP DATABASE testingdb;
```

## Comandos para trabajar y manipular datos

### `INSERT`

Es el _comando_ que utilizamos para insertar valores en una tabla. 

```sql
INSERT INTO 
  movies (title, overview, release_date, rate)
VALUES 
  ('Gattaca', 'In a future society in the era of indefinite eugenics, humans are set on a life course depending on their DNA. Young Vincent Freeman is born with a condition that would prevent him from space travel, yet is determined to infiltrate the GATTACA space program.', '1997-10-24', 7.50);
```

### `SELECT`

Es el _comando_ que utilizamos para **seleccionar valores de una tabla**.

Si queremos traer todas las columnas de una tabla, usamos el `*`

```sql
SELECT * FROM movies;
```

Si queremos ver sólo los títulos, tenemos que especificar la columna

```sql
SELECT title FROM movies;
```

También podemos traer varias columnas

```sql
SELECT title, rate FROM movies;
```

### `ORDER BY`

Es la _cláusula_ que utilizamos para ordenar valores por cierto campo.

Especificamos por qué campo ordenar. **Por default, ordena de forma ascendente**.

```sql
SELECT title, rate FROM movies ORDER BY rate;
```

Podemos especificar el orden agregando `ASC|DESC`

```sql
SELECT 
  title, rate 
FROM 
  movies 
ORDER BY 
  rate DESC;
```

### `WHERE`

Es la _cláusula_ que utilizamos para setear las condiciones que deben cumplir los campos que queremos seleccionar

```sql
SELECT 
  title, rate 
FROM 
  movies
WHERE
  rate > 7;
```

### `UPDATE`

Es el _comando_ que utilizamos para actualizar el valor de un campo. Se usa junto con `SET`, para especificar los valores nuevos y `WHERE`, para especificar qué campo queremos modificar.

```sql
UPDATE
  movies
SET
  rate = 8.00
WHERE
  title = 'Gattaca';
```

### `DELETE`

Es el _comando_ que utilizamos para eliminar registros de una tabla.

```sql
DELETE FROM
  movies
WHERE
  title = 'Gattaca';
```

:warning: **No te olvides de poner el `WHERE` en el `DELETE FROM`!**

[![](https://img.youtube.com/vi/i_cVJgIz_Cs/0.jpg)](https://www.youtube.com/watch?v=i_cVJgIz_Cs)
