# Modelo Relacional

## ¿Qué es?

Es la transformación del DER en tablas que serán implementadas en una base de datos relacional.

Cada entidad se convierte en una tabla.

Cada atributo en una columna.

Cada relación se representa mediante claves foráneas.

---

## Conversión

Entidad → Tabla

Atributo → Columna

Instancia → Registro

Relación → Foreign Key

---

## Ejemplo

CLIENTES

id_cliente (PK)

nombre

correo

PEDIDOS

id_pedido (PK)

fecha

id_cliente (FK)

---

## Ventajas

- Reduce redundancia.
- Facilita consultas.
- Mantiene integridad.
