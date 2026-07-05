# DDL (Data Definition Language)

El DDL se utiliza para definir y modificar la estructura de una base de datos.

---

## CREATE DATABASE

Crea una nueva base de datos.

```sql
CREATE DATABASE hospital;
```

---

## CREATE TABLE

Crea una nueva tabla.

```sql
CREATE TABLE pacientes(
    id INT PRIMARY KEY,
    nombre VARCHAR(100)
);
```

---

## ALTER TABLE

Modifica una tabla existente.

```sql
ALTER TABLE pacientes
ADD telefono VARCHAR(20);
```

---

## DROP TABLE

Elimina una tabla.

```sql
DROP TABLE pacientes;
```

⚠️ Elimina la tabla y todos sus datos.

---

## TRUNCATE TABLE

Elimina todos los registros.

```sql
TRUNCATE TABLE pacientes;
```

No elimina la estructura.

---

## RENAME TABLE

Renombra una tabla.

```sql
ALTER TABLE pacientes
RENAME TO clientes;
```

---

## Buenas prácticas

✅ Crear primero las tablas padre.

✅ Definir las claves primarias antes de las foráneas.

❌ No usar DROP sin respaldo.
