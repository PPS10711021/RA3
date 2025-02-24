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

🔹 **Ejemplo de cabecera CSP básica:**
```apache
Content-Security-Policy: default-src 'self'
```
Esta configuración permite que el contenido solo provenga del mismo origen que el sitio, excluyendo subdominios.

🔹 **Ejemplo de cabecera CSP avanzada:**
```apache
Content-Security-Policy: default-src 'self'; img-src *; media-src media1.com media2.com; script-src userscripts.example.com
```
### 📖 Explicación:
- **`default-src 'self'`** → Todo el contenido debe provenir del mismo origen.
- **`img-src *`** → Permite cargar imágenes desde cualquier origen.
- **`media-src media1.com media2.com`** → Solo permite archivos de audio/video desde `media1.com` y `media2.com`.
- **`script-src userscripts.example.com`** → Solo permite ejecutar scripts de `userscripts.example.com`.

---

## ⚙️ Configuración en Apache
Para definir **CSP** en Apache, se debe configurar la cabecera HTTP mediante el módulo `headers`:

```apache
Header set Content-Security-Policy \
    default-src 'self'; \
    img-src *; \
    media-src media1.com media2.com; \
    script-src userscripts.example.com
```

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

#### 🔐 2. Configurar la cabecera HSTS
Agregar en la configuración de Apache:
```apache
Header always set Strict-Transport-Security "max-age=31536000; includeSubDomains; preload"
```
**Nota:** Se necesita habilitar HTTPS con un certificado SSL válido.

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
systemctl restart apache2
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
![Captura de pantalla a 2025-02-24 19-52-47](https://github.com/user-attachments/assets/53d42e77-8e67-4951-8b9f-e7e2ab55e4f8)


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
2️⃣ **Comprobar CSP en el navegador:**
   - Abrir las herramientas de desarrollador (`F12` en Chrome/Firefox)
   - Ir a la pestaña `Red` → seleccionar la solicitud → `Encabezados` (`Headers`)
   - Verificar `Content-Security-Policy` y `Strict-Transport-Security`

3️⃣ **Probar CSP con un ataque XSS simulado** usando:
```html
<script>alert('XSS')</script>
```
Si el navegador bloquea el script, la CSP está funcionando correctamente. 🚀

---

## 🎯 Conclusión
Configurar **CSP** y **HSTS** en Apache mejora la seguridad contra ataques XSS, inyección de código y robo de datos. Además, con la implementación en **Docker**, se facilita la portabilidad y despliegue seguro de servidores web.

🔹 **Próximos pasos:**
✅ Integrar ModSecurity para mayor protección.
✅ Implementar políticas CSP más estrictas según la aplicación.
✅ Auditar la configuración de seguridad con herramientas como **Mozilla Observatory**.

🚀 ¡Asegura tu servidor Apache y refuerza la seguridad de tu aplicación web! 🔐

