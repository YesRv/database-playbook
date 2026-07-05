# DQL (Data Query Language)

Permite consultar información.

---

## SELECT

```sql
SELECT * FROM pacientes;
```

---

## WHERE

```sql
SELECT *
FROM pacientes
WHERE edad > 30;
```

---

## ORDER BY

```sql
SELECT *
FROM pacientes
ORDER BY nombre ASC;
```

---

## LIMIT

```sql
SELECT *
FROM pacientes
LIMIT 5;
```

---

## DISTINCT

```sql
SELECT DISTINCT ciudad
FROM pacientes;
```
