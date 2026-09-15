# Biblioteca — Consultas SQL en DBeaver

## Descripción

En esta actividad se creó una base de datos llamada `biblioteca` y una tabla llamada `libros_lissett` para almacenar información de distintos libros.

La tabla contiene el título, autor, género, año de publicación, número de páginas, calificación y disponibilidad de cada libro. Posteriormente, se realizaron diferentes consultas SQL para filtrar, ordenar, actualizar y resumir la información almacenada.

## Tecnologías utilizadas

- DBeaver
- MySQL
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

<img width="623" height="205" alt="image" src="https://github.com/user-attachments/assets/d60f9e03-0f2e-4efc-ae08-a1c494d867ac" />


### 2. Mostrar solamente el título, autor y género

```sql
SELECT titulo, autor, genero
FROM libros_lissett;
```

<img width="372" height="191" alt="image" src="https://github.com/user-attachments/assets/6d34f1bc-c819-4d62-89da-041f262db6f4" />


### 3. Mostrar los libros disponibles

```sql
SELECT *
FROM libros_lissett
WHERE disponible = TRUE;
```

<img width="620" height="202" alt="image" src="https://github.com/user-attachments/assets/102221a8-0b23-4fab-86a2-0ac21f19dc84" />
<img width="427" height="138" alt="image" src="https://github.com/user-attachments/assets/d144ddae-7d72-486d-a26c-f798c3a261c1" />



### 4. Buscar libros de un género específico

En este ejemplo se buscan los libros del género fantasía.

```sql
SELECT *
FROM libros_lissett
WHERE genero = 'Fantasía';
```
<img width="629" height="98" alt="image" src="https://github.com/user-attachments/assets/87a3e3a4-8b09-4aa8-8469-97f0797f744f" />



### 5. Mostrar los libros publicados después del año 2000

```sql
SELECT *
FROM libros_lissett
WHERE anio_publicacion > 2000;
```

<img width="626" height="158" alt="image" src="https://github.com/user-attachments/assets/fb6f3614-ac5d-4d5f-870f-5afae03da3af" />


### 6. Mostrar los libros con calificación mayor a 8

```sql
SELECT *
FROM libros_lissett
WHERE calificacion > 8;
```

<img width="634" height="239" alt="image" src="https://github.com/user-attachments/assets/b4952fdc-7c1f-406a-8d05-693d081522c6" />


### 7. Ordenar los libros del más reciente al más antiguo

```sql
SELECT *
FROM libros_lissett
ORDER BY anio_publicacion DESC;
```

<img width="634" height="236" alt="image" src="https://github.com/user-attachments/assets/ffd377da-edc3-4645-9a1f-f318e58934c9" />


### 8. Mostrar el libro con mayor calificación

```sql
SELECT *
FROM libros_lissett
ORDER BY calificacion DESC
LIMIT 1;
```

<img width="612" height="67" alt="image" src="https://github.com/user-attachments/assets/0ffb0ae3-a66b-4d28-9edf-ff0c5c3d0d80" />


### 9. Calcular el promedio de páginas de los libros

```sql
SELECT ROUND(AVG(numero_paginas), 2) AS promedio_paginas
FROM libros_lissett;
```

<img width="491" height="77" alt="image" src="https://github.com/user-attachments/assets/870d0009-9df8-4f86-b84f-a247ae35934e" />


### 10. Contar cuántos libros existen por género

```sql
SELECT genero, COUNT(*) AS cantidad_libros
FROM libros_lissett
GROUP BY genero
ORDER BY cantidad_libros DESC;
```

<img width="248" height="219" alt="image" src="https://github.com/user-attachments/assets/ec9d218c-833f-4b39-8896-e6c1999ea881" />


### 11. Buscar títulos que contengan una palabra utilizando `LIKE`

En este ejemplo se buscan los títulos que contienen la palabra `libros`.

```sql
SELECT *
FROM libros_lissett
WHERE titulo LIKE '%libros%';
```

<img width="632" height="95" alt="image" src="https://github.com/user-attachments/assets/7551e396-3f8c-4bb6-b3fd-99d518916080" />


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

<img width="467" height="163" alt="image" src="https://github.com/user-attachments/assets/910a2428-8925-4727-81f8-575c7a094a83" />


## Conclusión

Esta actividad permitió practicar la creación de bases de datos y tablas, la inserción de registros y el uso de consultas SQL. También se utilizaron condiciones con `WHERE`, búsquedas con `LIKE`, ordenamiento con `ORDER BY`, agrupación con `GROUP BY`, funciones de agregación como `AVG` y `COUNT`, y la actualización de registros mediante `UPDATE`.

## Autora

**Lissett Zuñiga Reyes**
