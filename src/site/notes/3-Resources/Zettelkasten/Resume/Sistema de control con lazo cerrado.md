---
{"dg-publish":true,"permalink":"/3-resources/zettelkasten/resume/sistema-de-control-con-lazo-cerrado/","created":"2026-05-19T20:09:47.947-03:00","updated":"2026-05-19T21:34:17.877-03:00"}
---

# Introducción
## Diagrama de bloques

![image-67.png\|637](/img/user/3-Resources/Archivos/image-67.png)

## Acciones de control simples
### ON-OFF
El controlador obtiene el error y decide entre No actuar o Actuar con un valor U como setpoint. #duda_instru

![image-68.png](/img/user/3-Resources/Archivos/image-68.png)


![image-69.png](/img/user/3-Resources/Archivos/image-69.png)
### ON-OFF con histéresis
Entiendo que el controlador recive el error, y actua cuando el error es mayor a un $e \geq epsilon$ y luego cuando es $e \leq epsilon$ haciendo una forma de histéresis
#duda_instru No entiendo de donde sale ese e mayor o menor a cero.
Pero entiendo que la idea es, dado un error mayor al epsilon, activar el "controlador" y apagarlo cuando sea menor a -epsilon.
![image-70.png](/img/user/3-Resources/Archivos/image-70.png)

![image-71.png](/img/user/3-Resources/Archivos/image-71.png)

### Proporcional
Se elige una ganancia "pendiente" para control.
![image-72.png](/img/user/3-Resources/Archivos/image-72.png)

![image-73.png](/img/user/3-Resources/Archivos/image-73.png)

### Integral0
![image-74.png](/img/user/3-Resources/Archivos/image-74.png)
![image-75.png](/img/user/3-Resources/Archivos/image-75.png)
Puede seguir habiendo acción integral, incluso después de haber error.
### Derivativo
![image-76.png](/img/user/3-Resources/Archivos/image-76.png)