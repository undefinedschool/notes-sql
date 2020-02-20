> El siguiente contenido fue elaborado por [@_nhsz](https://twitter.com/_nhsz) como guía para las clases de [undefined school](https://twitter.com/undefinedSchool)
> Son bienvenidos los _issues_ y _PRs_ para mejorar el contenido, corregir errores, etc. 

> 👉 Si te resultó útil, **se agradece que lo compartas para que le llegue a más gente!**

# [WIP] Notas sobre SQL

**SQL** (**S**tructured **Q**uery **L**anguage), es un lenguaje que utilizamos para interactuar con una base de datos relacional y realizar operaciones de tipo _CRUD_ (**C**reate, **R**ead, **U**pdate, **D**elete), como crear bases de datos, crear tablas, insertar datos en estas tablas, seleccionar datos específicos que cumplan con ciertos criterios, combinar datos, eliminar datos, etc, es decir, _consultar, manipular y transformar datos de una base de datos relacional_.

👉 **SQL nos permite entonces, responder preguntas específicas sobre los datos almacenados en la DB**.

> A las _bases de datos relacionales_ también se las conoce coloquialmente como _bases de datos SQL_. Existen muchas,     SQLite, MySQL, Postgres, Oracle, Microsoft SQL Server, etc. Todas estas tienen soporte para el **standard SQL** (que es lo que  vamos   a utilizar) y además, cada implementación o _engine_ agrega sus propias features y tipos de datos (no standard).

> ⚠️ **Nota:** las instrucciones deben siempre terminar con `;`. Es indiferente si las escribimos en una sola línea o en varias (SQL va a ignorar los saltos de línea, tabs y espacios), utilizando indentación para que resulte más legible.

👉 Vamos a llamar _consulta_ o **_query_** a cada instrucción que termina con `;`. Una _query_ es una sentencia que _declara_ qué información estamos buscando, dónde encontrarla dentro de la base de datos (qué tabla) y opcionalmente, cómo transformar esta información antes de retornarla.

Una _query_ está compuesta por _comandos_ y _cláusulas_. 

- **Comandos:** son los que utilizamos para crear y definir nuevas bases de datos, campos e índices. También para seleccionar, insertar, eliminar y actualizar datos, generar consultas para ordenar, filtrar y extraer datos de la base de datos.
- **Cláusulas:** son condiciones de modificación utilizadas para definir los datos que desea seleccionar o manipular. **El orden de las cláusulas importa**.

[![Introduction to SQL](https://img.youtube.com/vi/OfM5lC-7R4Y/0.jpg)](https://www.youtube.com/watch?v=OfM5lC-7R4Y&list=PLi01XoE8jYojRqM4qGBF1U90Ee1Ecb5tt)
> Ver [Introduction to SQL](https://www.youtube.com/watch?v=OfM5lC-7R4Y&list=PLi01XoE8jYojRqM4qGBF1U90Ee1Ecb5tt)

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

> 👉 **SQL no es _case sensitive_** es decir, no diferencia entre mayúsculas y minúsculas, por lo que podríamos escribir la query anterior de la forma

```sql
create database testingdb;
```

Por convención, se suele utilizar mayúsculas para comandos y cláusulas y minúsculas para el resto.

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

#### `DISTINCT`

Si queremos filtrar datos (filas) duplicados, podemos utilizar `DISTINCT` junto con `SELECT`

```SQL
SELECT DISTINCT
  cause
FROM
  earthquake;
```

### `ORDER BY`

Es la _cláusula_ que utilizamos para **ordenar valores por cierto campo**.

**Tenemos que especificar por qué columna queremos ordenar**. 

**Por default, ordena de forma ascendente**.

```sql
SELECT title, rate FROM movies ORDER BY rate;
```

Podemos especificar el orden agregando `ASC` ó `DESC` al final

```sql
SELECT 
  title, rate 
FROM 
  movies 
ORDER BY 
  rate DESC;
```

### `WHERE`

Es la _cláusula_ que utilizamos para **establecer las condiciones o criterios que deben cumplir los campos que queremos seleccionar**. Nos permite **especificar las filas que nos interesan** y por lo tanto, **funciona como un filtro**

```sql
SELECT 
  title, rate 
FROM 
  movies
WHERE
  rate > 7;
```

Combinándola con el `ORDER BY`, podemos hacer

```sql
SELECT 
  title, rate 
FROM 
  movies 
WHERE
  rate > 7
ORDER BY 
  rate DESC;
```

> 👉 Como dijimos al principio, **el orden de las cláusulas importa**: `SELECT`, `FROM`, `WHERE` y `ORDER BY` siempre deben usarse en ese orden y no en otro, sino tendremos un error de sintaxis y la instrucción no va a ejecutarse.

#### Operadores

##### `Comparación`

- mayor (`>`)
- mayor o igual (`>=`)
- menor (`<`)
- menor o igual (`<=`)
- igualdad (`=`)
- desigualdad (`!=` o `<>`)

##### `AND`

Podemos utilizar `AND` para combinar varios criterios que deben cumplirse en el `WHERE`

```sql
SELECT 
  title, rate 
FROM 
  movies
WHERE
  rate >= 3 AND rate <= 7;
```

##### `OR`

Podemos utilizar `AND` para establecer distintos criterios, de los que al menos 1 debe cumplirse en el `WHERE`

```sql
SELECT 
  title, rate 
FROM 
  movies
WHERE
  rate <= 4 OR rate >= 7;
```

##### `NOT`

##### `IN`

##### `LIKE`

##### `BETWEEN`

##### `IS/IS NOT NULL`

Representa la ausencia de valor definido. Por ejemplo, si nos interesan sólo aquellos resultados donde el valor de cierto campo no sea nulo,

```SQL
SELECT 
  column, another_column
FROM 
  mytable
WHERE 
  column IS NOT NULL;
```

Para traer resultados donde un campo es nulo, la query es análoga, esta vez utilizando `IS NULL`

```SQL
SELECT 
  column, another_column
FROM 
  mytable
WHERE 
  column IS NULL;
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

y si queremos utilizar un alias para una tabla, hacemos
 
```SQL
SELECT 
  column_name(s)
FROM 
  table_name AS alias_name;
```

Si queremos utilizar un alias con espacios, tenemos que ponerlo entre comillas (simples o dobles)
 
```SQL
SELECT 
  column_name(s)
FROM 
  table_name AS 'alias name';
```

## Comentarios

Podemos comentar código SQL agregando `--` delante. Como siempre, **el código comentado no se ejecuta**.

```sql
SELECT 
  title, rate 
FROM 
  movies;
-- WHERE rate > 7
-- LIMIT 1;
```

## Expresiones

Podemos utilizar [expresiones](https://sqlbolt.com/lesson/select_queries_with_expressions) para hacer consultas con una lógica un poco más compleja. Estas expresiones pueden por ejemplo, utilizar operaciones matemáticas de aritmética básica y operaciones con strings o fechas. **Se recomienda utilizar [alias](https://github.com/undefinedschool/notes-sql#alias) para que las expresiones resulten más legibles**.

```SQL
SELECT
  first_name,
  last_name,
  points + 10 AS total_points
FROM
  customers;
```

Los operadores aritméticos que podemos utilizar son

- suma (`+`)
- resta (`-`)
- multiplicación (`*`)
- división (`/`)
- módulo (resto de la división) (`%`)

> En las operaciones aritméticas, los operadores de multiplicación (`*`) y división (`/`) tienen precedencia sobre el resto (al igual que en JavaScript). Si queremos _forzar_ cierto orden de ejecución, podemos utilizar paréntesis.

Por ejemplo, si quisiéramos primero realizar la suma y luego la multiplicación, deberíamos hacer

```SQL
SELECT
  first_name,
  last_name,
  (points + 10) * 100
FROM
  customers;
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

Si queremos conocer el rango de fechas, podemos utilizar `MIN` y `MAX` con el selector `occurred_on`, donde este último representa la fecha en la que ocurrió el evento

```SQL
SELECT
  MIN(occurred_on), MAX(occurred_on)
FROM
  earthquake;
```
