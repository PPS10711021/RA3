# 🛡️ Protección contra ataques DoS con mod_evasive en Apache

## 📌 Introducción

### 🔥 ¿Qué es mod_evasive?
El módulo **mod_evasive** para **Apache** es una herramienta que detecta y previene ataques de **Denegación de Servicio (DoS)**. Este módulo supervisa las conexiones entrantes y bloquea temporalmente aquellas IPs que superen los límites definidos en la configuración.

✅ **Protege contra ataques de DoS/DDoS**

✅ **Monitorea las conexiones activas y bloquea IPs sospechosas**

✅ **Registra eventos de ataque en un log específico**

---

## 🛠️ Instalación y Configuración de mod_evasive

### 🔹 1. Instalar mod_evasive en Apache
Ejecutar el siguiente comando:
```bash
apt install libapache2-mod-evasive
```

### 🔹 2. Configurar mod_evasive
Editar el archivo de configuración:
```bash
nano /etc/apache2/mods-available/evasive.conf
```
Añadir o modificar los siguientes parámetros:
```apache
<IfModule mod_evasive20.c>
    DOSHashTableSize 3097
    DOSPageCount 5
    DOSSiteCount 50
    DOSPageInterval 1
    DOSSiteInterval 1
    DOSBlockingPeriod 10
    DOSEmailNotify admin@www.midominioseguro.com
    DOSLogDir "/var/log/mod_evasive"
    DOSWhitelist 127.0.0.1
</IfModule>
```
![confevasive](https://github.com/PPS10711021/RA3/blob/main/RA3/RA3_1/assets/4_DOS/confevasive.png)

### 🔹 3. Crear el directorio de logs y asignar permisos
```bash
mkdir /var/log/mod_evasive
chown www-data:www-data /var/log/mod_evasive
chmod 755 /var/log/mod_evasive
```

### 🔹 4. Habilitar el módulo y reiniciar Apache
```bash
a2enmod evasive
service apache2 reload
```

Para verificar que el módulo está activo:
```bash
apachectl -M | grep evasive
```
📸 **Captura de validación del módulo:**

![grepevasive](https://github.com/PPS10711021/RA3/blob/main/RA3/RA3_1/assets/4_DOS/grepevasive.png)

---

## 🔍 Verificación de Protección contra DoS

Para comprobar que **mod_evasive** bloquea correctamente las IPs sospechosas, se puede ejecutar un ataque de prueba con **Apache Bench (ab)**.

### 🛠️ **1. Simulación de ataque con Apache Bench**
Ejecutar el siguiente comando:
```bash
ab -n 1000 -c 50 http://localhost:8080/
```
📸 **Captura del test de Apache Bench:**

![prueba](https://github.com/PPS10711021/RA3/blob/main/RA3/RA3_1/assets/4_DOS/prueba.png)

### 🛠️ **2. Comprobar el log de mod_evasive**
```bash
ls -l /var/log/mod_evasive/
cat /var/log/mod_evasive/dos-*
```
📸 **Captura de los registros de IPs bloqueadas:**

![logevasive](https://github.com/PPS10711021/RA3/blob/main/RA3/RA3_1/assets/4_DOS/logevasive.png)

---

## 🎯 Conclusión

Configurar **mod_evasive** en **Apache** proporciona una defensa eficaz contra ataques **DoS** al detectar patrones de tráfico sospechosos y bloquear IPs en tiempo real. Al integrarlo con **Docker**, se facilita su despliegue y mantenimiento en entornos de producción.

---

[RA3_1_1](https://github.com/PPS10711021/RA3/edit/main/RA3/RA3_1/RA3_1_1) | 
[RA3_1_2](https://github.com/PPS10711021/RA3/edit/main/RA3/RA3_1/RA3_1_2) | 
[RA3_1_3](https://github.com/PPS10711021/RA3/edit/main/RA3/RA3_1/RA3_1_3) | 
[RA3_1_4](https://github.com/PPS10711021/RA3/edit/main/RA3/RA3_1/RA3_1_4)

---

[Imagen OWASP](https://hub.docker.com/layers/pps10711021/pps_docker/owasp/images/sha256-9e2068c855c5265813e2e1243454707a58c832b1b65dcc8e1ceb2a31ccddb504)
