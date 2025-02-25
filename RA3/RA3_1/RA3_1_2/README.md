# 🛡️ Web Application Firewall (WAF) en Apache

## 📌 Introducción

### 🔥 ¿Qué es un WAF?
Según **Wikipedia**, un **Web Application Firewall (WAF)** es un tipo de firewall que supervisa, filtra o bloquea el tráfico **HTTP** hacia y desde una aplicación web. Se diferencia de un firewall de red en que puede filtrar contenido de aplicaciones web específicas, protegiéndolas de amenazas como:

✅ **Inyección SQL**
✅ **Cross-Site Scripting (XSS)**
✅ **Falsificación de petición de sitios cruzados (CSRF)**

Desde 2002, el proyecto **ModSecurity** ha permitido democratizar esta tecnología, creando conjuntos de reglas básicas para proteger aplicaciones web, basándose en la lista **OWASP Top 10** de vulnerabilidades más críticas.

---

## 🛠️ Instalación y Configuración de ModSecurity

### 🔹 1. Instalar ModSecurity y sus reglas
Para instalar ModSecurity en **Apache**, ejecutar:
```bash
apt install libapache2-mod-security2
```

Una vez instalado, debemos copiar el archivo de configuración recomendado:
```bash
cp /etc/modsecurity/modsecurity.conf-recommended /etc/modsecurity/modsecurity.conf
```

Habilitar el motor de reglas editando el archivo de configuración:
```bash
nano /etc/modsecurity/modsecurity.conf
```
Buscar la línea:
```apache
SecRuleEngine DetectionOnly
```
Y cambiarla por:
```apache
SecRuleEngine On
```

### 🔹 2. Reiniciar Apache para aplicar cambios
```bash
systemctl restart apache2
```

---

## 🔍 Verificación de ModSecurity

Para comprobar que **ModSecurity** está funcionando correctamente, podemos realizar una prueba sencilla.

1️⃣ Copiar un archivo PHP de prueba llamado **post.php** dentro del **DocumentRoot** de Apache:
```bash
cp post.php /var/www/html/
```
[post.php](https://github.com/victorponz/Ciberseguridad-PePS/blob/master/php/validacion/post.php)
2️⃣ Acceder a la URL del script con una petición potencialmente maliciosa (**simulación de XSS**):
```
https://www.midominioseguro.com/post.php
```

Si la petición es bloqueada, ModSecurity devolverá un **Error 403 (Forbidden)**.

📸 **Captura de WAF en acción:**

🖼️ [Captura de pantalla bloqueando XSS](https://github.com/PPS10711021/RA3/blob/main/RA3/RA3_1/assets/2_WAF/error403.png)

---

## 🔍 Validación y Pruebas

Para verificar el funcionamiento de **ModSecurity**, ejecutar:

1️⃣ **Reiniciar Apache y comprobar logs**:
```bash
systemctl restart apache2
cat /var/log/apache2/modsec_audit.log
```

2️⃣ **Intentar acceder a una URL con una inyección SQL simulada**:
```
https://www.midominioseguro.com/post.php?id=1' OR '1'='1
```
📸 **Resultado esperado: ModSecurity bloqueando el acceso**:

🖼️ [Captura de pantalla de error 403](https://github.com/PPS10711021/RA3/blob/main/RA3/RA3_1/assets/2_WAF/error403.png)

🖼️ [Configuración de ModSecurity en Apache](https://github.com/PPS10711021/RA3/blob/main/RA3/RA3_1/assets/2_WAF/modsecurity.png)

---

## 🎯 Conclusión

Configurar **ModSecurity** como **WAF** en **Apache** es una excelente práctica para proteger aplicaciones web de ataques como **XSS, inyección SQL y CSRF**. Además, integrarlo con **Docker** facilita su despliegue y mantenimiento en entornos de producción.

🔹 **Próximos pasos:**
✅ Ajustar reglas personalizadas en ModSecurity para una mayor seguridad.
✅ Integrar ModSecurity con **OWASP CRS** (Core Rule Set) para una protección más avanzada.
✅ Analizar logs de ModSecurity con herramientas como **ELK Stack** o **Splunk**.

🚀 **¡Protege tus aplicaciones web con un WAF robusto como ModSecurity!** 🔐

