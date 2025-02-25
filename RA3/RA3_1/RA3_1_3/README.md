# 🛡️ Instalación de Reglas OWASP en ModSecurity (WAF) en Apache

## 📌 Introducción

### 🔥 ¿Qué son las reglas OWASP para ModSecurity?
La **OWASP Core Rule Set (CRS)** es un conjunto de reglas predefinidas para **ModSecurity**, diseñadas para proteger aplicaciones web contra ataques como:

✅ **Inyección SQL**
✅ **Cross-Site Scripting (XSS)**
✅ **Path Traversal**
✅ **Remote Command Execution (RCE)**

Al utilizar estas reglas, podemos reforzar la seguridad de Apache sin necesidad de configurar manualmente cada regla.

---

## 🛠️ Instalación y Configuración de OWASP ModSecurity CRS

### 🔹 1. Instalar ModSecurity
Para instalar ModSecurity en **Apache**, ejecutar:
```bash
apt install libapache2-mod-security2
```
Instalado en el  [RA3_1_2](https://github.com/PPS10711021/RA3/edit/main/RA3/RA3_1/RA3_1_2)
### 🔹 2. Clonar el repositorio de OWASP ModSecurity CRS
```bash
git clone https://github.com/SpiderLabs/owasp-modsecurity-crs.git
```

### 🔹 3. Mover los archivos de configuración
```bash
sudo mv owasp-modsecurity-crs/crs-setup.conf.example /etc/modsecurity/crs-setup.conf
sudo mv owasp-modsecurity-crs/rules/ /etc/modsecurity/
```
Si hay errores al mover las reglas, ejecutar:
```bash
sudo mkdir /etc/modsecurity/rules
cd owasp-modsecurity-crs/rules
sudo cp *.* /etc/modsecurity/rules
```

### 🔹 4. Configurar Apache para cargar las reglas
Editar el archivo de configuración de ModSecurity:
```bash
sudo nano /etc/apache2/mods-enabled/security2.conf
```
Añadir la siguiente configuración:
```apache
<IfModule security2_module>
    # Directorio para datos persistentes de modsecurity
    SecDataDir /var/cache/modsecurity
    SecRuleEngine On
    # Cargar configuración local
    IncludeOptional /etc/modsecurity/*.conf
    # Incluir las reglas OWASP
    Include /etc/modsecurity/rules/*.conf
</IfModule>
```

### 🔹 5. Configurar una regla personalizada
Editar el archivo del host virtual:
```bash
sudo nano /etc/apache2/sites-available/default-ssl.conf
```
Añadir la siguiente línea:
```apache
SecRuleEngine On
SecRule ARGS:testparam "@contains test" "id:1234,deny,status:403,msg:'Cazado por Ciberseguridad'"
```
Guardar los cambios y reiniciar Apache:
```bash
sudo systemctl restart apache2
```

---

## 🔍 Verificación y Pruebas

Para comprobar que las reglas están funcionando, podemos realizar distintas pruebas:

### 🛠️ **1. Intentar acceder con un parámetro bloqueado**
```bash
curl localhost:8080/index.html?testparam=test
```
📸 **Captura de respuesta esperada (403 Forbidden):**

🖼️ [Ver imagen](/mnt/data/Captura%20de%20pantalla%20a%202025-02-24%2021-49-00.png)

### 🛠️ **2. Intentar ejecutar un comando en la URL** (Simulación de ataque de RCE)
```bash
localhost:8080/index.html?exec=/bin/bash
```
📸 **Bloqueo del intento de ejecución de comandos:**

🖼️ [Ver imagen](/mnt/data/Captura%20de%20pantalla%20a%202025-02-24%2021-49-10.png)

### 🛠️ **3. Intento de Path Traversal**
```bash
localhost:8080/index.html?exec=/../../
```
📸 **Protección contra Path Traversal:**

🖼️ [Ver imagen](/mnt/data/Captura%20de%20pantalla%20a%202025-02-24%2021-51-57.png)

### 🛠️ **4. Revisar logs de ModSecurity**
Para verificar los bloqueos en los registros de Apache:
```bash
sudo tail /var/log/apache2/error.log
```
📸 **Captura de logs de eventos bloqueados:**

🖼️ [Ver imagen](/mnt/data/Captura%20de%20pantalla%20a%202025-02-24%2021-52-32.png)

📸 **Detalle de registros OWASP CRS:**

🖼️ [Ver imagen](/mnt/data/Captura%20de%20pantalla%20a%202025-02-24%2021-52-57.png)

---

## 📦 Creación de Imagen Docker con Apache + ModSecurity + OWASP CRS

### 📌 **Dockerfile:**
```dockerfile
# Imagen base de Apache
FROM httpd:latest

# Instalar dependencias y ModSecurity
RUN apt update && apt install -y libapache2-mod-security2 \
    && git clone https://github.com/SpiderLabs/owasp-modsecurity-crs.git /tmp/crs \
    && mv /tmp/crs/crs-setup.conf.example /etc/modsecurity/crs-setup.conf \
    && mv /tmp/crs/rules/ /etc/modsecurity/ \
    && rm -rf /tmp/crs \
    && echo "Include /etc/modsecurity/rules/*.conf" >> /etc/apache2/mods-enabled/security2.conf

# Exponer los puertos 80 y 443
EXPOSE 80 443

# Iniciar Apache en segundo plano
CMD ["httpd", "-D", "FOREGROUND"]
```

### 🚀 Construcción y ejecución del contenedor
Para construir la imagen:
```bash
docker build -t apache-owasp-modsecurity .
```
Para ejecutar el contenedor:
```bash
docker run -d -p 80:80 -p 443:443 --name waf-owasp apache-owasp-modsecurity
```

---

## 🎯 Conclusión

Configurar **ModSecurity** con las **reglas OWASP CRS** en **Apache** permite una protección avanzada contra amenazas web comunes. Al integrarlo con **Docker**, se facilita su despliegue y mantenimiento en entornos de producción.

---

[RA3_1_1](https://github.com/PPS10711021/RA3/edit/main/RA3/RA3_1/RA3_1_1) | 
[RA3_1_2](https://github.com/PPS10711021/RA3/edit/main/RA3/RA3_1/RA3_1_2) | 
[RA3_1_3](https://github.com/PPS10711021/RA3/edit/main/RA3/RA3_1/RA3_1_3) | 
[RA3_1_4](https://github.com/PPS10711021/RA3/edit/main/RA3/RA3_1/RA3_1_4)

---

[Imagen OWASP](https://hub.docker.com/layers/pps10711021/pps_docker/owasp/images/sha256-9e2068c855c5265813e2e1243454707a58c832b1b65dcc8e1ceb2a31ccddb504)
