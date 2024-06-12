#Deber de Base de Datos

## 1.Obtener la edad promedio de los miembros:
-sentencia
```
SELECT AVG(edad) AS edad_promedio
FROM Miembros;
```
-captura
<img src="Captura de pantalla 2024-06-11 235036.png" alt="drawing" width="500"/>


## 2.Obtener la edad mínima de los miembros:
-sentencia
```
SELECT MIN(edad) AS edad_minima
FROM Miembros;
```
-captura
<img src="Captura de pantalla 2024-06-11 235058.png" alt="drawing" width="500"/>


## 3.Obtener el número total de registros asistidos:
-sentencia
```
SELECT COUNT(*) AS total_registros_asistidos
FROM Registros;
```
-captura
<img src="Captura de pantalla 2024-06-11 235119.png" alt="drawing" width="500"/>


## 4.Obtener el número total de asistentes a todas las conferencias:
-sentencia
```
SELECT COUNT(DISTINCT miembro_id) AS total_asistentes
FROM Registros;
```
-captura
<img src="Captura de pantalla 2024-06-11 235138.png" alt="drawing" width="500"/>


## 5.obtener el número total de eventos por cada ciudad:
-sentencia
```
SELECT ciudad, COUNT(*) AS total_eventos
FROM Conferencias
GROUP BY ciudad;
```
-captura
<img src="Captura de pantalla 2024-06-11 235153.png" alt="drawing" width="500"/>


## 6.Obtener el número de registros por cada miembro:
-sentencia
```
SELECT miembro_id, COUNT(*) AS total_registros
FROM Registros
GROUP BY miembro_id;
```
-captura
<img src="Captura de pantalla 2024-06-11 235210.png" alt="drawing" width="500"/>


## 7.Obtener el número de registros por cada conferencia:
-sentencia
```
SELECT conferencia_id, COUNT(*) AS total_registros
FROM Registros
GROUP BY conferencia_id;
```
-captura
<img src="Captura de pantalla 2024-06-11 235412.png" alt="drawing" width="500"/>
