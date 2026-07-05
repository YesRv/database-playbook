# 📊 Funciones Agregadas en SQL

Las funciones agregadas permiten realizar cálculos sobre un conjunto de registros y devolver un único resultado.

Son muy utilizadas para generar reportes, estadísticas y análisis de datos.

---

# 📌 Definición

Una función agregada procesa varias filas y devuelve un solo valor.

Ejemplos:

- Contar registros.
- Calcular promedios.
- Obtener el valor máximo.
- Obtener el valor mínimo.
- Calcular sumas.

---

# 🎯 ¿Para qué sirven?

Las funciones agregadas permiten responder preguntas como:

- ¿Cuántos empleados hay?
- ¿Cuál es el salario promedio?
- ¿Cuál fue la venta más alta?
- ¿Cuánto dinero se ha vendido?
- ¿Cuál es la nota máxima?

---

# 🧠 Analogía

Imagina un salón con 30 estudiantes.

En lugar de revisar uno por uno, el profesor pregunta:

- ¿Cuál fue la nota más alta?
- ¿Cuál fue el promedio?
- ¿Cuántos aprobaron?

Las funciones agregadas hacen exactamente eso con los datos.

---

# Funciones Agregadas

## COUNT()

### ¿Qué hace?

Cuenta la cantidad de registros.

### Sintaxis

```sql
SELECT COUNT(*)
FROM empleados;
```

### Ejemplo

Cantidad de empleados.

```sql
SELECT COUNT(*)
FROM empleados;
```

Resultado

```
50
```

También puedes contar una columna específica.

```sql
SELECT COUNT(correo)
FROM empleados;
```

Solo contará los registros donde el correo NO sea NULL.

---

## SUM()

### ¿Qué hace?

Suma todos los valores de una columna numérica.

### Sintaxis

```sql
SELECT SUM(salario)
FROM empleados;
```

Resultado

```
35000000
```

---

## AVG()

### ¿Qué hace?

Calcula el promedio de una columna numérica.

### Sintaxis

```sql
SELECT AVG(salario)
FROM empleados;
```

Resultado

```
2800000
```

---

## MAX()

### ¿Qué hace?

Devuelve el valor más alto.

### Sintaxis

```sql
SELECT MAX(salario)
FROM empleados;
```

Resultado

```
4500000
```

---

## MIN()

### ¿Qué hace?

Devuelve el valor más pequeño.

### Sintaxis

```sql
SELECT MIN(salario)
FROM empleados;
```

Resultado

```
1200000
```

---

# GROUP BY

## 📌 Definición

Agrupa los registros que tienen un mismo valor en una o varias columnas.

Generalmente se utiliza junto con funciones agregadas.

---

## ¿Para qué sirve?

Permite obtener resultados por grupos.

Ejemplo:

- Promedio por curso.
- Total de ventas por ciudad.
- Cantidad de empleados por departamento.

---

## Sintaxis

```sql
SELECT columna,
       funcion_agregada(columna)
FROM tabla
GROUP BY columna;
```

---

## Ejemplo

Tabla Ventas

| vendedor | venta |
|----------|-------|
|Ana|100|
|Ana|150|
|Luis|300|
|Luis|250|

Consulta

```sql
SELECT vendedor,
       SUM(venta)
FROM ventas
GROUP BY vendedor;
```

Resultado

| vendedor | total |
|----------|-------|
|Ana|250|
|Luis|550|

---

## Otro ejemplo

Promedio de notas por curso.

```sql
SELECT curso,
       AVG(nota)
FROM inscripciones
GROUP BY curso;
```

Resultado

| curso | promedio |
|--------|-----------|
|SQL|4.6|
|Python|4.2|

---

# HAVING

## 📌 Definición

Filtra grupos creados con GROUP BY.

Es similar a WHERE, pero trabaja sobre grupos y funciones agregadas.

---

## Sintaxis

```sql
SELECT columna,
       AVG(columna2)
FROM tabla
GROUP BY columna
HAVING AVG(columna2) > valor;
```

---

## Ejemplo

Mostrar únicamente los cursos cuyo promedio sea mayor a 4.5.

```sql
SELECT curso,
       AVG(nota)
FROM inscripciones
GROUP BY curso
HAVING AVG(nota) > 4.5;
```

Resultado

| curso | promedio |
|--------|-----------|
|SQL|4.8|

---

# WHERE vs HAVING

## WHERE

Filtra registros **antes** de agrupar.

```sql
SELECT *
FROM empleados
WHERE salario > 2000000;
```

---

## HAVING

Filtra grupos **después** del GROUP BY.

```sql
SELECT departamento,
       AVG(salario)
FROM empleados
GROUP BY departamento
HAVING AVG(salario) > 2500000;
```

---

# Orden de ejecución

SQL ejecuta una consulta aproximadamente en este orden:

```
FROM

↓

WHERE

↓

GROUP BY

↓

Funciones Agregadas

↓

HAVING

↓

SELECT

↓

ORDER BY

↓

LIMIT
```

Conocer este orden ayuda a entender por qué algunas consultas generan errores.

---

# Tabla resumen

| Función | Descripción |
|----------|-------------|
| COUNT() | Cuenta registros. |
| SUM() | Suma valores. |
| AVG() | Calcula el promedio. |
| MAX() | Obtiene el valor más alto. |
| MIN() | Obtiene el valor más bajo. |

---

# ⚠️ Errores comunes

## ❌ Usar GROUP BY sin necesidad

No agrupes si solo necesitas un resultado general.

---

## ❌ Olvidar el GROUP BY

Incorrecto

```sql
SELECT curso,
AVG(nota)
FROM inscripciones;
```

Correcto

```sql
SELECT curso,
AVG(nota)
FROM inscripciones
GROUP BY curso;
```

---

## ❌ Usar WHERE con funciones agregadas

Incorrecto

```sql
SELECT curso,
AVG(nota)
FROM inscripciones
WHERE AVG(nota) > 4;
```

Correcto

```sql
SELECT curso,
AVG(nota)
FROM inscripciones
GROUP BY curso
HAVING AVG(nota) > 4;
```

---

## ❌ Seleccionar columnas que no están agrupadas

Incorrecto

```sql
SELECT nombre,
curso,
AVG(nota)
FROM inscripciones
GROUP BY curso;
```

`nombre` no pertenece al GROUP BY ni está dentro de una función agregada.

---

# ✅ Buenas prácticas

- Utilizar alias para mejorar la lectura.

```sql
SELECT curso,
AVG(nota) AS promedio
FROM inscripciones
GROUP BY curso;
```

- Utilizar WHERE antes de agrupar cuando sea posible.

- Utilizar HAVING únicamente para filtrar resultados agregados.

- Evitar SELECT * cuando se utilizan agregaciones.

---

# 📝 Ejercicios

## Ejercicio 1

Mostrar la cantidad de estudiantes.

---

## Ejercicio 2

Mostrar el promedio de notas por curso.

---

## Ejercicio 3

Mostrar el salario máximo de los empleados.

---

## Ejercicio 4

Mostrar el total vendido por cada vendedor.

---

## Ejercicio 5

Mostrar únicamente los departamentos cuyo salario promedio sea mayor a 3.000.000.

---

# ✅ Soluciones

```sql
-- Ejercicio 1

SELECT COUNT(*)
FROM estudiantes;
```

```sql
-- Ejercicio 2

SELECT curso,
AVG(nota)
FROM inscripciones
GROUP BY curso;
```

```sql
-- Ejercicio 3

SELECT MAX(salario)
FROM empleados;
```

```sql
-- Ejercicio 4

SELECT vendedor,
SUM(venta)
FROM ventas
GROUP BY vendedor;
```

```sql
-- Ejercicio 5

SELECT departamento,
AVG(salario)
FROM empleados
GROUP BY departamento
HAVING AVG(salario) > 3000000;
```

---

# 🎤 Preguntas de entrevista

### ¿Cuál es la diferencia entre COUNT(*) y COUNT(columna)?

**COUNT(*)** cuenta todas las filas.

**COUNT(columna)** solo cuenta los registros donde esa columna no es NULL.

---

### ¿Cuál es la diferencia entre WHERE y HAVING?

**WHERE** filtra registros antes de agrupar.

**HAVING** filtra grupos después del GROUP BY.

---

### ¿Es obligatorio usar GROUP BY con AVG()?

No.

Solo es necesario cuando quieres calcular un promedio por grupos.

---

### ¿Qué función utilizarías para conocer el salario más alto?

MAX()

---

### ¿Qué función utilizarías para saber cuántos clientes existen?

COUNT()

---

### ¿Qué función utilizarías para conocer el promedio de notas?

AVG()

---

### ¿Qué función utilizarías para calcular el total vendido?

SUM()

---

# 📚 Resumen

- Las funciones agregadas realizan cálculos sobre varias filas y devuelven un único resultado.
- `COUNT()` cuenta registros.
- `SUM()` suma valores.
- `AVG()` calcula promedios.
- `MAX()` devuelve el valor máximo.
- `MIN()` devuelve el valor mínimo.
- `GROUP BY` agrupa registros con un mismo valor.
- `HAVING` filtra grupos después del agrupamiento.
- `WHERE` filtra registros antes de agrupar.
