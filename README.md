> El siguiente contenido fue elaborado por [@_nhsz](https://twitter.com/_nhsz) como guía para las clases de [undefined school](https://twitter.com/undefinedSchool)
> Son bienvenidos los _issues_ y _PRs_ para mejorar el contenido, corregir errores, etc. 

> 👉 Si te resultó útil, **se agradece que lo compartas para que le llegue a más gente!**

# [WIP] Notas sobre SQL

**SQL** (**S**tructured **Q**uery **L**anguage), es un lenguaje que utilizamos para interactuar con una base de datos relacional y realizar operaciones de tipo _CRUD_ (**C**reate, **R**ead, **U**pdate, **D**elete), como crear bases de datos, crear tablas, insertar datos en estas tablas, seleccionar datos específicos que cumplan con ciertos criterios, combinar datos, eliminar datos, etc, es decir, _consultar, manipular y transformar datos de una base de datos relacional_.

👉 **SQL nos permite entonces, responder preguntas específicas sobre los datos almacenados en la DB**.

> A las _bases de datos relacionales_ también se las conoce coloquialmente como _bases de datos SQL_. Existen muchas,     SQLite, MySQL, Postgres, Oracle, Microsoft SQL Server, etc. Todas estas tienen soporte para el **standard SQL** (que es lo que  vamos   a utilizar) y además, cada implementación o _engine_ agrega sus propias features y tipos de datos (no standard).

⚠️ **Nota:** las instrucciones deben siempre terminar con `;`. Es indiferente si las escribimos en una sola línea o en varias, utilizando indentación para que resulte más legible.

👉 Vamos a llamar _consulta_ o **_query_** a cada instrucción que termina con `;`. Una _query_ es una sentencia que _declara_ qué información estamos buscando, dónde encontrarla dentro de la base de datos (qué tabla) y opcionalmente, cómo transformar esta información antes de retornarla.

Una _query_ está compuesta por _comandos_ y _cláusulas_. 

- **Comandos:** son los que utilizamos para crear y definir nuevas bases de datos, campos e índices. También para seleccionar, insertar, eliminar y actualizar datos, generar consultas para ordenar, filtrar y extraer datos de la base de datos.
- **Cláusulas:** son condiciones de modificación utilizadas para definir los datos que desea seleccionar o manipular.

## Comandos para modificar el _schema_

### `CREATE DATABASE`

Es el _comando_ que utilizamos para **crear una nueva base de datos**.

```sql
CREATE DATABASE testingdb;
```

También podríamos escribir la instrucción en 2 líneas, porque lo importante es el `;`.

```sql
CREATE DATABASE 
  testingdb;
```

### `CREATE TABLE`

Es el _comando_ que utilizamos para **crear una nueva tabla**.

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

Es un _comando_ que nos permite **modificar una tabla**.

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

Es un _comando_ que nos permite **eliminar tablas o la base de datos entera**.

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

Es el _comando_ que utilizamos para **insertar valores en una tabla**. 

```sql
INSERT INTO 
  movies (title, overview, release_date, rate)
VALUES 
  ('Gattaca', 'In a future society in the era of indefinite eugenics, humans are set on a life course depending on their DNA. Young Vincent Freeman is born with a condition that would prevent him from space travel, yet is determined to infiltrate the GATTACA space program.', '1997-10-24', 7.50);
```

### `SELECT`

Es el _comando_ que utilizamos para **seleccionar/obtener valores de una o más tablas**.

Si queremos traer todas las columnas de la tabla `movies`, usamos el `*`

```sql
SELECT * FROM movies;
```

Si queremos ver sólo los títulos, tenemos que especificar la columna (en este caso, `title`)

```sql
SELECT title FROM movies;
```

También podemos traer varias columnas. El orden en el que las seleccionemos será el orden en el que vendrán los resultados

```sql
SELECT title, rate FROM movies;
```

### `ORDER BY`

Es la _cláusula_ que utilizamos para **ordenar valores por cierto campo**.

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

Es la _cláusula_ que utilizamos para **setear las condiciones que deben cumplir los campos que queremos seleccionar**. Nos permite **especificar las filas que nos interesan**, por lo tanto, **funciona como un filtro**

```sql
SELECT 
  title, rate 
FROM 
  movies
WHERE
  rate > 7;
```

### `LIMIT`

Es la _cláusula_ que nos permite **limitar la cantidad de resultados (filas) a mostrar**. Por ejemplo, si sólo nos interesa el primer resultado, podemos hacer

```sql
SELECT 
  title, rate 
FROM 
  movies
WHERE
  rate > 7
LIMIT 
  1;
```

### `UPDATE`

Es el _comando_ que utilizamos para **actualizar el valor de un campo**. Se usa junto con `SET`, para especificar los valores nuevos y `WHERE`, para especificar qué campo queremos modificar.

```sql
UPDATE
  movies
SET
  rate = 8.00
WHERE
  title = 'Gattaca';
```

### `DELETE`

Es el _comando_ que utilizamos para **eliminar registros de una tabla**.

```sql
DELETE FROM
  movies
WHERE
  title = 'Gattaca';
```

:warning: **No te olvides de poner el `WHERE` en el `DELETE FROM`!**

[![](https://img.youtube.com/vi/i_cVJgIz_Cs/0.jpg)](https://www.youtube.com/watch?v=i_cVJgIz_Cs)

## Alias

Podemos utilizar un _alias_ para una tabla o columna, de forma temporal. Se suelen utilizar para que el nombre de las columnas resulte más legible o descriptivo.

Un _alias_ sólo existe temporalmente, al ejecutar una _query_, no estamos modificando una tabla ni nada similar.

Por ejemplo, si queremos utilizar un alias para una columna, hacemos

```SQL
SELECT 
  column_name AS alias_name
FROM 
  table_name;
```

y si queremos utilizar un alas para una tabla, hacemos
 
```SQL
SELECT 
  column_name(s)
FROM 
  table_name AS alias_name;
```

## Funciones de agregación

Las _funciones de agregación_ nos permiten efectuar operaciones sobre un conjunto de resultados, devolviendo un único valor agregado para todos ellos, como pueden ser la cantidad de filas, máximo, mínimo, promedio, etc.

- `COUNT`: devuelve la cantidad total de filas seleccionadas por la query
- `MIN`: devuelve el mínimo del campo que especifiquemos
- `MAX`: devuelve el máximo del campo que especifiquemos
- `SUM`: suma los valores del campo que especifiquemos (sólo se puede utilizar con datos de tipo numérico)
- `AVG`: devuelve el valor promedio del campo que especifiquemos (sólo se puede utilizar con datos de tipo numérico)

Por ejemplo, si queremos saber la cantidad total de filas de la tabla `earthquake`, podemos utilizar `COUNT` con el selector `*`

```SQL
SELECT
  COUNT(*)
FROM
  earthquake;
```
