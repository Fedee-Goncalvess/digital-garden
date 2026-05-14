---
{"dg-publish":true,"permalink":"/3-resources/zettelkasten/resume/repaso-instrumentacion-y-control-modulo-1/","created":"2026-05-04T18:09:30.476-03:00","updated":"2026-05-10T23:56:58.522-03:00"}
---

# Dudas
Resolución Resolución No entiendo por qué Hay un ejercicio de un parcial de dice se tiene un sistema de medida conocen proximidad con el alcance de 90 cm y prisión 1 mm y después habla de la amplificación analógica que hay de una etapa que dice más menos 12 entrada admisible y resolución de más menos 4 microbots Lo que no entiendo es por qué o sea en el caso de la precisión de 1 mm Entiendo que una medición puede ser o cero por ejemplo 1 mm la siguiente y otros la siguiente o cero o dos pero en la resolución de la otra de más menos 4 microboltes es Cero la siguiente seria cuatro microbolts y la otra puede ser 4 microvolts por lo tanto hay una diferencia de 8 microbolt y esa es resolución ¿Por qué resolución? No es lo más chiquito no entiendo por qué se agarra lo más grande

No entendemos NADA
![image-40.png](/img/user/3-Resources/Archivos/image-40.png)
![image-39.png](/img/user/3-Resources/Archivos/image-39.png)
Decir +/- 4uV pp. está mal????? Decir +/- 4uV = 8uV pp es decir no tiene sentido. Pero entonces por que hacen el calculo con 8uV?? Ademas que sentido tiene decir que una resolución es un rango? si la resolución es un valor fijo que determina el minimo paso entre un valor y otro, como puede ser variable entre un rango? debería ser algo fijo. 
![image-44.png](/img/user/3-Resources/Archivos/image-44.png)


En este caso, nos piden segun la datasheet la maxima tensión que podría tener y tataata. Ahora que datos podemos obviar? ya que hay datos como resistencia o capacitor que se utilizaron pero tal vez no nos interesa
![image-41.png](/img/user/3-Resources/Archivos/image-41.png)
![image-42.png](/img/user/3-Resources/Archivos/image-42.png)

Si tuvieramos que calcualr I+ e I- para corrientes de polarización como lo hacemos si tenemos una datasheet de este estilo?
![image-43.png](/img/user/3-Resources/Archivos/image-43.png)

QUE OINDA COMO ES ESTO
Necesitamos saber todas las configuraciones, ventajas y desventajas
![image-46.png](/img/user/3-Resources/Archivos/image-46.png)
![image-47.png](/img/user/3-Resources/Archivos/image-47.png)
Que onda esto?
![image-48.png](/img/user/3-Resources/Archivos/image-48.png)

Resolución de ADC siempre debe ser mayor al del sensor (es decir, el "paso" mínimo distinguible del adc debe ser más chico que el del sensor)?

3)d) Es eso de abajo? 
El enano dice que el I_bias es corriente de offset, y en enunciado dicen que es corriente de polarización. O al menos lo que si se asegura el enano es que es la corriente de polarización en **modo comun** nose que quiere decir. 

Cuando dicen I_bias decimos que es el modo común de las corrientes de polarización. 
![image-50.png](/img/user/3-Resources/Archivos/image-50.png)
![image-49.png](/img/user/3-Resources/Archivos/image-49.png)

QUE ONDA ESTO????????
![image-51.png](/img/user/3-Resources/Archivos/image-51.png)

Factor de escala: 
Niveles/Rango medida sensor

Resolución ADC:
Rango entrada ADC/Niveles

![image-52.png](/img/user/3-Resources/Archivos/image-52.png)
La solución $V_0$ de este es aunque en el caso de abajo no existe $V_s$ es decir vale 0
![IMG_20260506_005613406.jpg](/img/user/3-Resources/Archivos/IMG_20260506_005613406.jpg)

Por qué en este caso hacen R3=R0? no podría ser R2=Rt? es lo mismo?
Y por qué R=rR0?  Para que es la razón? Simplemente una forma de medir sensibilidad o algo así?
![image-53.png](/img/user/3-Resources/Archivos/image-53.png)
Y tiene sentido decir que para aumentar linealidad o sensibilidad hay que aumentar r? Es decir aumentar las resistencias R o tener un R0 menor?
![image-54.png](/img/user/3-Resources/Archivos/image-54.png)
Todo esto de arriba era para este ejercicio de parcial
![image-55.png](/img/user/3-Resources/Archivos/image-55.png)
Utilizar un Pt1000? Se utiliza un Pt1000 cuando los cables para el sensor son muy largos (por ejemplo si el sensor se debe colocar lejos), esto produce
![image-65.png](/img/user/3-Resources/Archivos/image-65.png)
JUSTIFICACION DE USAR PT1000 PARA CABLES LARGOS
Para el siguiente ejercicio
![image-56.png](/img/user/3-Resources/Archivos/image-56.png)
planteo Rango Dinamico del sensor de proximidad con 20log(20cm/1mm)?
![image-57.png](/img/user/3-Resources/Archivos/image-57.png)

Luego la etapa de amplificación analógica tiene
RD = 20 log (12V/4uV)

y por últmo ADC con Vref 5v y 8bits
Para el ADC se necesita saber cual es el rango de entrada (Ejemplo de 0°C a 100°C) y saber cuanta resolución se necesita (1°C) por lo que tenemos la cantidad de valores posibles. **Se debe agregar el 0!** $\frac{RE}{Resolución}+1\leq 2{^N}$
Luego para saber el voltaje necesario para cada bit es decir la diferencia entre un bit y otro es $LSB=\mathrm{Re}solución_{ADC}=\frac{Vref}{2{^N}}$

---
Ejercicio con Sistemas: Sensor->AmpOp-> ADC

1. Conseguir Rango Dinámico de cada etapa (logaritmo o sin logaritmo)
	1. $\frac{Máx-Min}{\mathrm{Re}solución}$
2. Evaluar cual es el cuello de botella comparando las etapas
3. Proponer mejorar cada etapa
	1. Etapa de sensor: 
	2. Etapa de AmpOp: 
	3. Etapa de ADC: Aumentar cantidad de bits


3 hilos 4 hilos etc:
![image-58.png](/img/user/3-Resources/Archivos/image-58.png)

<iframe src="/img/user/3-Resources/Archivos/PDFs/Facultad/Eye-AmpOps.pdf" width="100%" height="900px" title="Eye-AmpOps.pdf" style="border:1px solid #ccc;"></iframe>

**Regulación y Seguimiento**
![image-59.png](/img/user/3-Resources/Archivos/image-59.png)

![image-60.png](/img/user/3-Resources/Archivos/image-60.png)
![image-61.png](/img/user/3-Resources/Archivos/image-61.png)![image-62.png](/img/user/3-Resources/Archivos/image-62.png)
![image-63.png](/img/user/3-Resources/Archivos/image-63.png)

![image-64.png](/img/user/3-Resources/Archivos/image-64.png)


![image-66.png](/img/user/3-Resources/Archivos/image-66.png)