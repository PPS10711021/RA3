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
service apache2 reload
```
![a2dismod](https://github.com/PPS10711021/RA3/blob/main/RA3/RA3_1/assets/1_CSP/a2dismod_autoindex.png)

#### 🔐 2. Configurar la cabecera HSTS
Agregar en la configuración de Apache:
```apache
Header always set Content-Security-Policy "default-src 'self'; script-src 'self'"
```
![apache2conf](https://github.com/PPS10711021/RA3/blob/main/RA3/RA3_1/assets/1_CSP/apache2conf.png)

**Nota:** Se necesita habilitar HTTPS con un certificado SSL válido.

#### 🔍 2.1 Instalación de un Certificado Digital en Apache

### 📌 Introducción
En esta guía, aprenderemos cómo instalar un **certificado SSL auto-firmado** en Apache en un servidor Linux, lo que permitirá cifrar el tráfico del servidor.

### 🚀 Pasos a seguir

#### 🔹 1. Activar el módulo SSL
Ejecutar:
```bash
a2enmod ssl
service apache2 reload
```

#### 🔹 2. Crear un Certificado SSL Auto-firmado

![cert](https://github.com/PPS10711021/RA3/blob/main/RA3/RA3_1/assets/1_CSP/creacion_cert.png)

#### 🔹 3. Configurar Apache para usar SSL
Editar el archivo:
```bash
nano /etc/apache2/sites-available/default-ssl.conf
```
Cambiar las siguientes líneas:
```apache
SSLCertificateFile /etc/apache2/ssl/apache.crt
SSLCertificateKeyFile /etc/apache2/ssl/apache.key
```
![virtualhost443](https://github.com/PPS10711021/RA3/blob/main/RA3/RA3_1/assets/1_CSP/config_virtualhost443.png)

Guardar y cerrar el archivo, luego habilitar la configuración SSL:
```bash
a2ensite default-ssl.conf
service apache2 restart
```

#### 🔹 4. Configurar `/etc/hosts` en el anfitrión
Añadir la línea:
```bash
172.16.0.2 www.midominioseguro.com
```
![etc_hosts](https://github.com/PPS10711021/RA3/blob/main/RA3/RA3_1/assets/1_CSP/etc_hosts.png)

#### 🔹 5. Probar la Configuración
Abrir en un navegador:
```
https://www.midominioseguro.com
```
Es normal recibir un aviso de seguridad, ya que el certificado no está firmado por una autoridad de confianza.

![apache_https](https://github.com/PPS10711021/RA3/blob/main/RA3/RA3_1/assets/1_CSP/Apache_https.png)

---

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

---

[RA3_1_1](https://github.com/PPS10711021/RA3/edit/main/RA3/RA3_1/RA3_1_1) | 
[RA3_1_2](https://github.com/PPS10711021/RA3/edit/main/RA3/RA3_1/RA3_1_2) | 
[RA3_1_3](https://github.com/PPS10711021/RA3/edit/main/RA3/RA3_1/RA3_1_3) | 
[RA3_1_4](https://github.com/PPS10711021/RA3/edit/main/RA3/RA3_1/RA3_1_4)

---

[Imagen CSP](https://hub.docker.com/layers/pps10711021/pps_docker/csp/images/sha256-8b3eb9ed765e95c7178e1b6a801a8bdcab6d986a2ae30ad9365485e6374d7171)
