# Proyecto Retail: tablas principales con restricciones y datos iniciales

Pre-entrega 2 del curso de SQL. Crea el esquema base de un proyecto retail en PostgreSQL y carga los datos iniciales.

## Contenido

| Archivo | Descripción |
|---|---|
| `retail_project.sql` | Script único con el DDL y el DML del proyecto |

## Qué hace el script

1. Crea la base de datos `retail_project`.
2. Crea las tablas `clientes`, `productos` y `ventas`, en ese orden.
3. Carga los datos iniciales dentro de una transacción (`BEGIN ... COMMIT`).
4. Aumenta un 10 % el precio de los productos de la categoría `Electrónica` (`UPDATE` con `WHERE`).
5. Elimina una venta de prueba por su ID (`DELETE` con `WHERE`).

## Modelo

| Tabla | Clave primaria | Restricciones |
|---|---|---|
| `clientes` | `id_cliente` | `email` único y no nulo, `CHECK (edad >= 18)` |
| `productos` | `id_producto` | `CHECK (precio > 0)`, `CHECK (stock >= 0)` |
| `ventas` | `id_venta` | `FOREIGN KEY` a `clientes` y a `productos`, `CHECK (cantidad > 0)`, `CHECK (precio_unitario > 0)` |

Tipos de datos: `SERIAL` para los ID, `DECIMAL(10,2)` para dinero, `VARCHAR` para texto, `DATE` y `TIMESTAMP` para fechas.

## Cómo ejecutarlo

Requisito: PostgreSQL 12 o superior.

### Opción 1: psql (recomendada)

```bash
psql -U postgres -f retail_project.sql
```

El script crea la base de datos y se conecta a ella con `\c retail_project`.

### Opción 2: pgAdmin o DBeaver

El comando `\c` solo funciona en psql, así que:

1. Crea la base de datos `retail_project` desde la interfaz.
2. Abre una ventana de consultas conectada a esa base.
3. Ejecuta el script desde la sección `1. DDL - ESTRUCTURA DE TABLAS` en adelante.

### Volver a ejecutarlo

Las tablas se borran y se crean de nuevo en cada ejecución. Si la base de datos ya existe, `CREATE DATABASE` muestra un error que se puede ignorar: el resto del script corre normalmente.

## Resultado esperado

| Tabla | Registros finales |
|---|---|
| `clientes` | 5 |
| `productos` | 6 |
| `ventas` | 6 (se insertan 7 y se elimina la de prueba) |
