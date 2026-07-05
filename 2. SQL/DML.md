# DML (Data Manipulation Language)

Permite manipular los datos almacenados.

---

## INSERT

```sql
INSERT INTO pacientes(nombre,edad)
VALUES('Ana',25);
```

---

## UPDATE

```sql
UPDATE pacientes
SET edad = 26
WHERE id = 1;
```

⚠️ Nunca olvides el WHERE.

---

## DELETE

```sql
DELETE FROM pacientes
WHERE id = 5;
```

---

## Ejemplo completo

```sql
INSERT INTO pacientes(nombre,edad)
VALUES
('Juan',30),
('María',28),
('Pedro',40);
```
