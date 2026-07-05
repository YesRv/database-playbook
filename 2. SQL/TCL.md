# TCL (Transaction Control Language)

Permite controlar transacciones.

---

## BEGIN

```sql
BEGIN;
```

---

## COMMIT

```sql
COMMIT;
```

Guarda los cambios.

---

## ROLLBACK

```sql
ROLLBACK;
```

Revierte los cambios.

---

## SAVEPOINT

```sql
SAVEPOINT punto1;
```

---

## Ejemplo

```sql
BEGIN;

INSERT INTO pacientes VALUES (...);

SAVEPOINT sp1;

UPDATE pacientes
SET edad=30;

ROLLBACK TO sp1;

COMMIT;
```
