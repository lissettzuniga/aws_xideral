# Biblioteca — Consultas SQL en DBeaver

## Descripción

En esta actividad se creó una base de datos llamada `biblioteca` y una tabla llamada `libros_lissett` para almacenar información de distintos libros.

La tabla contiene el título, autor, género, año de publicación, número de páginas, calificación y disponibilidad de cada libro. Posteriormente, se realizaron diferentes consultas SQL para filtrar, ordenar, actualizar y resumir la información almacenada.

## Tecnologías utilizadas

- DBeaver
- MySQL/MariaDB
- SQL

## Estructura de la tabla

| Columna | Tipo de dato | Descripción |
| --- | --- | --- |
| `libro_id` | `INT` | Llave primaria autoincremental |
| `titulo` | `VARCHAR(150)` | Título del libro |
| `autor` | `VARCHAR(100)` | Autor del libro |
| `genero` | `VARCHAR(50)` | Género literario |
| `anio_publicacion` | `INT` | Año de publicación |
| `numero_paginas` | `INT` | Número de páginas |
| `calificacion` | `DECIMAL(3,1)` | Calificación del libro |
| `disponible` | `BOOLEAN` | Indica si el libro está disponible |

## Creación de la base de datos

```sql
CREATE DATABASE biblioteca;

USE biblioteca;
```

## Creación de la tabla

```sql
CREATE TABLE libros_lissett (
    libro_id INT AUTO_INCREMENT PRIMARY KEY,
    titulo VARCHAR(150) NOT NULL,
    autor VARCHAR(100) NOT NULL,
    genero VARCHAR(50) NOT NULL,
    anio_publicacion INT NOT NULL,
    numero_paginas INT NOT NULL,
    calificacion DECIMAL(3,1),
    disponible BOOLEAN DEFAULT TRUE
);
```

## Inserción de datos

Se insertaron diez libros de distintos géneros y años de publicación.

```sql
INSERT INTO libros_lissett
    (titulo, autor, genero, anio_publicacion, numero_paginas, calificacion, disponible)
VALUES
    ('Cien años de soledad', 'Gabriel García Márquez', 'Realismo mágico', 1967, 471, 9.5, TRUE),
    ('1984', 'George Orwell', 'Distopía', 1949, 328, 9.3, TRUE),
    ('El principito', 'Antoine de Saint-Exupéry', 'Fábula', 1943, 96, 8.9, FALSE),
    ('Harry Potter y la piedra filosofal', 'J. K. Rowling', 'Fantasía', 1997, 309, 9.1, TRUE),
    ('Los juegos del hambre', 'Suzanne Collins', 'Ciencia ficción', 2008, 374, 8.7, TRUE),
    ('La ladrona de libros', 'Markus Zusak', 'Novela histórica', 2005, 584, 9.0, FALSE),
    ('El código Da Vinci', 'Dan Brown', 'Misterio', 2003, 656, 8.2, TRUE),
    ('Bajo la misma estrella', 'John Green', 'Romance', 2012, 313, 8.5, TRUE),
    ('El psicoanalista', 'John Katzenbach', 'Suspenso', 2002, 528, 8.8, FALSE),
    ('Hábitos atómicos', 'James Clear', 'Desarrollo personal', 2018, 328, 9.2, TRUE);
```

## Consultas realizadas

### 1. Mostrar todos los libros

```sql
SELECT *
FROM libros_lissett;
```

<!-- Agrega aquí tu captura: ![Resultado de la consulta 1](capturas/consulta-01.png) -->

### 2. Mostrar solamente el título, autor y género

```sql
SELECT titulo, autor, genero
FROM libros_lissett;
```

<!-- Agrega aquí tu captura: ![Resultado de la consulta 2](capturas/consulta-02.png) -->

### 3. Mostrar los libros disponibles

```sql
SELECT *
FROM libros_lissett
WHERE disponible = TRUE;
```

<!-- Agrega aquí tu captura: ![Resultado de la consulta 3](capturas/consulta-03.png) -->

### 4. Buscar libros de un género específico

En este ejemplo se buscan los libros del género fantasía.

```sql
SELECT *
FROM libros_lissett
WHERE genero = 'Fantasía';
```

<!-- Agrega aquí tu captura: ![Resultado de la consulta 4](capturas/consulta-04.png) -->

### 5. Mostrar los libros publicados después del año 2000

```sql
SELECT *
FROM libros_lissett
WHERE anio_publicacion > 2000;
```

<!-- Agrega aquí tu captura: ![Resultado de la consulta 5](capturas/consulta-05.png) -->

### 6. Mostrar los libros con calificación mayor a 8

```sql
SELECT *
FROM libros_lissett
WHERE calificacion > 8;
```

<!-- Agrega aquí tu captura: ![Resultado de la consulta 6](capturas/consulta-06.png) -->

### 7. Ordenar los libros del más reciente al más antiguo

```sql
SELECT *
FROM libros_lissett
ORDER BY anio_publicacion DESC;
```

<!-- Agrega aquí tu captura: ![Resultado de la consulta 7](capturas/consulta-07.png) -->

### 8. Mostrar el libro con mayor calificación

```sql
SELECT *
FROM libros_lissett
ORDER BY calificacion DESC
LIMIT 1;
```

<!-- Agrega aquí tu captura: ![Resultado de la consulta 8](capturas/consulta-08.png) -->

### 9. Calcular el promedio de páginas de los libros

```sql
SELECT ROUND(AVG(numero_paginas), 2) AS promedio_paginas
FROM libros_lissett;
```

<!-- Agrega aquí tu captura: ![Resultado de la consulta 9](capturas/consulta-09.png) -->

### 10. Contar cuántos libros existen por género

```sql
SELECT genero, COUNT(*) AS cantidad_libros
FROM libros_lissett
GROUP BY genero
ORDER BY cantidad_libros DESC;
```

<!-- Agrega aquí tu captura: ![Resultado de la consulta 10](capturas/consulta-10.png) -->

### 11. Buscar títulos que contengan una palabra utilizando `LIKE`

En este ejemplo se buscan los títulos que contienen la palabra `libros`.

```sql
SELECT *
FROM libros_lissett
WHERE titulo LIKE '%libros%';
```

<!-- Agrega aquí tu captura: ![Resultado de la consulta 11](capturas/consulta-11.png) -->

### 12. Cambiar un libro de disponible a no disponible

En este ejemplo se modifica el libro con identificador `1`.

```sql
UPDATE libros_lissett
SET disponible = FALSE
WHERE libro_id = 1;
```

Para comprobar el cambio se ejecutó la siguiente consulta:

```sql
SELECT libro_id, titulo, disponible
FROM libros_lissett
WHERE libro_id = 1;
```

<!-- Agrega aquí tu captura: ![Resultado de la consulta 12](capturas/consulta-12.png) -->

## Conclusión

Esta actividad permitió practicar la creación de bases de datos y tablas, la inserción de registros y el uso de consultas SQL. También se utilizaron condiciones con `WHERE`, búsquedas con `LIKE`, ordenamiento con `ORDER BY`, agrupación con `GROUP BY`, funciones de agregación como `AVG` y `COUNT`, y la actualización de registros mediante `UPDATE`.

## Autora

**Lissett Zuñiga Reyes**
