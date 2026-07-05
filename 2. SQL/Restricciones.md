# Restricciones (Constraints)

Las restricciones garantizan la integridad de los datos.

| Restricción | Descripción |
|-------------|-------------|
| PRIMARY KEY | Identifica un registro de forma única. |
| FOREIGN KEY | Relaciona tablas. |
| NOT NULL | No permite valores nulos. |
| UNIQUE | No permite duplicados. |
| CHECK | Valida una condición. |
| DEFAULT | Asigna un valor por defecto. |

## Ejemplo

```sql
CREATE TABLE empleados(
    id INT PRIMARY KEY,
    correo VARCHAR(100) UNIQUE,
    salario DECIMAL CHECK (salario > 0),
    activo BOOLEAN DEFAULT TRUE
);
```
