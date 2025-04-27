# 🚀 Vulnerabilidad y Hardening Web - DVWA Security Practices

---

## 📌 Introducción

### 🔒 1.1. Vulnerabilidades en Aplicaciones Web
La **seguridad de aplicaciones web** es un pilar esencial de la ciberseguridad actual. Una mala configuración o un desarrollo inseguro puede dar lugar a vulnerabilidades explotables, tales como:

✅ Inyección de código (**SQL Injection**)  
✅ Robo de información sensible (**XSS, CSRF**)  
✅ Acceso no autorizado a sesiones  
✅ Ejecución remota de comandos  

### 🛡️ 1.2. Damn Vulnerable Web Application (DVWA)
**DVWA** es una aplicación web creada intencionadamente con múltiples vulnerabilidades, diseñada para que estudiantes, investigadores y profesionales practiquen técnicas de **hacking ético** y pruebas de penetración. Permite:

- 🔹 Identificar y explotar vulnerabilidades web en un entorno seguro
- 🔹 Mejorar habilidades en **pentesting** y análisis de seguridad
- 🔹 Aprender métodos de mitigación y corrección de vulnerabilidades
- 🔹 Analizar distintos niveles de seguridad: **Low**, **Medium** y **High**
- 🔹 Familiarizarse con técnicas de explotación realistas y su correspondiente hardening

---

## 🎯 Objetivos
Esta práctica permite alcanzar los siguientes criterios de evaluación:

📌 **RA3**: Detecta y corrige vulnerabilidades de aplicaciones web analizando su código fuente y configurando servidores web.

- ✔ **CA.A**: Análisis de riesgos y evaluación de vulnerabilidades
- ✔ **CA.B**: Explotación controlada de vulnerabilidades web
- ✔ **CA.C**: Aplicación de técnicas de remediación
- ✔ **CA.D**: Configuración segura de servidores y aplicaciones
- ✔ **CA.E**: Implementación de prácticas de hardening
- ✔ **CA.F**: Documentación de hallazgos y propuestas de mejora

---

## 🛠️ Actividades

### ✅ 3.1. Instalación de DVWA
- 📦 Montar el entorno DVWA en una máquina virtual usando **XAMPP**, **WAMP** o **Docker**.
- 🔧 Configurar correctamente la base de datos y los permisos de DVWA.
- 🔒 Ajustar los niveles de seguridad de la aplicación (Low, Medium y High).

### 🔥 3.2. Explotación de vulnerabilidades
📖 Referencias:
- [Repositorio Oficial de DVWA](https://github.com/digininja/DVWA)
- [Writeups DVWA de Aftab Sama](https://aftabsama.com/writeups/dvwa/)

#### 📌 Prácticas a realizar:
1️⃣ **SQL Injection (SQLi)**  
2️⃣ **Cross-Site Scripting (XSS)**  
3️⃣ **Cross-Site Request Forgery (CSRF)**  
4️⃣ **Inseguridad en sesiones y autenticaciones**  
5️⃣ **Ejecución remota de comandos**

Cada explotación debe incluir:

- 📸 **Capturas de pantalla** del proceso de explotación
- 🖋️ **Explicaciones detalladas** de los comandos y técnicas usadas
- 🔒 **Propuestas de solución** para mitigar cada vulnerabilidad detectada

---

## 📦 Requisitos de entrega

- 📂 Entrega de la práctica mediante **Git**, documentando el proceso.
- ✍️ Informe detallado explicando:
  - Técnicas empleadas en cada vulnerabilidad
  - Capturas de pantalla
  - Soluciones y medidas de hardening propuestas
