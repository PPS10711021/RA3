# 🛡️ Ejecución de comandos remotos

## HIGH
## 📋 Explicación
Introducimos |ls en un campo donde debería ir una IP, como el servidor no valida bien el input, se ejecuta el comando ls, permitiendo al atacante listar archivos en el servidor.

## 🖥️ Payload ejecutado
```bash
|ls
|ip a
```
## 📸 Captura de pantalla
![a2dismod](https://github.com/PPS10711021/RA3/blob/main/RA3/RA3_2/images/remote1.png)
![a2dismod](https://github.com/PPS10711021/RA3/blob/main/RA3/RA3_2/images/remote2.png)
