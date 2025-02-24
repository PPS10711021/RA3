# 🚀 Server Hardening - Apache Security Practices

---

## 📌 Introducción

### 🔒 1.1. Server Hardening
El **hardening** de servidores web es el proceso de mejorar la seguridad de un servidor web reduciendo vulnerabilidades y eliminando puntos de entrada explotables por atacantes. Su objetivo es proteger contra diversas amenazas, como:

✅ Ataques de denegación de servicio (**DDoS**)

✅ Inyecciones de código

✅ Explotación de vulnerabilidades conocidas

✅ Acceso no autorizado

### 🛡️ 1.2. Apache Hardening
El **hardening de Apache** consiste en reforzar la seguridad del servidor web Apache para reducir la superficie de ataque y prevenir posibles vulnerabilidades. Algunas buenas prácticas incluyen:

🔹 Mantener Apache actualizado

🔹 Desactivar módulos innecesarios

🔹 Deshabilitar la visualización de información del servidor

🔹 Configurar permisos estrictos

🔹 Usar **HTTPS (SSL/TLS)**

🔹 Limitar métodos HTTP permitidos

🔹 Protección contra inyección de código

🔹 Implementar autenticación básica

🔹 Configurar **firewall** y restricciones de acceso IP

🔹 Ajustar **Timeout** y **KeepAlive**

---

## 🎯 Objetivos
Esta unidad didáctica permite cumplir con los siguientes criterios de evaluación:

📌 **RA4**: Detecta y corrige vulnerabilidades en aplicaciones web.

✔ **CA.A**: Validación de entradas de usuario.

✔ **CA.B**: Detección de riesgos de inyección (servidor/cliente).

✔ **CA.E**: Gestión segura de sesiones de usuario.

---

## 🛠️ Actividades

### ✅ 3.1. Requisitos
- 🔗 Crear una cuenta de **GitHub** para entregas con el usuario (https://github.com/PPS10711021/RA3).

- 📦 Crear una cuenta en **Docker HUB** para subir imágenes con el mismo usuario (https://hub.docker.com/r/pps10711021/pps_docker/tags).
  
- 🎨 Utilizar **GIT + template**: [Repositorio Template](https://github.com/pkaminasfp/template).

### 🔥 3.2. Apache Hardening
📖 Referencia: [Hardening Servidor](https://psegarrac.github.io/Ciberseguridad-PePS/tema3/seguridad/web/2021/03/01/Hardening-Servidor.html)

#### 📌 Prácticas
1️⃣ **[Content Security Policy (CSP)](https://github.com/PPS10711021/RA3/edit/main/RA3/RA3_1/RA3_1_1/README.md)**

2️⃣ **Web Application Firewall** (https://github.com/PPS10711021/RA3/edit/main/RA3/RA3_1/RA3_1_2/README.md)

3️⃣ **OWASP** (https://github.com/PPS10711021/RA3/edit/main/RA3/RA3_1/RA3_1_3/README.md)

4️⃣ **Evitar ataques DDoS** (https://github.com/PPS10711021/RA3/edit/main/RA3/RA3_1/RA3_1_4/README.md)

5️⃣ **EXTRA: Implementación con Nginx** (https://github.com/PPS10711021/RA3/edit/main/RA3/RA3_1/RA3_1_5/README.md)

### 🔐 3.3. Certificados SSL
📖 Referencia: [Instalación de Certificados SSL](https://psegarrac.github.io/Ciberseguridad-PePS/tema1/practicas/2020/11/08/P1-SSL.html)

✅ Instalar un certificado digital en Apache y generar la imagen Docker.

### 🏆 3.4. Apache Hardening Best Practices
📖 Referencia: [Apache Web Server Hardening](https://geekflare.com/cybersecurity/apache-web-server-hardening-security/)

✅ Implementar mejores prácticas de seguridad en Apache y generar la imagen Docker.

