# ![Notas sobre SQL](https://i.imgur.com/wTVGbtA.png)

### 👉 Ver [todas las notas](https://github.com/undefinedschool/notes)

## Contenido

- [Intro](https://github.com/undefinedschool/notes-sql#intro)
- [Comandos y cláusulas](https://github.com/undefinedschool/notes-sql#comandos-y-cl%C3%A1usulas)
- [DDL: Comandos para modificar el _schema_](https://github.com/undefinedschool/notes-sql/blob/master/README.md#ddl-comandos-para-modificar-el-schema)
  - [`CREATE DATABASE`](https://github.com/undefinedschool/notes-sql#create-database)
  - [`CREATE TABLE`](https://github.com/undefinedschool/notes-sql#create-table)
  - [`ALTER`](https://github.com/undefinedschool/notes-sql#alter)
  - [`DROP`](https://github.com/undefinedschool/notes-sql#drop)
- [DML: Comandos para trabajar con los datos](https://github.com/undefinedschool/notes-sql/blob/master/README.md#dml-comandos-para-trabajar-con-los-datos)
  - [CRUD](https://github.com/undefinedschool/notes-sql#crud)
  - [`INSERT`](https://github.com/undefinedschool/notes-sql#insert)
  - [`SELECT`](https://github.com/undefinedschool/notes-sql#select)
    - [`DISTINCT`](https://github.com/undefinedschool/notes-sql#distinct)
  - [`ORDER BY`](https://github.com/undefinedschool/notes-sql#order-by)
  - [`WHERE`](https://github.com/undefinedschool/notes-sql#where)
  - [`LIMIT`](https://github.com/undefinedschool/notes-sql#limit)
  - [`OFFSET`](https://github.com/undefinedschool/notes-sql#offset)
  - [`UPDATE`](https://github.com/undefinedschool/notes-sql#update)
  - [`DELETE`](https://github.com/undefinedschool/notes-sql#delete)
- [Operadores](https://github.com/undefinedschool/notes-sql#operadores)
  - [Comparación](https://github.com/undefinedschool/notes-sql#comparaci%C3%B3n)
  - [`AND`](https://github.com/undefinedschool/notes-sql#and)
  - [`OR`](https://github.com/undefinedschool/notes-sql#or)
  - [`NOT`](https://github.com/undefinedschool/notes-sql#not)
  - [`IN/NOT IN`](https://github.com/undefinedschool/notes-sql#innot-in)
  - [`LIKE`](https://github.com/undefinedschool/notes-sql#like)
  - [`BETWEEN`](https://github.com/undefinedschool/notes-sql#between)
  - [`IS/IS NOT NULL`](https://github.com/undefinedschool/notes-sql#isis-not-null)
- [`JOIN`](https://github.com/undefinedschool/notes-sql/blob/master/README.md#join)
  - [`INNER JOIN`](https://github.com/undefinedschool/notes-sql#inner-join)
  - [`LEFT JOIN`](https://github.com/undefinedschool/notes-sql#left-join)
  - [`RIGHT JOIN`](https://github.com/undefinedschool/notes-sql#right-join)
  - [`FULL JOIN`](https://github.com/undefinedschool/notes-sql#full-join)
- [Alias](https://github.com/undefinedschool/notes-sql#alias)
- [Comentarios](https://github.com/undefinedschool/notes-sql#comentarios)
- [Expresiones](https://github.com/undefinedschool/notes-sql#expresiones)
- [Funciones de agregación](https://github.com/undefinedschool/notes-sql#funciones-de-agregaci%C3%B3n)
  - [`GROUP BY`](https://github.com/undefinedschool/notes-sql#group-by)
  - [`HAVING`](https://github.com/undefinedschool/notes-sql#having)
- [Funciones](https://github.com/undefinedschool/notes-sql#funciones)
  - [`ROUND`](https://github.com/undefinedschool/notes-sql#round)
- [Índices](https://github.com/undefinedschool/notes-sql#%C3%ADndices)
- [Ejercicios](https://github.com/undefinedschool/notes-sql#ejercicios)

---

## Intro

**SQL** (**S**tructured **Q**uery **L**anguage), es un lenguaje que utilizamos para interactuar con una base de datos relacional y realizar operaciones de tipo _CRUD_ (**C**reate, **R**ead, **U**pdate, **D**elete), como crear bases de datos, crear tablas, insertar datos en estas tablas, seleccionar datos específicos que cumplan con ciertos criterios, combinar datos, eliminar datos, etc, es decir, _consultar, manipular y transformar datos de una base de datos relacional_.

👉 **SQL nos permite entonces, responder preguntas específicas sobre los datos almacenados en la DB**.

> A las _bases de datos relacionales_ también se las conoce coloquialmente como _bases de datos SQL_. Existen muchas,     SQLite, MySQL, Postgres, Oracle, Microsoft SQL Server, etc. Todas estas tienen soporte para el **standard SQL** (que es lo que  vamos   a utilizar) y además, cada implementación o _engine_ agrega sus propias features y tipos de datos (no standard).

> ⚠️ **Nota 1:** las instrucciones deben siempre terminar con `;`. Es indiferente si las escribimos en una sola línea o en varias (SQL va a ignorar los saltos de línea, tabs y espacios), utilizando indentación para que resulte más legible.

> ⚠️ **Nota 2:** debemos asegurarnos de poner todos los _strings_ dentro de comillas simples (`'`), no dobles. SQL interpreta las comillas dobles como el nombre de una tabla y las simples como un valor string.

👉 Vamos a llamar _consulta_ o **_query_** a cada instrucción que termina con `;`. Una _query_ es una sentencia que _declara_ qué información estamos buscando, dónde encontrarla dentro de la base de datos (qué tabla) y opcionalmente, cómo transformar esta información antes de retornarla.

[![Introduction to SQL](https://img.youtube.com/vi/OfM5lC-7R4Y/0.jpg)](https://www.youtube.com/watch?v=OfM5lC-7R4Y&list=PLi01XoE8jYojRqM4qGBF1U90Ee1Ecb5tt)
> Ver [Introduction to SQL](https://www.youtube.com/watch?v=OfM5lC-7R4Y&list=PLi01XoE8jYojRqM4qGBF1U90Ee1Ecb5tt)

[↑ Ir al inicio](https://github.com/undefinedschool/notes-sql/#contenido)

## Comandos y cláusulas

Una _query_ está compuesta por _comandos_ y _cláusulas_. 

- **Comandos:** son los que utilizamos para crear y definir nuevas bases de datos, campos e índices. También para seleccionar, insertar, eliminar y actualizar datos, generar consultas para ordenar, filtrar y extraer datos de la base de datos.
- **Cláusulas:** son condiciones de modificación utilizadas para definir los datos que desea seleccionar o manipular. **El orden de las cláusulas importa**.

[↑ Ir al inicio](https://github.com/undefinedschool/notes-sql/#contenido)

## DDL: Comandos para modificar el _schema_

Los comandos _DDL_ (Data Definition Language) son aquellos que utilizamos para crear, modificar y eliminar tablas, columnas y bases de datos.

[↑ Ir al inicio](https://github.com/undefinedschool/notes-sql/#contenido)

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

[↑ Ir al inicio](https://github.com/undefinedschool/notes-sql/#contenido)

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

En el ejemplo de arriba, `movies` es el nombre de la tabla que estamos creando. `id`, `title`, `overview`, `release_date` y `remove_this` son columnas que estamos definiendo en la tabla. `SERIAL`, `VARCHAR`, `CHAR` y `DATE` son ejemplos de [tipos de datos](https://github.com/undefinedschool/notes-dbs#tipos-de-datos). `PRIMARY KEY` es una _constraint_ (restricción) impuesta en la columna.

[↑ Ir al inicio](https://github.com/undefinedschool/notes-sql/#contenido)

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

Para **renombrar una columna**, usamos `ALTER` con `RENAME`

```sql
ALTER TABLE users 
RENAME COLUMN jobb TO job;
```

Para **cambiar el tipo de dato de una columna**

```SQL
ALTER TABLE post
ALTER COLUMN posted_on
SET DATA TYPE VARCHAR(100);
```

o las [_constraints_](https://github.com/undefinedschool/notes-dbs#constraints) (setear valores por default, campo no _nulleable_, etc)

```SQL
ALTER TABLE post
ALTER COLUMN posted_on
  SET DEFAULT CURRENT_TIMESTAMP;
```

```SQL
ALTER TABLE users 
ADD CONSTRAINT favorite_number NOT NULL;
```

[↑ Ir al inicio](https://github.com/undefinedschool/notes-sql/#contenido)

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

[↑ Ir al inicio](https://github.com/undefinedschool/notes-sql/#contenido)

## DML: Comandos para trabajar con los datos

Los comandos _DML_ (Data Manipulation Language) son aquellos que utilizamos para crear, leer, modificar, manipular y eliminar datos de registros (filas).

[↑ Ir al inicio](https://github.com/undefinedschool/notes-sql/#contenido)

### CRUD

Cuando realizamos [_operaciones CRUD_](https://github.com/undefinedschool/notes-apis#crud) en las filas (no columnas, tablas o bases de datos), estamos utilizando DML.

| CRUD | SQL |
| ---- | --- |
| Create | INSERT |
| Read | SELECT |
| Update | UPDATE |
| Delete | DELETE |

[↑ Ir al inicio](https://github.com/undefinedschool/notes-sql/#contenido)

### `INSERT`

Es el _comando_ que utilizamos para **insertar valores en una tabla**. 

```sql
INSERT INTO 
  movies (title, overview, release_date, rate)
VALUES 
  ('Gattaca', 'In a future society in the era of indefinite eugenics, humans are set on a life course depending on their DNA. Young Vincent Freeman is born with a condition that would prevent him from space travel, yet is determined to infiltrate the GATTACA space program.', '1997-10-24', 7.50);
```

> 👉 **Podemos insertar varias filas a la vez**, separando por comas. **Esta operación es mucho más eficiente que insertar de a una fila por vez**.

```SQL
INSERT INTO post
  (user_id, post_text)
VALUES
  (1, 'Hello, World!'),
  (2, 'Hello again, world!');
```

[↑ Ir al inicio](https://github.com/undefinedschool/notes-sql/#contenido)

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

[↑ Ir al inicio](https://github.com/undefinedschool/notes-sql/#contenido)

#### `DISTINCT`

Si queremos filtrar datos (filas) duplicados, podemos utilizar `DISTINCT` junto con `SELECT`

```SQL
SELECT DISTINCT
  cause
FROM
  earthquake;
```

[↑ Ir al inicio](https://github.com/undefinedschool/notes-sql/#contenido)

### `ORDER BY`

Es la _cláusula_ que utilizamos para **ordenar valores por cierto campo**. Si no utilizamos `ORDER BY`, el orden por default de los valores de una tabla es según el `id` de las filas.

**Tenemos que especificar por qué columna queremos ordenar**. 

**Por default, ordena de forma ascendente** (`ASC`).

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

También podemos ordenar por múltiples campos. En el siguiente ejemplo, ordenaríamos primero por `state` y luego (entre registros que tengan el mismo valor de `state`) por `first_name`, de forma descendiente. Podemos utilizar `ASC` y `DESC` de forma separada para cada campo

```SQL
SELECT *
FROM customers
ORDER BY state DESC, first_name DESC;
```

[↑ Ir al inicio](https://github.com/undefinedschool/notes-sql/#contenido)

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

[↑ Ir al inicio](https://github.com/undefinedschool/notes-sql/#contenido)

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

[↑ Ir al inicio](https://github.com/undefinedschool/notes-sql/#contenido)

### `OFFSET`

Opcionalmente (por ejemplo, si queremos utilizar [paginación](https://www.citusdata.com/blog/2016/03/30/five-ways-to-paginate/)), podemos proveer (como primer parámetro) un `OFFSET` para saltear algunos registros

Por ejemplo, si queremos limitar los resultados a 3 y saltear los primeros 6 registros, podemos hacer

```SQL
SELECT *
FROM customers
LIMIT 3 OFFSET 6;
```

[↑ Ir al inicio](https://github.com/undefinedschool/notes-sql/#contenido)

### `UPDATE`

Es el _comando_ que utilizamos para **actualizar el valor de un campo** de una tabla determinada. Se usa junto con `SET`, para especificar los valores nuevos y `WHERE`, para especificar qué campo queremos modificar.

```sql
UPDATE
  movies
SET
  rate = 8.00
WHERE
  title = 'Gattaca';
```

> ⚠️ Es importante **no olvidarnos del `WHERE`, si no vamos a modificar todas las filas de la tabla!** (salvo que estemos buscando hacer eso)

```SQL
UPDATE users SET first_name = 'Elie'; -- will update all users
UPDATE users SET first_name = 'Elie' WHERE id = 1; -- will update a user with an id of 1
```

También podemos modificar varios campos simultáneamente

```SQL
UPDATE
  secret_user
SET
  code_name = 'Neo 2.0', salary = 115000
WHERE
  user_id = 7;
```

[↑ Ir al inicio](https://github.com/undefinedschool/notes-sql/#contenido)

### `DELETE`

Es el _comando_ que utilizamos para **eliminar registros de una tabla**.

> 👉 **`DELETE` elimina registros (filas), no columnas**. Para hacer esto último, tendríamos que utilizar [`ALTER`](https://github.com/undefinedschool/notes-sql#alter) junto con `DROP COLUMN`

```sql
DELETE FROM
  movies
WHERE
  title = 'Gattaca';
```

```SQL
DELETE FROM users; -- will delete all users
DELETE FROM users WHERE id=1; -- will delete a user with an id of 1
```

> :warning: **No te olvides de poner el `WHERE` en el `DELETE FROM`!**

[![](https://img.youtube.com/vi/i_cVJgIz_Cs/0.jpg)](https://www.youtube.com/watch?v=i_cVJgIz_Cs)

[↑ Ir al inicio](https://github.com/undefinedschool/notes-sql/#contenido)

## Operadores

### Comparación

- mayor (`>`)
- mayor o igual (`>=`)
- menor (`<`)
- menor o igual (`<=`)
- igualdad (`=`)
- desigualdad (`!=` o `<>`)

[↑ Ir al inicio](https://github.com/undefinedschool/notes-sql/#contenido)

### `AND`

Podemos utilizar `AND` para **combinar varios criterios que deben cumplirse** en el `WHERE`

```sql
SELECT 
  title, rate 
FROM 
  movies
WHERE
  rate >= 3 AND rate <= 7;
```

[↑ Ir al inicio](https://github.com/undefinedschool/notes-sql/#contenido)

### `OR`

Podemos utilizar `AND` para **establecer distintos criterios, de los que al menos 1 debe cumplirse** en el `WHERE`

```sql
SELECT 
  title, rate 
FROM 
  movies
WHERE
  rate <= 4 OR rate >= 7;
```

> 👉 Al igual que en JavaScript, los diferentes operadores pueden combinarse para definir criterios más complejos

```SQL
SELECT 
  *
FROM
  customers
WHERE
  birthdate > '1990-01-01' OR points > 100;
```

[↑ Ir al inicio](https://github.com/undefinedschool/notes-sql/#contenido)

### `NOT`

Sirve para negar un criterio y obtener el opuesto, para obtener todos aquellos que no lo cumplan

```SQL
SELECT 
  *
FROM
  customers
WHERE
  NOT (birthdate > '1990-01-01' OR points > 100);
```

En este caso, la cláusula

```SQL
 NOT (birthdate > '1990-01-01' OR points > 100)
```

es equivalente a hacer
 
```SQL
WHERE birthdate <= '1990-01-01' AND points <= 100
```

porque si negamos cada parte, tenemos

```
NOT (birthdate > '1990-01-01') => (birthdate <= '1990-01-01')
NOT (OR)                       => AND 
NOT (points > 100)             => (points <= 100)
```

[↑ Ir al inicio](https://github.com/undefinedschool/notes-sql/#contenido)

### `IN/NOT IN`

Es útil cuando un campo puede matchear con varios valores posibles, algo que haríamos utilizando varios `OR`

Por ejemplo, en lugar de hacer

```SQL
SELECT *
FROM customers
WHERE state = 'VA' 
  OR state = 'MI' 
  OR state = 'FL';
```

podemos utilizar `IN` para simplificar

```SQL
SELECT *
FROM customers
WHERE state IN ('VA', 'MI', 'FL');
```

También se puede negar, para obtener el complemento. Si nos interesan aquellos `customers` que no pertenecen al estado de 'VA', 'MI' o 'FL', hacemos 

```SQL
SELECT *
FROM customers
WHERE state NOT IN ('VA', 'MI', 'FL');
```

[↑ Ir al inicio](https://github.com/undefinedschool/notes-sql/#contenido)

### `LIKE`

Sirve para **obtener aquellas filas que matcheen cierto patrón de caracteres**.

Por ejemplo, si queremos obtener todos aquellos `customers` cuyo apellido empiece con 'b', podemos hacer

```SQL
SELECT *
FROM customers
WHERE last_name LIKE 'b%'
```

El símbolo `%` significa que no nos interesan qué caracteres (ni cuántos, incluyendo 0) vengan después. El `%` puede estar en cualquier parte del patrón (al principio, entre otros caracteres o al final).

Por ejemplo, si nos interesan aquellos `customers` cuyo apellido tenga una letra 'b' en cualquier parte del apellido, podemos hacer

```SQL
SELECT *
FROM customers
WHERE last_name LIKE '%b%'
```

> 👉 Notas que estamos usando `'b%'` como patrón, es indistinto si usamos mayúsculas o minúsculas (`'b%'` o `'B%'`), no es _case sensitive_

**Si en cambio queremos indicar que antes (o después) de cierto caracter puede haber sólo una cantidad exacta, utilizamos `_`**.

Entonces si queremos obtener aquellos `customers` cuyo apellido tenga exactamente 1 caracter (cualquiera) antes de la letra 'b' y cualquier caracter después, podemos hacer

```SQL
SELECT *
FROM customers
WHERE last_name LIKE '_b%'
```

Si queremos obtener aquellos `customers` cuyo apellido tenga exactamente 5 caracteres (cualesquiera), finalizando con la letra 'b', podemos hacer

```SQL
SELECT *
FROM customers
WHERE last_name LIKE '____b'
```

En resumen:

- `%` representa cualquier cantidad de caracteres
- `_` representa 1 único caracter

> 👉 Ver más detalles sobre [PostgreSQL LIKE](https://www.postgresqltutorial.com/postgresql-like/)

[↑ Ir al inicio](https://github.com/undefinedschool/notes-sql/#contenido)

### `BETWEEN`

Se utiliza para obtener resultados que se encuentren dentro de cierto rango (numérico, fechas, etc)

```SQL
SELECT *
FROM customers
WHERE points BETWEEN 100 AND 500;
```

Esto es equivalente a hacer

```SQL
SELECT *
FROM customers
WHERE points >= 100 
  AND points <= 500;
```

> 👉 También podemos obtener el complemento (valores fuera de cierto rango) utilizando `NOT BETWEEN`.

[↑ Ir al inicio](https://github.com/undefinedschool/notes-sql/#contenido)

### `IS/IS NOT NULL`

Representa la ausencia de valor definido. Por ejemplo, si nos interesan sólo aquellos `customers` con el número de teléfono definido,

```SQL
SELECT *
FROM customers
WHERE phone IS NOT NULL;
```

Para traer resultados donde un campo es nulo, ya sea porque no nos interesa el valor de este campo o queremos saber si faltan ciertos datos, la query es análoga, esta vez utilizando `IS NULL`. Por ejemplo, si nos interesan saber a qué `customers` les falta el número de teléfono, podemos hacer

```SQL
SELECT *
FROM customers
WHERE phone IS NULL;
```

[↑ Ir al inicio](https://github.com/undefinedschool/notes-sql/#contenido)

## `JOIN`

[![SQL Joins Examples](https://img.youtube.com/vi/Jh_pvk48jHA/0.jpg)](https://www.youtube.com/watch?v=Jh_pvk48jHA)
> Ver [SQL Joins Examples](https://www.youtube.com/watch?v=Jh_pvk48jHA)

### `INNER JOIN`

También conocido simplemente como `JOIN`, retorna sólo las filas conectadas (por alguna key, definida en la _constraint_ `ON`), que matcheen en ambas tablas.

```SQL
SELECT *
FROM martian
INNER JOIN base
ON martian.base_id = base.base_id;
```

[↑ Ir al inicio](https://github.com/undefinedschool/notes-sql/#contenido)

### `LEFT JOIN`

Retorna todas las filas conectadas (por alguna key, definida en la _constraint_ `ON`), y de las que no matchean, retorna las filas de la tabla izquierda y completa con `null` las columnas de las filas de la tabla izquierda que no matchean.

[↑ Ir al inicio](https://github.com/undefinedschool/notes-sql/#contenido)

### `RIGHT JOIN`

Retorna todas las filas conectadas (por alguna key, definida en la _constraint_ `ON`), y de las que no matchean, retorna las filas de la tabla derecha y completa con `null` las columnas de las filas de la tabla derecha que no matchean.

[↑ Ir al inicio](https://github.com/undefinedschool/notes-sql/#contenido)

### `FULL JOIN`

También conocido como `FULL OUTER JOIN`. Es una combinación del `LEFT JOIN` y `RIGHT JOIN`. Retorna todas las filas, conectadas y no conectadas, tanto de la tabla izquierda como de la derecha.

Si hay filas de la tabla que se quiere _joinear_ que no matchean, se setea `NULL` en cada columna de la tabla que tenga una fila desconectada.

[↑ Ir al inicio](https://github.com/undefinedschool/notes-sql/#contenido)

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

[↑ Ir al inicio](https://github.com/undefinedschool/notes-sql/#contenido)

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

También podemos comentar varias líneas a la vez, usando `/* */`

```sql
SELECT 
  title, rate 
FROM 
  movies;
/* 
WHERE rate > 7
LIMIT 1; 
*/
```

[↑ Ir al inicio](https://github.com/undefinedschool/notes-sql/#contenido)

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

[↑ Ir al inicio](https://github.com/undefinedschool/notes-sql/#contenido)

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

[↑ Ir al inicio](https://github.com/undefinedschool/notes-sql/#contenido)

### `GROUP BY`

La cláusula `GROUP BY` sirve para agrupar las filas de los resultados obtenidos a partir del `SELECT`. Para cada grupo, podemos aplicar alguna función de agregación (por ejemplo, `SUM()` para calcular la suma de items o `COUNT()` para obtener la cantidad de items en un grupo).

`GROUP BY` debe definirse luego de las cláusulas `FROM` o `WHERE`. Luego, definimos la columna o lista de columnas, separadas por comas, por las que queremos agrupar los resultados.

```SQL
SELECT 
   column_1, 
   column_2,
   aggregate_function(column_3)
FROM 
   table_name
GROUP BY 
   column_1,
   column_2;
```

> 👉 Ver **[`PostgreSQL GROUP BY`](https://www.postgresqltutorial.com/postgresql-group-by/)**

[↑ Ir al inicio](https://github.com/undefinedschool/notes-sql/#contenido)

### `HAVING`

Sirve para setear condiciones y filtrar grupos de resultados según algún criterio (en una cláusula `GROUP BY` o funciones de agregación), similar a lo que haríamos con `WHERE`. 

Podemos utilizar `WHERE` y `HAVING` en la misma query.

> tener en cuenta que `WHERE` sólo puede utilizarse para filtrar resultados individuales (filas).

- `HAVING` filtra registros obtenidos a partir de resultados resumidos por `GROUP BY`.
- `HAVING` aplica a un conjunto resumido de registros, mientras que `WHERE` aplica a registros individuales.
- `HAVING` requiere que la cláusula `GROUP BY` esté presente.
- `WHERE` y `HAVING` pueden utilizarse en la misma query.

```SQL
SELECT COUNT(customer_id), country
FROM customers
GROUP BY country
HAVING COUNT(customer_id) > 5;
```

> 👉 Ver **[`PostgreSQL HAVING`](https://www.postgresqltutorial.com/postgresql-having/)**

[↑ Ir al inicio](https://github.com/undefinedschool/notes-sql/#contenido)

## Funciones

[↑ Ir al inicio](https://github.com/undefinedschool/notes-sql/#contenido)

### `ROUND`

> 👉 Ver **[`PostgreSQL ROUND Function`](https://www.postgresqltutorial.com/postgresql-round/)**

[↑ Ir al inicio](https://github.com/undefinedschool/notes-sql/#contenido)

## Índices

Para _indexar_ la tabla `person` por las columnas `first_name` y `last_name`, hacemos

```SQL
CREATE INDEX person_first_name_last_name_idx
ON person (first_name, last_name);
```

En este caso, el nombre del índice es `person_first_name_last_name_idx`. Como convención, se sugiere utilizar `<NOMBRE-TABLA_NOMBRE-COLUMNA(S)_idx>` para nombrar los índices.

[↑ Ir al inicio](https://github.com/undefinedschool/notes-sql/#contenido)

---

## Ejercicios

1. Práctica con [SQLBolt](https://sqlbolt.com/).
2. Completar los ejercicios de [Codewars - SQL for Beginners](https://www.codewars.com/collections/sql-for-beginners).
3. Completar los ejercicios de [SQL - CRUD Exercises](https://github.com/rithmschool/sql_curriculum_exercises/blob/master/02-crud_operators.md).
4. Completar los ejercicios de [SQL - Aggregates Exercises](https://github.com/rithmschool/sql_curriculum_exercises/blob/master/03-aggregates.md).
5. Completar los ejercicios de [SQL-  JOIN Exercises](https://github.com/rithmschool/sql_curriculum_exercises/blob/master/04-joins.md).
6. Completar los ejercicios de [SQL - Normalization Exercises](https://github.com/rithmschool/sql_curriculum_exercises/blob/master/05-normalization.md).
7. Completar los ejercicios de [SQL Assessment](https://github.com/rithmschool/sql_curriculum_exercises/blob/master/07-assessment.md).
8. Práctica en [PostgreSQL Exercises](https://pgexercises.com/gettingstarted.html).

[↑ Ir al inicio](https://github.com/undefinedschool/notes-sql/#contenido)
