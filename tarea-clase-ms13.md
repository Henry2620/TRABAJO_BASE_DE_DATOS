# Deber 

#TRIGGERS

## 1.- Crear una función y un trigger para validar que el numero de cedula del cliente tenga 10 números (no letras) en la tabla cliente.

## 1.1.-Función de validación.

-sentencia
```
CREATE OR REPLACE FUNCTION validar_nui(nui VARCHAR) RETURNS BOOLEAN AS $$
BEGIN
    IF LENGTH(nui) = 10 AND nui ~ '^\d+$' THEN
        RETURN TRUE;
    ELSE
        RETURN FALSE;
    END IF;
END;
$$ LANGUAGE plpgsql;
```
-captura
<img src="(1.png)" alt="drawing" width="500"/>

## 1.2.-Creamos la función para la validación de la cédula

-sentencia
```
CREATE OR REPLACE FUNCTION trigger_validar_nui() RETURNS TRIGGER AS $$
BEGIN
    IF NOT validar_nui(NEW.nui) THEN
        RAISE EXCEPTION 'El NUI debe tener exactamente 10 dígitos y no contener letras.';
    END IF;
    RETURN NEW;
END;
$$ LANGUAGE plpgsql;
```
-captura
<img src="(2.png)" alt="drawing" width="500"/>

## 1.3.-Creamos el Trigger.


-sentencia
```
CREATE TRIGGER trigger_validar_nui_before_insert
BEFORE INSERT ON client
FOR EACH ROW
EXECUTE PROCEDURE trigger_validar_nui();
```
-captura
<img src="(3.png)" alt="drawing" width="500"/>

## 1.4.-Verificamos la correcta creación del Trigger.


-sentencia
```
SELECT * 
FROM information_schema.triggers
WHERE event_object_table = 'client';
```
-captura
<img src="(4.png)" alt="drawing" width="500"/>

## 2.-Crear una función y un trigger para que cada vez que se inserte un nuevo registro en la tabla item se disminuya el stock de la tabla product.

## 2.1.-Función para actualizar el stock.

-sentencia
```
CREATE OR REPLACE FUNCTION update_stock()
RETURNS TRIGGER AS $$
BEGIN
  UPDATE productos
  SET stock = stock - NEW.quantity
  WHERE id = NEW.product_id;

  RETURN NEW;
END;
$$ LANGUAGE plpgsql;
```
-captura
<img src="(5.png)" alt="drawing" width="500"/>

## 2.2.-Creamos el Trigger para la actualización del stock.


-sentencia
```
CREATE TRIGGER update_stock
AFTER INSERT ON detail
FOR EACH ROW
EXECUTE PROCEDURE update_stock();
```
-captura
<img src="(6.png)" alt="drawing" width="500"/>

## 2.3.-Verificamos la creación del Trigger.


-sentencia
```
SELECT *
FROM information_schema.triggers
WHERE trigger_name = 'update_stock'
  AND event_object_table = 'detail';
```
-captura
<img src="(7.png)" alt="drawing" width="500"/>

## 3.- Crear una función y un trigger para la tabla invoice donde valide que el campo create_at sea del año actual (fecha sistema).

## 3.1.-Función para validar la fecha.


-sentencia
```
CREATE OR REPLACE FUNCTION validate_invoice_create_at()
RETURNS TRIGGER AS $$
BEGIN
  IF EXTRACT(YEAR FROM NEW.create_at) <> EXTRACT(YEAR FROM CURRENT_DATE) THEN
    RAISE EXCEPTION 'La fecha de creación debe ser del año actual.';
  END IF;

  RETURN NEW;
END;
$$ LANGUAGE plpgsql;
```
-captura
<img src="(8.png)" alt="drawing" width="500"/>

## 3.2.-Creamos el Trigger para la validación del año actual.


-sentencia
```
CREATE TRIGGER validate_invoice_create_at
AFTER INSERT ON invoice
FOR EACH ROW
EXECUTE PROCEDURE validate_invoice_create_at();
```
-captura
<img src="(9.png)" alt="drawing" width="500"/>

## 3.3.-Verificamos la creación del Trigger.


-sentencia
```
SELECT *
FROM information_schema.triggers
WHERE trigger_name = 'validate_invoice_create_at'
  AND event_object_table = 'invoice';
```
-captura
<img src="(10.png)" alt="drawing" width="500"/>

## 4.- Crear un función y un trigger para la tabla client y validar que el correo tenga un @.

## 4.1.-Función para la validación del correo.


-sentencia
```
CREATE OR REPLACE FUNCTION validate_email()
RETURNS TRIGGER AS $$
BEGIN
  IF NEW.email !~ '@' THEN
    RAISE EXCEPTION 'El correo electrónico debe contener un "@".';
  END IF;

  RETURN NEW;
END;
$$ LANGUAGE plpgsql;
```
-captura
<img src="(11.png)" alt="drawing" width="500"/>

## 4.2.-Creamos el Trigger para la validación del correo.


-sentencia
```
CREATE TRIGGER validate_email
AFTER INSERT ON client
FOR EACH ROW
EXECUTE PROCEDURE validate_email();
```
-captura
<img src="(12.png)" alt="drawing" width="500"/>

## 4.3.-Verificamos la creación del Trigger.


-sentencia
```
SELECT *
FROM information_schema.triggers
WHERE trigger_name = 'validate_email'
  AND event_object_table = 'client';
```
-captura
<img src="(13.png)" alt="drawing" width="500"/>



