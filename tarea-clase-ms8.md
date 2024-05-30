 #Tarea de Base de Datos 

 ## 1. Escribir una sentencia que muestre los productos que no registren su pais de origen
 -sentencia
 ```
 SELECT COUNT (*) - COUNT (country_of_origin) AS products_without_country
 FROM product;
```
-captura
<img src="capturas/Captura de pantalla 2024-05-30 153930.png" alt="drawing" width="500"/>

## Escribir una sentencia para poder visualizar el numero de clientes por ciudad 
-sentencia 
```
SELECT DISTINCT city, COUNT (city)
FROM client
GROUP BY (city)
```
-captura
<img src="capturas/Captura de pantalla 2024-05-30 155422.png" alt="drawing" width="500"/>
