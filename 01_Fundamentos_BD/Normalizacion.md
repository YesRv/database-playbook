# Normalización

## ¿Qué es?

Es un proceso que organiza la información para reducir redundancia y evitar inconsistencias en la base de datos.

---

## Primera Forma Normal (1FN)

Reglas:

- Cada columna debe contener un único valor.
- No se permiten listas o grupos repetidos.
- Cada fila debe ser única.

---

## Segunda Forma Normal (2FN)

Requisitos:

- Cumplir la 1FN.
- Todos los atributos deben depender completamente de la clave primaria.

---

## Tercera Forma Normal (3FN)

Requisitos:

- Cumplir la 2FN.
- No deben existir dependencias transitivas.

---

## Beneficios

- Evita duplicidad.
- Facilita mantenimiento.
- Reduce errores.
