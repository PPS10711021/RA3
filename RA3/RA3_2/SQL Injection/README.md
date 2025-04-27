# 🛡️ SQL Injection

## LOW
## 📋 Explicación
Al ingresar un apóstrofe (') en un campo de entrada de la aplicación, el servidor devuelve un error SQL. Esto indica que las entradas del usuario no están correctamente validadas ni saneadas, permitiendo descubrir que la aplicación es vulnerable a inyección SQL.

Utilizando un payload como ' UNION SELECT user, password FROM users#, es posible realizar una inyección SQL para unir consultas (UNION) y extraer información confidencial de la base de datos, como usuarios y contraseñas, sin necesidad de autenticación previa.

## 🖥️ Payload ejecutado
```bash
' or 1=1#
' UNION SELECT user, password FROM users#
```
## 📸 Captura de pantalla
![a2dismod](https://github.com/PPS10711021/RA3/blob/main/RA3/RA3_2/images/sql1.png)
![a2dismod](https://github.com/PPS10711021/RA3/blob/main/RA3/RA3_2/images/sql2.png)
---

## MEDIUM
## 📋 Explicación
La aplicación utiliza parámetros enviados por POST, pero agrega directamente el valor del ID a la consulta SQL sin necesidad de comillas. Esto permite realizar una inyección SQL utilizando payloads como 1 or 1=1 UNION SELECT user, password FROM users#, logrando extraer usuarios y contraseñas, incluso si las comillas han sido filtradas.

## 🖥️ Payload ejecutado
```bash
1 or 1=1 UNION SELECT user, password FROM users#
```
## 📸 Captura de pantalla
![a2dismod](https://github.com/PPS10711021/RA3/blob/main/RA3/RA3_2/images/sql3.png)
