# 🛡️ XSS

# 🛡️ DOM Based Cross Site Scripting (XSS)
## LOW
## 📋 Explicación
Inyectamos directamente el script y el navegador ejecuta alert(document.cookie) sin restricciones y muestra las cookies.

## 🖥️ Payload ejecutado
```bash
<script>alert(document.cookie);</script>
```
## 📸 Captura de pantalla
![a2dismod](https://github.com/PPS10711021/RA3/blob/main/RA3/RA3_2/images/xss1.png)
---

## MEDIUM
## 📋 Explicación
Estamos dentro de una etiqueta <option>, así que debemos cerrar las etiquetas (</option></select>) y luego usar una imagen falsa (<img>) con onerror para ejecutar alert(document.cookie), muestra las cookies.

## 🖥️ Payload ejecutado
```bash
" ></option></select><img src=x onerror="alert(document.cookie)">
```
## 📸 Captura de pantalla
![a2dismod](https://github.com/PPS10711021/RA3/blob/main/RA3/RA3_2/images/xss2.png)

# 🛡️ Reflected Cross Site Scripting (XSS)
## LOW
## 📋 Explicación
En el campo name, usando <img src=x onerror="alert(document.cookie)">, podemos hacer que aparezca un popup mostrando las cookies.

## 🖥️ Payload ejecutado
```bash
<img src=x onerror="alert(document.cookie)">
```
## 📸 Captura de pantalla
![a2dismod](https://github.com/PPS10711021/RA3/blob/main/RA3/RA3_2/images/xss3.png)
---

## MEDIUM
## 📋 Explicación
El mismo payload ejecutado en el nivel low nos sirve para el medium, ya que no hay filtros efectivos para evitar el ataque con imágenes y eventos onerror.

## 🖥️ Payload ejecutado
```bash
<img src=x onerror="alert(document.cookie)">
```
## 📸 Captura de pantalla
![a2dismod](https://github.com/PPS10711021/RA3/blob/main/RA3/RA3_2/images/xss4.png)

# 🛡️ Stored Cross Site Scripting (XSS)
## LOW
## 📋 Explicación
En este apartado, tenemos el campo name y message, en el name ponemos cualquier cosa, y en el mensaje ponemos el payload a ejecutar, usando el payload de abajo, logramos un popup mostrando las cookies.

## 🖥️ Payload ejecutado
```bash
<img src=x onerror="alert(document.cookie)">
```
## 📸 Captura de pantalla
![a2dismod](https://github.com/PPS10711021/RA3/blob/main/RA3/RA3_2/images/xss5.png)
---

## MEDIUM
## 📋 Explicación
En este nivel, el campo name tiene un número limitado de caracteres, por si quisieramos ejecutar el payload en esa casilla, inspeccionamos y cambiamos el maxlength a 100, para así poder jecutar el payload, además para evitar filtros de mayúsculas/minúsculas, usamos etiquetas mezcladas como <sCrIpT>...</sCrIpT>.

## 🖥️ Payload ejecutado
```bash
<sCrIpT>alert(document.cookie);</ScRiPt>
```
## 📸 Captura de pantalla
![a2dismod](https://github.com/PPS10711021/RA3/blob/main/RA3/RA3_2/images/xss6.png)
![a2dismod](https://github.com/PPS10711021/RA3/blob/main/RA3/RA3_2/images/xss7.png)

