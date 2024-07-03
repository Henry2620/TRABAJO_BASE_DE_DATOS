# Deber 

#DB invoice

## 1.Número total de facturas realizadas por cada cliente:


-sentencia
```
SELECT c.full_name, c.adress, (SELECT COUNT(i.client_id) FROM invoice i WHERE c.id = i.client_id) FROM client c;
```
-captura
<img src="(1.png)" alt="drawing" width="500"/>

## 2.Listar nombre y correo de los clientes junto a su compra mas cara realizada:
-sentencia
```
SELECT full_name, email, (SELECT MAX(total) FROM invoice i WHERE c.id = i.client_id) FROM client c;
```
-captura
<img src="(2.png)" alt="drawing" width="500"/>

## 3.Listar las facturas donde sus totales sean mayores al promedio de las facturas:
-sentencia
```
SELECT i.create_at, i.total FROM invoice i WHERE (SELECT AVG(i.total) FROM invoice i ) < i.total;
```
-captura
<img src="(3.png)" alt="drawing" width="500"/>

#DB events

## 1.Listar una lista de conferencias, incluyendo el número total de asistentes registrados en cada conferencia:
-sentencia
```
SELECT c.id, c.title, c.speaker, c.hour, c.day,c.total_attendees, ( SELECT COUNT(*) FROM register r WHERE r.conference_id = c.id ) AS total_registered FROM conference c;
```
-captura
<img src="(4.png)" alt="drawing" width="500"/>

## 2.Listar los detalles de los miembros que asistieron a al menos una conferencia que tuvo más de 100 asistentes:
-sentencia
```
SELECT m.id, m.fullname, m.email, m.age FROM member m WHERE m.id IN ( SELECT r.member_id FROM register r JOIN conference c ON r.conference_id = c.id WHERE c.total_attendees > 50);
```
-captura
<img src="(5.png)" alt="drawing" width="500"/>