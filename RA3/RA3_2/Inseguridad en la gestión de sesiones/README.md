# 🛡️ Inseguridad en la gestión de sesiones

## LOW
## 📋 Explicación
Para generar el ID de la cookie, incrementa en 1 el número de la cookie, inicialmente comienza en 0 y incrementa ++1 el id, es decir, es un id autoincrementado.

## 📸 Captura de pantalla
![a2dismod](https://github.com/PPS10711021/RA3/blob/main/RA3/RA3_2/images/ids1.png)
![a2dismod](https://github.com/PPS10711021/RA3/blob/main/RA3/RA3_2/images/ids2.png)
---

## MEDIUM
## 📋 Explicación
Para generar el ID de la cookie, utiliza la función time(), esto se sabe porque al pasar el id de la cookie en segundos a años, nos devuelve 55,34 años, esto tiene sentido ya que la función time() devuelve los segundos transcurridos desde el 1 de enero del 1970 a las 00:00:00.

## 📸 Captura de pantalla
![a2dismod](https://github.com/PPS10711021/RA3/blob/main/RA3/RA3_2/images/ids3.png)
