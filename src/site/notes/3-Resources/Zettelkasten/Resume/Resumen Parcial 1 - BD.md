---
{"dg-publish":true,"permalink":"/3-resources/zettelkasten/resume/resumen-parcial-1-bd/","created":"2026-05-13T21:04:23.116-03:00","updated":"2026-05-13T23:04:26.861-03:00"}
---

#  Modelo Lógico → Físico

## La pregunta clave

> Dada una relación `|A| -<R>- |B|`, ¿cómo la paso a tablas?

Hay **dos grandes caminos**:

```
¿La cardinalidad máxima de ambos lados es N?
        │
        ├── NO (al menos un lado tiene máx 1)  →  FK dentro de una tabla
        │
        └── SÍ (ambos lados son N)             →  crear tabla R
```

---

## Los 6 casos

---

### 1️⃣ (0,1) — (1,1)

```
|A|  ----0,1----<R>----1,1----  |B|
```

B **siempre** tiene un A. La FK va en B.

```
A = ( idA, atr... )
B = ( idB, atr..., idA FK )
                   ↑
              B "apunta" a A
```

---

### 2️⃣ (1,1) — (1,1)

```
|A|  ----1,1----<R>----1,1----  |B|
```

Ambos se necesitan mutuamente. La FK puede ir en cualquiera, se elige por criterio semántico.

```
A = ( idA, atr..., idB FK )     ← opción A
B = ( idB, atr... )

        ── ó ──

A = ( idA, atr... )
B = ( idB, atr..., idA FK )     ← opción B
```

---

### 3️⃣ (1,1) — (X,N)

```
|A|  ----1,1----<R>----X,N----  |B|
```

A **siempre** tiene un B, y B puede tener muchos A. La FK va en el lado 1,1.

```
A = ( idA, atr..., idB FK )
                   ↑
              A "apunta" a B
B = ( idB, atr... )
```

> [!tip] Patrón común Cuando **un lado tiene máximo 1 y mínimo 1** → la FK siempre va en ese lado, sin tabla R.

---

### 4️⃣ (0,1) — (0,1)

```
|A|  ----0,1----<R>----0,1----  |B|
```

La relación es **opcional en ambos lados**. No se puede poner la FK en A ni en B porque la relación puede no existir. Se crea tabla R, y el id de una de las dos es PK.

```
A = ( idA, atr... )
B = ( idB, atr... )
R = ( idA FK PK,  idB FK )
      ↑
  PK porque A aparece como máximo UNA vez en R
```

---

### 5️⃣ (0,1) — (X,N)

```
|A|  ----0,1----<R>----X,N----  |B|
```

La relación es **opcional del lado A**. Se crea tabla R, y el id del lado (0,1) es PK.

```
A = ( idA, atr... )
B = ( idB, atr... )
R = ( idA FK PK,  idB FK )
      ↑
  PK porque A aparece como máximo UNA vez en R
  (B puede aparecer muchas veces)
```

> [!note] ¿Por qué se parece al caso (0,1)-(0,1)? En ambos casos hay un lado con **máximo 1** y **mínimo 0**, lo que obliga a crear tabla R con ese id como PK.

---

### 6️⃣ (X,N) — (X,N)

```
|A|  ----X,N----<R>----X,N----  |B|
```

Ambos pueden aparecer **muchas veces**. Se crea tabla R con **PK compuesta** por ambos ids.

```
A = ( idA, atr... )
B = ( idB, atr... )
R = ( idA FK,  idB FK,  atr_de_R... )
     └────────────────┘
       PK compuesta: ninguno solo
       alcanza, necesitás la combinación
```

---

## 🗺️ Mapa de decisión

```
                    ┌─────────────────────────────────┐
                    │  ¿Algún lado tiene máximo = 1?  │
                    └─────────────────────────────────┘
                          │                │
                         SÍ               NO
                          │                │
                          ▼                ▼
            ┌─────────────────────┐   ┌──────────────────────┐
            │ ¿El lado con máx 1  │   │  Tabla R             │
            │ tiene mínimo = 1?   │   │  PK compuesta        │
            └─────────────────────┘   │  (idA + idB)         │
                  │         │         └──────────────────────┘
                 SÍ         NO             caso (X,N)-(X,N)
                  │          │
                  ▼          ▼
          ┌────────────┐  ┌──────────────────────┐
          │  FK en esa │  │  Tabla R             │
          │  tabla     │  │  PK = id del lado    │
          │  (sin R)   │  │  con máximo 1        │
          └────────────┘  └──────────────────────┘
          casos 1,2,3      casos 4 y 5
```

---

## 📋 Tabla resumen

|Cardinalidad|¿Tabla R?|FK / PK|
|:-:|:-:|---|
|(0,1) — (1,1)|❌|FK en el lado **(1,1)**|
|(1,1) — (1,1)|❌|FK en **cualquiera** (criterio semántico)|
|(1,1) — (X,N)|❌|FK en el lado **(1,1)**|
|(0,1) — (0,1)|✅|PK = id de **cualquiera** de los dos|
|(0,1) — (X,N)|✅|PK = id del lado **(0,1)**|
|(X,N) — (X,N)|✅|PK compuesta = **idA + idB**|

---

## ♻️ Caso especial: relación recursiva

Una entidad que se relaciona **consigo misma**.

```
        ┌──────┐
        │      │
       |A| ---<R>
```

**Ejemplo:** un empleado puede supervisar a otros empleados.

```
Empleado   = ( idEmpleado,  nombre,  ... )

Supervision = ( idEmpleado  FK,   →  el supervisado
                idSupervisor FK   →  también es un idEmpleado
                PK compuesta: (idEmpleado, idSupervisor) )
```

> [!tip] Las dos columnas de R apuntan a la **misma tabla** pero con **nombres distintos** para indicar que representan roles diferentes de la misma entidad.

# Modelo Lógico → Físico

## Concepto base

Dado un modelo lógico con dos entidades y una relación:

```
|A| -<R>- |B|
```

Al pasar al modelo físico (tablas SQL), la forma de resolver la relación **depende de la cardinalidad**. Las reglas cambian según los mínimos y máximos de cada lado.

---

## Reglas por cardinalidad

### (0,1) — (1,1)

```
|A (0,1)| -<R>- |B (1,1)|
```

**Regla:** A y B tienen sus propias tablas. La entidad con cardinalidad **(1,1) incorpora la FK** del otro como atributo más.

```
A = (idA, ...atributos)
B = (idB, ...atributos, idA (FK))
         -- B siempre tiene A, por eso lleva la FK
```

> [!tip] La FK va en el lado que **obligatoriamente** tiene al otro (el 1,1).

---

### (1,1) — (1,1)

```
|A (1,1)| -<R>- |B (1,1)|
```

**Regla:** A y B tienen sus propias tablas. **Cualquiera de las dos** incorpora la FK del otro como atributo más. Se elige por criterio semántico o de diseño.

```
A = (idA, ...atributos, idB (FK))
B = (idB, ...atributos)
```

> [!note] Como ambas son obligatorias, cualquiera puede llevar la FK. Elegís la que tenga más sentido en el dominio.

---

### (0,1) — (0,1)

```
|A (0,1)| -<R>- |B (0,1)|
```

**Regla:** A y B tienen sus propias tablas. Se crea además la **tabla R** que contiene los identificadores de ambas. El identificador de **una de las dos entidades es la PK** de R (porque la relación es como máximo uno a uno).

```
A = (idA, ...atributos)
B = (idB, ...atributos)
R = (idA (FK, PK), idB (FK))
     -- idA es PK porque cada A puede aparecer como máximo una vez en R
```

> [!warning] No se puede poner la FK directamente en A o B porque la relación es opcional en ambos lados. La tabla R solo existe cuando la relación existe.

---

### (1,1) — (X,N)

```
|A (1,1)| -<R>- |B (X,N)|
```

**Regla:** A y B tienen sus propias tablas. La entidad **(1,1) incorpora la FK** del otro como atributo más.

```
A = (idA, ...atributos, idB (FK))
B = (idB, ...atributos)
     -- A siempre tiene exactamente un B, por eso lleva la FK
```

> [!tip] Es el mismo criterio que (0,1)-(1,1): la FK va en el lado que tiene cardinalidad máxima 1.

---

### (0,1) — (X,N)

```
|A (0,1)| -<R>- |B (X,N)|
```

**Regla:** A y B tienen sus propias tablas. Se crea además la **tabla R** que contiene los identificadores de ambas. El identificador de la entidad **(0,1) es la PK** de R.

```
A = (idA, ...atributos)
B = (idB, ...atributos)
R = (idA (FK, PK), idB (FK))
     -- idA es PK porque A puede aparecer como máximo una vez en R
```

> [!note] La diferencia con (0,1)-(0,1) es que acá B puede aparecer muchas veces en R, pero A solo una vez como máximo → la PK es idA.

---

### (X,N) — (X,N)

```
|A (X,N)| -<R>- |B (X,N)|
```

**Regla:** A y B tienen sus propias tablas. Se crea además la **tabla R** que contiene los identificadores de ambas. **Ambos identificadores juntos forman la PK compuesta** de R.

```
A = (idA, ...atributos)
B = (idB, ...atributos)
R = (idA (FK), idB (FK), ...atributos de R si los hay)
     PK compuesta: (idA, idB)
```

> [!warning] La PK compuesta garantiza que no se repita la misma combinación de A y B. Ninguna de las dos FK sola es suficiente como PK porque cada entidad puede aparecer muchas veces.

---

## Resumen visual

|Cardinalidad|¿Se crea tabla R?|¿Dónde va la FK?|¿Cuál es la PK de R?|
|---|---|---|---|
|(0,1) — (1,1)|No|En el lado (1,1)|—|
|(1,1) — (1,1)|No|En cualquiera de las dos|—|
|(0,1) — (0,1)|Sí|En R|idA o idB (uno solo)|
|(1,1) — (X,N)|No|En el lado (1,1)|—|
|(0,1) — (X,N)|Sí|En R|id del lado (0,1)|
|(X,N) — (X,N)|Sí|En R|idA + idB (compuesta)|

---

## Caso especial: relación recursiva

Cuando una entidad tiene una relación **consigo misma**.

```
|A| -<R>- |A|
```

**Regla:** A tiene su propia tabla. Se crea la **tabla R** con dos columnas que referencian a A, con **nombres distintos** para diferenciar los dos roles.

**Ejemplo:** empleados donde cada empleado puede tener un supervisor (que también es empleado).

```
Empleado = (idEmpleado, nombre, ...atributos)

Supervision = (idEmpleado (FK),  →  el supervisado
               idSupervisor (FK) →  el supervisor, también es idEmpleado de Empleado
               PK compuesta: (idEmpleado, idSupervisor))
```

> [!tip] Ambas columnas de R apuntan a la **misma tabla**, pero con nombres diferentes para indicar que representan distintas instancias (roles distintos) de la misma entidad.

---

## Regla general para recordar

```
¿La cardinalidad máxima de alguno de los dos lados es 1?
  ├── Sí, de los dos lados → FK en una de las tablas (sin tabla R)
  ├── Sí, de un solo lado  → depende del mínimo del lado que tiene máx 1:
  │     ├── mínimo = 1 → FK en esa tabla (sin tabla R)
  │     └── mínimo = 0 → tabla R con ese id como PK
  └── No (ambos lados N)  → tabla R con PK compuesta (idA + idB)
```


# 📚 SQL — Resumen completo para el examen

---

## Estructura básica

```sql
SELECT lista_de_atributos   -- qué columnas mostrar
FROM lista_de_tablas        -- de qué tablas
WHERE (predicado)           -- condición (opcional)
```

---

## Orden correcto de cláusulas

```
SELECT → FROM → JOIN → WHERE → GROUP BY → HAVING → ORDER BY
```

> [!warning] `WHERE` siempre va **antes** de `GROUP BY`. `HAVING` siempre va **después**.

---

## Operadores importantes

### * y DISTINCT

```sql
-- * trae todas las columnas
SELECT * FROM producto

-- DISTINCT elimina filas repetidas
SELECT DISTINCT(codProducto)
FROM detalle
WHERE precio > 10000
```

---

### BETWEEN

Verifica si un valor está dentro de un rango. **Incluye los extremos.**

```sql
SELECT nroTicket
FROM factura
WHERE total BETWEEN 5000 AND 6000
--    equivale a: total >= 5000 AND total <= 6000
```

---

### LIKE — búsqueda de texto

|Símbolo|Significa|
|---|---|
|`%`|Cualquier cadena de caracteres (inclusive vacía)|
|`_`|Exactamente un carácter|

```sql
-- Productos cuyo nombre empieza con "Agen"
WHERE nombre LIKE 'Agen%'

-- Descripciones que contienen "za" en cualquier posición
WHERE descripcion LIKE '%za%'

-- Descripciones que dicen "utilit" seguido de exactamente 4 caracteres
WHERE descripcion LIKE 'utilit____'
```

---

### IS NULL / IS NOT NULL

```sql
-- Productos sin descripción cargada
WHERE descripcion IS NULL

-- Productos con descripción cargada
WHERE descripcion IS NOT NULL
```

> [!tip] Un campo con `?` en el esquema indica que **puede ser NULL**. Ejemplo: `fechaUsoReal?` → se verifica con `IS NULL` o `IS NOT NULL`.

---

### AS — renombrar columnas o tablas

```sql
SELECT f.nroTicket AS ticket, f.total AS totalCompra
FROM factura f     -- alias de tabla
```

---

### ORDER BY

Ordena el resultado. Por defecto es **ASC** (menor a mayor).

```sql
ORDER BY nombre ASC          -- de A a Z
ORDER BY precio_unitario DESC -- de mayor a menor

-- Se pueden combinar: primero ordena por nombre,
-- si empatan, ordena esos por precio DESC
ORDER BY nombre, precio_unitario DESC
```

---

### Operaciones en el SELECT

Los atributos pueden tener operaciones matemáticas directamente.

```sql
-- Calcular el IVA de cada factura
SELECT nroTicket, total * 0.21
FROM factura
WHERE YEAR(fecha) = 2020
```

---

## Funciones de fecha

|Función|Qué devuelve|
|---|---|
|`YEAR(fecha)`|El año|
|`MONTH(fecha)`|El mes (número)|
|`GETDATE()`|La fecha actual (SQL Server)|
|`CURDATE()`|La fecha actual (MySQL)|

```sql
-- Ventas de mayo de 2020
WHERE YEAR(f.fecha) = 2020 AND MONTH(f.fecha) = 5

-- Ventas del año actual
WHERE YEAR(f.fecha) = YEAR(GETDATE())
```

---

## Funciones de agregación

Operan sobre un grupo de filas y devuelven **un único valor**.

|Función|Qué hace|
|---|---|
|`COUNT(*)`|Cantidad de filas|
|`SUM(col)`|Suma de los valores|
|`AVG(col)`|Promedio|
|`MAX(col)`|Valor máximo|
|`MIN(col)`|Valor mínimo|

> [!warning] Nunca escribas `COUNT(tabla.*)`. Siempre es `COUNT(*)`.

---

## GROUP BY + HAVING

Agrupa filas para aplicar funciones de agregación.

```sql
SELECT nombre, COUNT(*) AS cantidad
FROM producto p
INNER JOIN detalle d ON p.codigo = d.codProducto
GROUP BY p.codigo, p.nombre
HAVING COUNT(*) > 10
```

> [!tip] Regla de oro **Toda columna del SELECT que no sea una función debe estar en el GROUP BY.**

**Diferencia WHERE vs HAVING:**

- `WHERE` filtra filas **antes** de agrupar
- `HAVING` filtra grupos **después** de agrupar

---

## Tipos de JOIN

### INNER JOIN

Solo trae filas que **coinciden en ambas tablas**.

```sql
FROM producto p
INNER JOIN detalle d ON p.codigo = d.codProducto
```

> `JOIN` solo = `INNER JOIN`. Son equivalentes.

---

### LEFT JOIN

Trae **todo de la tabla izquierda**, aunque no haya coincidencia. Lo que no coincide llega como NULL.

```sql
-- Todos los productos, aunque no tengan ventas
SELECT nombre, COUNT(d.idFactura) AS cant_facturas
FROM producto p
LEFT JOIN detalle d ON p.codigo = d.codProducto
GROUP BY p.codigo, nombre, descripcion
```

> [!tip] ¿Cuándo usar LEFT JOIN en vez de INNER JOIN? Cuando querés que aparezcan filas aunque no tengan datos en la otra tabla. En el ejemplo: si un producto nunca se vendió, igual aparece con `cant_facturas = 0`.

---

### RIGHT JOIN

Es el espejo del LEFT JOIN. Trae todo de la tabla **derecha**.

---

### Resumen visual

```
Tabla A          Tabla B
[ 1, 2, 3 ]    [ 1, 2, 99 ]

INNER JOIN  →  solo [ 1, 2 ]         (intersección)
LEFT JOIN   →  [ 1, 2, 3 ]           (todo A)
RIGHT JOIN  →  [ 1, 2, 99 ]          (todo B)
```

---

### ¿Importa el orden en INNER JOIN?

**No.** `A INNER JOIN B` = `B INNER JOIN A`. El resultado es idéntico.

En `LEFT/RIGHT JOIN` sí importa porque define cuál tabla es "la principal".

---

## Subconsultas

Una consulta dentro de otra. Operadores disponibles:

|Operador|Uso|
|---|---|
|`= valor`|Cuando la subquery devuelve **un solo resultado**|
|`IN`|Si el valor pertenece al conjunto devuelto|
|`NOT IN`|Si el valor **no** pertenece al conjunto|
|`=SOME`|Igual a alguno del conjunto|
|`>ALL`|Mayor que todos del conjunto|
|`EXISTS`|Si la subquery devuelve **al menos una fila**|
|`NOT EXISTS`|Si la subquery **no devuelve ninguna fila**|

```sql
-- IN: productos que alguna vez se vendieron
WHERE p.codigo IN (SELECT d.codProducto FROM detalle d)

-- NOT IN: productos que nunca se vendieron
WHERE p.codigo NOT IN (SELECT d.codProducto FROM detalle d)
```

> [!warning] `NOT IN` necesita una **columna específica**, nunca `SELECT *`. ❌ `NOT IN(SELECT * ...)` → ✅ `NOT IN(SELECT columna ...)`

---

## EXISTS / NOT EXISTS

```sql
-- EXISTS: ¿hay al menos un detalle para este producto?
WHERE EXISTS (
    SELECT 1 FROM detalle d
    WHERE d.codProducto = p.codigo
)
```

> [!tip] Siempre usá `SELECT 1` dentro de EXISTS. Es convención y más eficiente que `SELECT *`.

### Regla de visibilidad (subquery correlacionada)

> La subquery **puede ver** las tablas del nivel exterior. El nivel exterior **no puede ver** las tablas declaradas adentro. Por eso en cada `EXISTS` hay que declarar todas las tablas que se usan adentro.

---

## Operadores de conjuntos

```sql
-- UNION: une dos resultados, elimina duplicados
consulta1
UNION
consulta2

-- UNION ALL: une dos resultados, conserva duplicados
consulta1
UNION ALL
consulta2

-- INTERSECT: solo lo que aparece en ambos resultados
consulta1
INTERSECT
consulta2

-- EXCEPT: lo que está en la primera pero no en la segunda
consulta1
EXCEPT
consulta2
```

---

## ABM — Alta, Baja, Modificación

```sql
-- INSERTAR una fila
INSERT INTO tabla (col1, col2) VALUES (val1, val2)

-- ELIMINAR filas
DELETE FROM tabla
WHERE condicion

-- MODIFICAR filas
UPDATE tabla
SET col1 = valor1, col2 = valor2
WHERE condicion
```

---

## Palabras clave → estrategia

|La consigna dice...|Estrategia|
|---|---|
|"tiene X **y también** Y"|Dos `EXISTS` con `AND`|
|"**solo** tiene X"|`EXISTS` para X + `NOT EXISTS` para lo contrario|
|"**nunca** / no tiene"|`NOT EXISTS` o `NOT IN`|
|"**todos** los X"|`GROUP BY` + `HAVING COUNT(DISTINCT) = (SELECT COUNT(*) FROM tabla)`|
|"cantidad / total"|`COUNT(*)` o `SUM()` con `GROUP BY`|
|"año actual"|`YEAR(campo) = YEAR(GETDATE())`|
|"contiene el texto X"|`LIKE '%X%'`|
|"empieza con X"|`LIKE 'X%'`|
|"en el rango X a Y"|`BETWEEN X AND Y`|
|"X **o** Y"|`UNION`|
|"X **e** Y (ambos)"|`INTERSECT`|

---

## Ejercicios de ejemplo

### Esquema de los ejercicios de clase

```
Producto(codigo, nombre, descripcion, precio_unitario)
Detalle(codProducto FK, idFactura FK, cantidad, precio)
Factura(id, nroTicket, fecha, total)
```

---

### Productos vendidos en mayo de 2020

```sql
SELECT DISTINCT p.nombre
FROM producto p
INNER JOIN detalle d ON p.codigo = d.codProducto
INNER JOIN factura f ON d.idFactura = f.id
WHERE YEAR(f.fecha) = 2020 AND MONTH(f.fecha) = 5
```

---

### Monto total facturado en 2019

```sql
SELECT SUM(total) AS monto_total
FROM factura
WHERE fecha BETWEEN '2019-01-01' AND '2019-12-31'
```

---

### Facturas con descripción que contiene 'za', ordenadas por fecha

```sql
SELECT DISTINCT nroTicket, fecha, total
FROM factura f
INNER JOIN detalle d ON d.idFactura = f.id
INNER JOIN producto p ON p.codigo = d.codProducto
WHERE p.descripcion LIKE '%za%'
ORDER BY fecha
```

---

### Para cada producto: nombre, descripción y cantidad de facturas

Usa `LEFT JOIN` para incluir productos que nunca se vendieron (aparecen con 0).

```sql
SELECT nombre, descripcion, COUNT(d.idFactura) AS cant_facturas
FROM producto p
LEFT JOIN detalle d ON p.codigo = d.codProducto
GROUP BY p.codigo, nombre, descripcion
```

---

### Productos cuyo total en ventas supere $50.000.000

```sql
SELECT nombre, descripcion
FROM producto p
INNER JOIN detalle d ON p.codigo = d.codProducto
GROUP BY p.codigo, p.nombre, p.descripcion
HAVING SUM(cantidad * precio) > 50000000
```

---

### Facturas donde se vendió el producto 'X' O no se vendió el producto 'Y'

Usá `UNION` para combinar dos condiciones distintas.

```sql
-- Facturas con producto 'X'
SELECT DISTINCT nroTicket, fecha, total
FROM factura f
INNER JOIN detalle d ON d.idFactura = f.id
INNER JOIN producto p ON p.codigo = d.codProducto
WHERE p.nombre = 'X'

UNION

-- Facturas sin producto 'Y'
SELECT nroTicket, fecha, total
FROM factura f
WHERE NOT EXISTS (
    SELECT 1 FROM detalle d1
    INNER JOIN producto p1 ON p1.codigo = d1.codProducto
    WHERE f.id = d1.idFactura AND p1.nombre = 'Y'
)
```

---

### Facturas donde se vendieron AMBOS productos 'C' y 'D'

Usá `INTERSECT` para quedarte solo con lo que cumple las dos condiciones.

```sql
SELECT nroTicket, fecha, total
FROM factura f
INNER JOIN detalle d ON d.idFactura = f.id
INNER JOIN producto p ON p.codigo = d.codProducto
WHERE p.nombre = 'C'

INTERSECT

SELECT nroTicket, fecha, total
FROM factura f
INNER JOIN detalle d ON d.idFactura = f.id
INNER JOIN producto p ON p.codigo = d.codProducto
WHERE p.nombre = 'D'
```

---

### Esquema del ejercicio de canchas (de hoy)

```
Socio           = (DNI, CUIL, apellido, nombre, domicilio, telefono)
Cancha          = (id_cancha, deporte, superficie, cubierta, precio_hora)
Reserva         = (id_reserva, fechaReserva, fechaUsoTentativa, fechaUsoReal?, DNI FK)
Detalle_Reserva = (id_reserva FK, id_cancha FK, precio_final, estado_uso)
                  -- estado_uso: 'bueno', 'malo', 'regular'
```

---

### Socios con reservas no utilizadas Y también con estado 'regular'

```sql
SELECT *
FROM Socio s
WHERE EXISTS (
    SELECT 1 FROM Reserva r
    WHERE s.DNI = r.DNI
      AND r.fechaUsoReal IS NULL       -- no utilizada
)
AND EXISTS (
    SELECT 1 FROM Reserva r
    INNER JOIN Detalle_Reserva dr ON r.id_reserva = dr.id_reserva
    WHERE r.DNI = s.DNI
      AND dr.estado_uso = 'regular'
)
```

---

### Socios que SOLO tienen reservas en 2024

```sql
SELECT *
FROM Socio s
WHERE EXISTS (
    SELECT 1 FROM Reserva r
    WHERE r.DNI = s.DNI
      AND YEAR(r.fechaReserva) = 2024
)
AND NOT EXISTS (
    SELECT 1 FROM Reserva r
    WHERE r.DNI = s.DNI
      AND YEAR(r.fechaReserva) <> 2024
)
```

---

### Socios que reservaron TODAS las canchas

```sql
SELECT s.DNI, s.apellido, s.nombre
FROM Socio s
INNER JOIN Reserva r ON r.DNI = s.DNI
INNER JOIN Detalle_Reserva dr ON dr.id_reserva = r.id_reserva
GROUP BY s.DNI, s.apellido, s.nombre
HAVING COUNT(DISTINCT dr.id_cancha) = (SELECT COUNT(*) FROM Cancha)
```

---

## Errores frecuentes para no repetir

| ❌ Mal                                  | ✅ Bien                                   |
| -------------------------------------- | ---------------------------------------- |
| `EXIST(`                               | `EXISTS(` — con S                        |
| `NOT IN(SELECT * ...)`                 | `NOT IN(SELECT columna ...)`             |
| `COUNT(tabla.*)`                       | `COUNT(*)`                               |
| `WHERE` después de `HAVING`            | `WHERE` → `GROUP BY` → `HAVING`          |
| `SUM(cantidad)` para importe           | `SUM(precio_unitario * cantidad)`        |
| Usar alias de subquery afuera          | Cada subquery es independiente           |
| `THIS_YEAR(campo)`                     | `YEAR(campo) = YEAR(GETDATE())`          |
| Olvidar `GROUP BY` cuando usás `COUNT` | Toda columna no-función va en `GROUP BY` |
| Olvidar coma entre columnas del SELECT | Revisá siempre el SELECT                 |

# SQL — Resumen para el examen

## Conceptos clave

### EXISTS / NOT EXISTS

Pregunta si existe al menos una fila que cumpla la condición. No importa qué columnas devuelve, solo si hay filas o no.

```sql
-- Siempre usar SELECT 1 adentro (es convención y más eficiente)
WHERE EXISTS (SELECT 1 FROM tabla WHERE condicion)
```

> [!tip] Regla de visibilidad (subquery correlacionada) Una subquery **puede ver** las tablas del nivel exterior. El nivel exterior **no puede ver** las tablas declaradas adentro. Por eso en cada `EXISTS` hay que declarar todas las tablas que se usan adentro.

---

### Tipos de JOIN

|Tipo|Qué trae|
|---|---|
|`INNER JOIN`|Solo filas que coinciden en **ambas** tablas|
|`LEFT JOIN`|**Todo** de la tabla izquierda, NULL si no hay coincidencia|
|`RIGHT JOIN`|**Todo** de la tabla derecha, NULL si no hay coincidencia|

> [!note] `JOIN` solo = lo mismo que `INNER JOIN`. Son equivalentes.

**Sintaxis:**

```sql
FROM TablaA a
INNER JOIN TablaB b ON a.id = b.id
--                     ↑ columna que las conecta
```

---

### GROUP BY + HAVING

Se usan cuando querés aplicar funciones como `COUNT`, `SUM`, `AVG` por grupos.

```sql
SELECT columna, COUNT(*) AS cantidad
FROM tabla
WHERE condicion          -- filtra ANTES de agrupar
GROUP BY columna
HAVING COUNT(*) > 10    -- filtra DESPUÉS de agrupar
ORDER BY columna ASC
```

> [!warning] Regla importante Toda columna del `SELECT` que **no sea una función** (`COUNT`, `SUM`, etc.) **debe estar en el `GROUP BY`**.

---

### Orden correcto de cláusulas

```
SELECT → FROM → JOIN → WHERE → GROUP BY → HAVING → ORDER BY
```

---

## Palabras clave → estrategia

|La consigna dice...|Estrategia|
|---|---|
|"tiene X **y también** Y"|Dos `EXISTS` con `AND`|
|"**solo** tiene X"|`EXISTS` para X + `NOT EXISTS` para lo contrario|
|"**nunca** / no tiene"|`NOT EXISTS` o `NOT IN`|
|"**todos** los X"|`GROUP BY` + `HAVING COUNT(DISTINCT) = (SELECT COUNT(*) FROM tabla)`|
|"cantidad / total"|`COUNT(*)` o `SUM()` con `GROUP BY`|
|"año actual"|`YEAR(campo) = YEAR(GETDATE())`|

---

## Ejercicios de ejemplo

### Esquema usado en los ejercicios

```
Socio        = (DNI, CUIL, apellido, nombre, domicilio, telefono)
Cancha       = (id_cancha, deporte, superficie, cubierta, precio_hora)
Reserva      = (id_reserva, fechaReserva, fechaUsoTentativa, fechaUsoReal?, DNI (FK))
Detalle_Reserva = (id_reserva (FK), id_cancha (FK), precio_final, estado_uso)
                   -- estado_uso puede ser 'bueno', 'malo', 'regular'
```

---

### Ej 1 — Socios con reservas no utilizadas Y también con estado 'regular'

**Palabras clave:** "y también" → dos `EXISTS` separados.

"No utilizada" = `fechaUsoReal IS NULL` (el `?` en el esquema indica que puede ser nulo).

```sql
SELECT *
FROM Socio s
WHERE EXISTS (
    -- Condición A: tiene al menos una reserva no utilizada
    SELECT 1
    FROM Reserva r
    WHERE s.DNI = r.DNI
      AND r.fechaUsoReal IS NULL
)
AND EXISTS (
    -- Condición B: tiene al menos una reserva con estado 'regular'
    -- Necesita JOIN porque estado_uso está en Detalle_Reserva, no en Reserva
    SELECT 1
    FROM Reserva r
    INNER JOIN Detalle_Reserva dr ON r.id_reserva = dr.id_reserva
    WHERE r.DNI = s.DNI
      AND dr.estado_uso = 'regular'
);
```

> [!tip] ¿Por qué el JOIN solo en la condición B? `fechaUsoReal` está en `Reserva`, no hace falta ir a otra tabla. `estado_uso` está en `Detalle_Reserva`, así que hay que hacer JOIN para acceder a ella.

---

### Ej 2 — Socios que SOLO tienen reservas en 2024

**Palabra clave:** "solo" → `EXISTS` para lo que querés + `NOT EXISTS` para excluir lo contrario.

```sql
SELECT *
FROM Socio s
WHERE EXISTS (
    -- Que tenga al menos una reserva en 2024
    SELECT 1 FROM Reserva r
    WHERE r.DNI = s.DNI
      AND YEAR(r.fechaReserva) = 2024
)
AND NOT EXISTS (
    -- Que NO tenga ninguna reserva fuera de 2024
    SELECT 1 FROM Reserva r
    WHERE r.DNI = s.DNI
      AND YEAR(r.fechaReserva) <> 2024
);
```

---

### Ej 3 — Socios que reservaron TODAS las canchas

**Palabra clave:** "todos" → `GROUP BY` + `HAVING COUNT(DISTINCT) = total`.

No sabés de antemano cuántas canchas hay, pero podés preguntárselo a la base de datos con una subquery.

```sql
SELECT s.DNI, s.apellido, s.nombre
FROM Socio s
INNER JOIN Reserva r ON r.DNI = s.DNI
INNER JOIN Detalle_Reserva dr ON dr.id_reserva = r.id_reserva
GROUP BY s.DNI, s.apellido, s.nombre
HAVING COUNT(DISTINCT dr.id_cancha) = (SELECT COUNT(*) FROM Cancha);
--     ↑ canchas distintas que reservó    ↑ total de canchas que existen
```

---

### Ej 4 — Cantidad de reservas del año actual

```sql
SELECT COUNT(id_reserva) AS cantidad
FROM Reserva r
WHERE YEAR(r.fechaReserva) = YEAR(GETDATE());
-- GETDATE() = fecha actual. En MySQL usar CURDATE()
```

---

### Ej 5 — DNI, apellido, nombre y cantidad de reservas por socio

```sql
SELECT s.DNI, s.apellido, s.nombre, COUNT(r.id_reserva) AS cantidad_reservas
FROM Socio s
INNER JOIN Reserva r ON r.DNI = s.DNI
GROUP BY s.DNI, s.apellido, s.nombre;
-- Todo lo del SELECT que no es COUNT debe estar en el GROUP BY
```

---

### Ej 6 — Paquetes con más de 10 ventas en 2022 (esquema turístico)

Muestra cómo combinar `WHERE` (año), `GROUP BY` (por paquete) y `HAVING` (filtrar grupos).

```sql
SELECT pt.codP, pt.cantDias, pt.cantPersonas, pt.precio,
       pt.disponible, pt.destino, pt.detalles,
       COUNT(*) AS cantidad_ventas
FROM Compra c
INNER JOIN Detalle d ON d.ticket = c.ticket
INNER JOIN PaquetesTuristicos pt ON d.codP = pt.codP
WHERE YEAR(c.fecha) = 2022          -- primero filtrás el año
GROUP BY pt.codP, pt.cantDias, pt.cantPersonas,
         pt.precio, pt.disponible, pt.destino, pt.detalles
HAVING COUNT(*) > 10                -- después filtrás los grupos
ORDER BY pt.codP ASC;
```

---

## Errores frecuentes para no repetir

| ❌ Mal                                  | ✅ Bien                                                        |
| -------------------------------------- | ------------------------------------------------------------- |
| `EXIST(`                               | `EXISTS(` — con S                                             |
| `NOT IN(SELECT * ...)`                 | `NOT IN(SELECT columna ...)` — columna específica             |
| `COUNT(tabla.*)`                       | `COUNT(*)`                                                    |
| `WHERE` después de `HAVING`            | `WHERE` → `GROUP BY` → `HAVING`                               |
| `SUM(cantidad)` para calcular importe  | `SUM(precio_unitario * cantidad)`                             |
| Usar alias de subquery afuera          | Cada subquery es independiente, hay que redeclarar las tablas |
| `THIS_YEAR(campo)`                     | `YEAR(campo) = YEAR(GETDATE())`                               |
| Olvidar `GROUP BY` cuando usás `COUNT` | Toda columna no-función va en `GROUP BY`                      |
