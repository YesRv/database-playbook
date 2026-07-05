Incluye:

INNER JOIN
LEFT JOIN
RIGHT JOIN
FULL JOIN
SELF JOIN
CROSS JOIN

# 🔗 JOINS en SQL

Los **JOIN** permiten combinar información de dos o más tablas utilizando una columna en común, generalmente una **Primary Key (PK)** y una **Foreign Key (FK)**.

---

# 📌 Definición

Un JOIN es una operación de SQL que une registros de diferentes tablas para obtener información relacionada.

Sin los JOIN tendríamos que guardar información repetida en varias tablas, lo que iría en contra de la normalización.

---

# 🎯 ¿Para qué sirven?

Los JOIN permiten:

- Relacionar tablas.
- Evitar duplicidad de información.
- Consultar datos distribuidos en varias tablas.
- Mantener una base de datos organizada y normalizada.

---

# 🤔 ¿Qué problema resuelven?

Supongamos que tenemos estas tablas.

## Tabla Clientes

| id_cliente | nombre |
|------------|---------|
|1|Ana|
|2|Luis|
|3|Pedro|

## Tabla Pedidos

| id_pedido | id_cliente | producto |
|-----------|------------|----------|
|101|1|Mouse|
|102|2|Teclado|

La tabla **Pedidos** solo almacena el **id_cliente**, no el nombre.

Si queremos mostrar:

| Cliente | Producto |
|----------|----------|
|Ana|Mouse|
|Luis|Teclado|

Necesitamos unir ambas tablas.

---

# 🧠 Analogía

Imagina dos carpetas.

📁 Clientes

```
1 → Ana

2 → Luis

3 → Pedro
```

📁 Pedidos

```
Cliente 1 → Mouse

Cliente 2 → Teclado
```

SQL abre ambas carpetas y relaciona la información usando el identificador del cliente.

Eso es un JOIN.

---

# 📝 Sintaxis General

```sql
SELECT columnas
FROM tabla1
JOIN tabla2
ON tabla1.columna = tabla2.columna;
```

El **ON** indica la condición que utilizará SQL para unir ambas tablas.

---

# Tipos de JOIN

## 1️⃣ INNER JOIN

### ¿Qué hace?

Devuelve únicamente los registros que existen en ambas tablas.

### Sintaxis

```sql
SELECT c.nombre, p.producto
FROM clientes c
INNER JOIN pedidos p
ON c.id_cliente = p.id_cliente;
```

### Resultado

| Cliente | Producto |
|----------|----------|
|Ana|Mouse|
|Luis|Teclado|

Pedro no aparece porque no tiene pedidos.

### ¿Cuándo usarlo?

Cuando solo necesitas información que exista en ambas tablas.

Ejemplos:

- Pacientes con citas.
- Estudiantes inscritos.
- Clientes con compras.

---

## 2️⃣ LEFT JOIN

### ¿Qué hace?

Devuelve todos los registros de la tabla izquierda y únicamente los registros relacionados de la tabla derecha.

Si no existe relación, SQL devuelve **NULL**.

### Sintaxis

```sql
SELECT c.nombre, p.producto
FROM clientes c
LEFT JOIN pedidos p
ON c.id_cliente = p.id_cliente;
```

### Resultado

| Cliente | Producto |
|----------|----------|
|Ana|Mouse|
|Luis|Teclado|
|Pedro|NULL|

### ¿Cuándo usarlo?

Cuando necesitas mostrar todos los registros de la tabla principal, aunque no tengan relación.

Ejemplos:

- Todos los empleados, aunque no tengan departamento.
- Todos los estudiantes, aunque no estén inscritos.
- Todos los clientes, aunque nunca hayan comprado.

---

## 3️⃣ RIGHT JOIN

### ¿Qué hace?

Es el contrario del LEFT JOIN.

Conserva todos los registros de la tabla derecha.

### Sintaxis

```sql
SELECT c.nombre, p.producto
FROM clientes c
RIGHT JOIN pedidos p
ON c.id_cliente = p.id_cliente;
```

### ¿Cuándo usarlo?

Cuando la información más importante está en la tabla derecha.

> En la práctica se usa mucho menos, ya que normalmente basta con cambiar el orden de las tablas y usar un LEFT JOIN.

---

## 4️⃣ FULL JOIN

### ¿Qué hace?

Devuelve todos los registros de ambas tablas.

Si una fila no tiene coincidencia, los datos faltantes aparecen como **NULL**.

### Sintaxis

```sql
SELECT c.nombre, p.producto
FROM clientes c
FULL OUTER JOIN pedidos p
ON c.id_cliente = p.id_cliente;
```

### ¿Cuándo usarlo?

Cuando quieres ver absolutamente toda la información de ambas tablas.

> **Nota:** MySQL no soporta `FULL OUTER JOIN` de forma nativa. En MySQL suele simularse combinando un `LEFT JOIN` y un `RIGHT JOIN` mediante `UNION`.

---

## 5️⃣ CROSS JOIN

### ¿Qué hace?

Genera todas las combinaciones posibles entre dos tablas.

No necesita condición `ON`.

### Sintaxis

```sql
SELECT *
FROM clientes
CROSS JOIN productos;
```

Si existen:

- 3 clientes
- 4 productos

El resultado tendrá:

```
3 × 4 = 12 registros
```

### ¿Cuándo usarlo?

Cuando necesitas todas las combinaciones posibles.

Ejemplo:

- Crear horarios.
- Generar combinaciones de productos.
- Simulaciones.

---

## 6️⃣ SELF JOIN

### ¿Qué hace?

Une una tabla consigo misma.

Se utiliza cuando los datos de una misma tabla tienen una relación entre sí.

Ejemplo:

Tabla Empleados

| id | nombre | jefe_id |
|----|---------|----------|
|1|Carlos|NULL|
|2|Ana|1|
|3|Luis|1|

Consulta:

```sql
SELECT e.nombre AS Empleado,
       j.nombre AS Jefe
FROM empleados e
LEFT JOIN empleados j
ON e.jefe_id = j.id;
```

Resultado

| Empleado | Jefe |
|-----------|------|
|Carlos|NULL|
|Ana|Carlos|
|Luis|Carlos|

### ¿Cuándo usarlo?

Cuando una tabla hace referencia a sí misma.

Ejemplos:

- Empleados y jefes.
- Categorías y subcategorías.
- Comentarios y respuestas.

---

# 📊 Resumen visual

| JOIN | ¿Qué devuelve? |
|------|----------------|
| INNER JOIN | Solo coincidencias entre ambas tablas. |
| LEFT JOIN | Todos los registros de la tabla izquierda y las coincidencias de la derecha. |
| RIGHT JOIN | Todos los registros de la tabla derecha y las coincidencias de la izquierda. |
| FULL JOIN | Todos los registros de ambas tablas. |
| CROSS JOIN | Todas las combinaciones posibles. |
| SELF JOIN | Relaciona una tabla consigo misma. |

---

# ⚠️ Errores comunes

### ❌ Olvidar el ON

```sql
SELECT *
FROM clientes
INNER JOIN pedidos;
```

SQL no sabe cómo relacionar las tablas.

---

### ❌ Usar una columna incorrecta

```sql
ON clientes.nombre = pedidos.producto;
```

Las columnas relacionadas deben representar la misma información.

---

### ❌ No utilizar alias

Cuando trabajas con varias tablas es recomendable utilizar alias para hacer las consultas más legibles.

```sql
FROM clientes c
INNER JOIN pedidos p
```

---

# ✅ Buenas prácticas

- Utilizar alias (`c`, `p`, `e`, etc.) para mejorar la legibilidad.
- Relacionar tablas mediante claves primarias y foráneas.
- Seleccionar únicamente las columnas necesarias en lugar de usar `SELECT *`.
- Usar `LEFT JOIN` cuando necesites conservar todos los registros de una tabla principal.

---

# 📝 Ejercicio

Tenemos las siguientes tablas:

## Estudiantes

| id | nombre |
|----|---------|
|1|Ana|
|2|Luis|
|3|Pedro|

## Inscripciones

| id | estudiante_id | curso |
|----|---------------|--------|
|1|1|SQL|
|2|2|Python|

**Pregunta:** ¿Qué JOIN utilizarías para mostrar todos los estudiantes, incluso aquellos que no están inscritos en ningún curso?

<details>
<summary>✅ Ver respuesta</summary>

Se utiliza un **LEFT JOIN**, porque necesitamos conservar todos los estudiantes y mostrar `NULL` para aquellos que no tienen inscripciones.

```sql
SELECT e.nombre, i.curso
FROM estudiantes e
LEFT JOIN inscripciones i
ON e.id = i.estudiante_id;
```

</details>

---

# 🎤 Preguntas de entrevista

### ¿Cuál es la diferencia entre INNER JOIN y LEFT JOIN?

**INNER JOIN** devuelve únicamente los registros que tienen coincidencia en ambas tablas.

**LEFT JOIN** devuelve todos los registros de la tabla izquierda y, si no existe coincidencia, muestra `NULL` en las columnas de la tabla derecha.

---

### ¿Qué JOIN utilizarías para mostrar todos los clientes aunque nunca hayan realizado compras?

**LEFT JOIN.**

---

### ¿Qué JOIN genera todas las combinaciones posibles?

**CROSS JOIN.**

---

### ¿Qué JOIN utilizarías para relacionar empleados con sus jefes?

**SELF JOIN.**

---

### ¿Qué JOIN usarías para obtener solo los registros relacionados?

**INNER JOIN.**

---

# 📚 Resumen

- Un **JOIN** permite combinar información de varias tablas relacionadas.
- La relación normalmente se realiza mediante una **Primary Key (PK)** y una **Foreign Key (FK)**.
- El tipo de JOIN depende del resultado que necesites obtener:
  - **INNER JOIN:** solo coincidencias.
  - **LEFT JOIN:** conserva todos los registros de la tabla izquierda.
  - **RIGHT JOIN:** conserva todos los registros de la tabla derecha.
  - **FULL JOIN:** conserva todos los registros de ambas tablas.
  - **CROSS JOIN:** genera todas las combinaciones posibles.
  - **SELF JOIN:** relaciona una tabla consigo misma.
