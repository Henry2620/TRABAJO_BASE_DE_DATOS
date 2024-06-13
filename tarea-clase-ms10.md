## 1. Contar el número de productos de una categoría específica:
- sentencia
```
SELECT COUNT(*) AS num_productos
FROM product
WHERE category = 'Electronics';
```
- captura
<img src="Captura de pantalla 2024-06-12 200614.png" alt="drawing" width="500"/>

## 2. Contar el número de clientes en una ciudad específica.
- sentencia
```
SELECT COUNT(*) AS num_clientes
FROM client
WHERE city = 'San Antonio';
```
- captura
<img src="Captura de pantalla 2024-06-12 201046.png" alt="drawing" width="500"/>

## 3. Contar el número de productos cuyo precio está dentro de un rango específico 
- sentencia
```
SELECT COUNT(*) AS num_productos
FROM product
WHERE price BETWEEN 100 AND 300;

```
- captura
<img src="Captura de pantalla 2024-06-12 201110.png" alt="drawing" width="500"/>

## 4. Seleccionar clientes que viven en una ciudad específica y tienen un tipo de cliente específico 
- sentencia
```
SELECT *
FROM client
WHERE city = 'Los Ángeles' AND type_of_client = 'REG';

```
- captura
<img src="Captura de pantalla 2024-06-12 201129.png" alt="drawing" width="500"/>

## 5. Seleccionar productos que pertenecen a una categoría específica y cuyo precio está por encima de un valor específico
- sentencia
```
SELECT *
FROM product
WHERE category = 'Furniture' AND price > 200;
```
- captura
<img src="Captura de pantalla 2024-06-12 201146.png" alt="drawing" width="500"/>

## 6. Seleccionar productos que fueron producidos en un año específico y en un país de origen específico
- sentencia
```
SELECT *
FROM product
WHERE year_of_production = 2022 AND country_of_origin = 'China';
```
- captura
<img src="Captura de pantalla 2024-06-12 201206.png" alt="drawing" width="500"/>

## 7. Seleccionar clientes cuyo nombre completo comience con 'J'.
- sentencia
```
SELECT *
FROM client
WHERE full_name LIKE 'J%';

```
- captura
<img src="Captura de pantalla 2024-06-12 201219.png" alt="drawing" width="500"/>

## 8. Seleccionar clientes cuya ciudad contenga la letra 'a'
- sentencia
```
SELECT *
FROM client
WHERE city LIKE '%a%';
```
- captura
<img src="Captura de pantalla 2024-06-12 201231.png" alt="drawing" width="500"/>