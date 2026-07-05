# Diagrama Entidad-Relación (DER)

## ¿Qué es?

Es un modelo gráfico que representa cómo se relacionan las entidades de un sistema antes de crear la base de datos.

Es el primer paso del diseño de una base de datos.

---

## Componentes

### Entidad

Representa un objeto del negocio.

Ejemplos:

- Cliente
- Producto
- Empleado

---

### Atributo

Describe las características de una entidad.

Ejemplo

Empleado

- id
- nombre
- correo
- salario

---

### Relación

Indica cómo interactúan dos entidades.

Ejemplo

Un cliente realiza pedidos.

Cliente -------- Pedido

---

## Símbolos

Rectángulo → Entidad

Óvalo → Atributo

Rombo → Relación

---

## Ejemplo

Cliente

↓

Realiza

↓

Pedido

---

## Buenas prácticas

- No agregar claves foráneas en el DER.
- Representar únicamente entidades del negocio.
- Evitar relaciones redundantes.
