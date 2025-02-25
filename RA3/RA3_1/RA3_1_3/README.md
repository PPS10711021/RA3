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
mv owasp-modsecurity-crs/crs-setup.conf.example /etc/modsecurity/crs-setup.conf
mv owasp-modsecurity-crs/rules/ /etc/modsecurity/
```

### 🔹 4. Configurar Apache para cargar las reglas
Editar el archivo de configuración de ModSecurity:
```bash
nano /etc/apache2/mods-enabled/security2.conf
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
📸 **Captura de la configuración:**

![security2](https://github.com/PPS10711021/RA3/blob/main/RA3/RA3_1/assets/3_OWASP/security2.png)

### 🔹 5. Configurar una regla personalizada
Editar el archivo del host virtual:
```bash
nano /etc/apache2/sites-available/default-ssl.conf
```
Añadir la siguiente línea:
```apache
SecRuleEngine On
SecRule ARGS:testparam "@contains test" "id:1234,deny,status:403,msg:'Cazado por Ciberseguridad'"
```
📸 **Captura de la configuración:**

![defaultssl](https://github.com/PPS10711021/RA3/blob/main/RA3/RA3_1/assets/3_OWASP/defaultssl.png)

Guardar los cambios y reiniciar Apache:
```bash
service apache2 reload
```

---

## 🔍 Verificación y Pruebas

Para comprobar que las reglas están funcionando, podemos realizar distintas pruebas:

### 🛠️ **1. Intentar ejecutar un comando en la URL** (Simulación de ataque de RCE)
```bash
localhost:8080/index.html?exec=/bin/bash
```
📸 **Bloqueo del intento de ejecución de comandos:**

![intento_comando](https://github.com/PPS10711021/RA3/blob/main/RA3/RA3_1/assets/3_OWASP/intento_comando.png)

### 🛠️ **2. Intento de Path Traversal**
```bash
localhost:8080/index.html?exec=/../../
```
📸 **Bloqueo del intento de ejecución de comandos:**

![intento_escalar_dir](https://github.com/PPS10711021/RA3/blob/main/RA3/RA3_1/assets/3_OWASP/intento_escalar_dir.png)

📸 **Protección contra Path Traversal:**

### 🛠️ **3. Revisar logs de ModSecurity**
Para verificar los bloqueos en los registros de Apache:
```bash
sudo tail /var/log/apache2/error.log
```
📸 **Captura de logs de eventos bloqueados:**

![logs](https://github.com/PPS10711021/RA3/blob/main/RA3/RA3_1/assets/3_OWASP/logs.png)

---

## 🎯 Conclusión

Configurar **ModSecurity** con las **reglas OWASP CRS** en **Apache** permite una protección avanzada contra amenazas web comunes. Al integrarlo con **Docker**, se facilita su despliegue y mantenimiento en entornos de producción.

---

[RA3_1_1](https://github.com/PPS10711021/RA3/edit/main/RA3/RA3_1/RA3_1_1) | 
[RA3_1_2](https://github.com/PPS10711021/RA3/edit/main/RA3/RA3_1/RA3_1_2) | 
[RA3_1_3](https://github.com/PPS10711021/RA3/edit/main/RA3/RA3_1/RA3_1_3) | 
[RA3_1_4](https://github.com/PPS10711021/RA3/edit/main/RA3/RA3_1/RA3_1_4)

---
💾 **Imagen Docker OWASP:**

[Imagen OWASP](https://hub.docker.com/layers/pps10711021/pps_docker/owasp/images/sha256-9e2068c855c5265813e2e1243454707a58c832b1b65dcc8e1ceb2a31ccddb504)
