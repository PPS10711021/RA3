# 🛡️ Content Security Policy (CSP) en Apache

## 📌 Introducción

### 🔒 ¿Qué es CSP?
Según **Mozilla Developer**, la **Política de Seguridad del Contenido** (**Content Security Policy - CSP**) es una capa de seguridad adicional que ayuda a prevenir y mitigar ataques como:

✅ **Cross Site Scripting (XSS)**
✅ **Inyección de datos**
✅ **Distribución de malware**
✅ **Desfiguración de sitios**

### 🛠️ ¿Cómo funciona?
CSP opera enviando una **cabecera HTTP** en la respuesta del servidor, que indica a los navegadores desde qué orígenes pueden cargar contenido. Esto permite restringir la ejecución de scripts, imágenes o contenido multimedia desde fuentes no autorizadas.

---

## 🛠️ Práctica 1: Configuración en Apache y Docker
### 🎯 Objetivos:
1️⃣ **Deshabilitar el módulo autoindex**

2️⃣ **Configurar la cabecera HSTS** (requiere habilitar el módulo `headers` y un certificado SSL/TLS)

3️⃣ **Configurar la cabecera CSP** con un ejemplo válido

4️⃣ **Crear un Dockerfile con toda la configuración**

### 🚀 Pasos a seguir
#### 🛠️ 1. Deshabilitar el módulo autoindex
Ejecutar el siguiente comando:
```bash
a2dismod autoindex
systemctl restart apache2
```
![a2dismod](https://github.com/PPS10711021/RA3/blob/main/RA3/RA3_1/assets/1_CSP/a2dismod_autoindex.png)

#### 🔐 2. Configurar la cabecera HSTS
Agregar en la configuración de Apache:
```apache
Header always set Strict-Transport-Security "max-age=31536000; includeSubDomains; preload"
```
**Nota:** Se necesita habilitar HTTPS con un certificado SSL válido.

#### 🔍 2.1 Instalación de un Certificado Digital en Apache

### 📌 Introducción
En esta guía, aprenderemos cómo instalar un **certificado SSL auto-firmado** en Apache en un servidor Linux, lo que permitirá cifrar el tráfico del servidor.

### 🚀 Pasos a seguir

#### 🔹 1. Activar el módulo SSL
Ejecutar:
```bash
sudo a2enmod ssl
sudo service apache2 restart
```

#### 🔹 2. Crear un Certificado SSL Auto-firmado
```bash
sudo mkdir /etc/apache2/ssl
sudo openssl req -x509 -nodes -days 365 \ 
    -newkey rsa:2048 -keyout /etc/apache2/ssl/apache.key \ 
    -out /etc/apache2/ssl/apache.crt
```

#### 🔹 3. Configurar Apache para usar SSL
Editar el archivo:
```bash
sudo nano /etc/apache2/sites-available/default-ssl.conf
```
Cambiar las siguientes líneas:
```apache
SSLCertificateFile /etc/apache2/ssl/apache.crt
SSLCertificateKeyFile /etc/apache2/ssl/apache.key
```
Guardar y cerrar el archivo, luego habilitar la configuración SSL:
```bash
sudo a2ensite default-ssl.conf
sudo service apache2 restart
```

#### 🔹 4. Configurar `/etc/hosts`
Añadir la línea:
```bash
127.0.0.1 www.midominioseguro.com
```

#### 🔹 5. Probar la Configuración
Abrir en un navegador:
```
https://www.midominioseguro.com
```
Es normal recibir un aviso de seguridad, ya que el certificado no está firmado por una autoridad de confianza.

---

#### 🛡️ 3. Configurar la cabecera CSP
Editar el archivo de configuración de Apache (`/etc/apache2/sites-available/000-default.conf` o `default-ssl.conf` si está usando HTTPS) y añadir:
```apache
Header set Content-Security-Policy \
    default-src 'self'; \
    img-src *; \
    media-src media1.com media2.com; \
    script-src userscripts.example.com
```
Reiniciar Apache para aplicar los cambios:
```bash
service apache2 reload
```

---

## 📦 Dockerfile

```dockerfile
FROM ubuntu:latest

#Actualizar paquetes e instalar Apache y herramientas necesarias
RUN apt-get update && apt-get install -y \
    apache2 apache2-utils openssl \
    nano iproute2 tree bash procps net-tools curl wget

#Copiar la configuración personalizada de Apache
COPY 000-default.conf /etc/apache2/sites-available/000-default.conf

#Crear directorio necesario para Apache
RUN mkdir -p /var/run/apache2

#Exponer los puertos HTTP y HTTPS
EXPOSE 80 443

#Mantener Apache en ejecución
CMD ["apachectl", "-D", "FOREGROUND"]
```
![Dockerfile](https://github.com/PPS10711021/RA3/blob/main/RA3/RA3_1/assets/1_CSP/Dockerfile.png)

### 📌 Notas:
- **`a2enmod headers`** habilita el módulo `headers`, requerido para CSP y HSTS.
- **`a2dismod autoindex`** deshabilita el listado de directorios.
- **`EXPOSE 80 443`** permite tráfico HTTP y HTTPS en el contenedor.

---

## 🔍 Validación y pruebas
Para verificar que la **CSP** y **HSTS** están configuradas correctamente:

1️⃣ **Reiniciar Apache y verificar los encabezados HTTP:**
```bash
curl -I https://localhost
```
![curl](https://github.com/PPS10711021/RA3/blob/main/RA3/RA3_1/assets/1_CSP/curl.png)

2️⃣ **Comprobar CSP en el navegador:**
   - Abrir las herramientas de desarrollador (`F12` en Chrome/Firefox)
   - Ir a la pestaña `Red` → seleccionar la solicitud → `Encabezados` (`Headers`)
   - Verificar `Content-Security-Policy` y `Strict-Transport-Security`
---

## 🎯 Conclusión
Configurar **CSP** y **HSTS** en Apache mejora la seguridad contra ataques XSS, inyección de código y robo de datos. Además, con la implementación en **Docker**, se facilita la portabilidad y despliegue seguro de servidores web.
