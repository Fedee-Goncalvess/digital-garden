---
{"dg-publish":true,"permalink":"/3-resources/zettelkasten/resume/resumen-teoria-bd/","created":"2026-06-05T12:22:22.608-03:00","updated":"2026-06-08T18:53:23.924-03:00"}
---

# Clase 1
[BD-Clase1.pdf](/img/user/3-Resources/Archivos/PDFs/Facultad/BD-Clase1.pdf)
SGBD 
Sistema de software que permite crear mantener y utilizar BD
Procesos:
	Definicion
		Especificar tipos, estructuras y restricciones de los datos
	Construccion
		Configuracion y carga inicial de datos en algun dispositivo de almacenamiento 
	Manipulación
		Recuperar datos, actualizar, etc.

Objetivos de SGBD
	Redundancia
	Acceso todo momento
	Acceso concurrente (mas de una persona a todo momento)
	Seguridad
	Integridad (Resistente a fallos)

Componentes 
	DDL
		Especifíca esquema de BD (Diccionario de datos)
	DML
		Recuperacion de información
		Adicion/Eliminacion/Modificacion
		Lenguaje procedimental y no procedimental
Sistema de BD = BD + SGBD
![image-77.png](/img/user/3-Resources/Archivos/image-77.png)

Independencia de datos 
	Hay distintos software que procesan datos. Se diferencian en
	![image-78.png](/img/user/3-Resources/Archivos/image-78.png)
No entiendo sin independencia de datos como que SO?

| Nivel                             | ¿Qué oculta?                                                 | Ejemplo                                       |
| --------------------------------- | ------------------------------------------------------------ | --------------------------------------------- |
| **Sin independencia**             | Nada                                                         | Leer sector 1543 del disco                    |
| **Independencia física**          | La ubicación física de los datos                             | Leer un registro sin saber en qué sector está |
| **Independencia lógica parcial**  | La ubicación física y permite recorrer registros lógicamente | Leer el siguiente registro de un archivo      |
| **Independencia lógica y física** | La organización lógica y física de los datos                 | `SELECT * FROM Cliente` en un SGBD            |
| **Independencia geográfica**      | También oculta dónde están almacenados los datos en la red   | BD distribuidas                               |

![image-79.png](/img/user/3-Resources/Archivos/image-79.png)

![image-80.png](/img/user/3-Resources/Archivos/image-80.png)
#consulta No entiendo a que va con Sistema de información


![image-81.png](/img/user/3-Resources/Archivos/image-81.png)
#consulta  Esquema conceptual es el resultado de los requerimientos + el modelo conceptual???? o por que diferencia diseño conceptual con diseño

![image-82.png](/img/user/3-Resources/Archivos/image-82.png)
#consulta  "Depende de la clase de modelo" Ejemplo SQLlike o No-SQL like?? serian distintas SGBD pero del mismo tipo

![image-83.png](/img/user/3-Resources/Archivos/image-83.png)
#consulta Esquema/Modelo/Diseño diferencias?

![image-84.png](/img/user/3-Resources/Archivos/image-84.png)
#consulta Diseño físico incluye consultas? porque en ese caso entiendo porque SGBD específico

Mecanismos de abstracción
- Clasificación
	- Nodos son elementos/instancias de la misma clase raiz
- Agregación 
	- Nodos FORMAN la clase raiz
- Generalización
	- Nodos son subclases que pueden generalizarse en la clase raiz

![image-85.png](/img/user/3-Resources/Archivos/image-85.png)
#consulta Agr Binaria: Entre dos clases se hace por agregación una nueva clase raíz. Ejemplo Clase Motor + Clase Rueda = Vehiculo. 
No entendimos nada lo de cardinalidad wtf?

# Clase 2
[BD-Clase2.pdf](/img/user/3-Resources/Archivos/PDFs/Facultad/BD-Clase2.pdf)

![image-86.png](/img/user/3-Resources/Archivos/image-86.png)
![image-87.png](/img/user/3-Resources/Archivos/image-87.png)
#consulta  entiendo que agregación en este caso es  lo de que entre  dos clases/entidades distintas, se hace agregación de esta y se crea la clase(en realidad es una  relación) CURSA

![image-88.png](/img/user/3-Resources/Archivos/image-88.png)
#consulta La agregación de atributos te da una entidad
Id+DNI+nombre = Persona

![image-89.png](/img/user/3-Resources/Archivos/image-89.png)
![image-90.png](/img/user/3-Resources/Archivos/image-90.png)
#consulta Entiendo que Primitivas Ascendente te comiste algo  o agregas algo. 
Luego Primitivas Descendentes, refinas el diseño, y terminas agregando pero para dar más detalle.
![image-91.png](/img/user/3-Resources/Archivos/image-91.png)
#consulta Se generan modelos conceptuales para cada fuente, y luego se analiza y se define un único modelo conceptual que abarque las de todos los interesados


# Clase 3
[BD-Clase3.pdf](/img/user/3-Resources/Archivos/PDFs/Facultad/BD-Clase3.pdf)
![image-92.png](/img/user/3-Resources/Archivos/image-92.png)
#consulta  Criterios de rendimiento info de carga wtf


![image-93.png](/img/user/3-Resources/Archivos/image-93.png)
#consulta  wtf bro que chota concha es IR
*Para  tratar  tablas referenciadas, por ejemplo borrar. Se puede establecer FK en nulo, restringir operación, no hacer nada pero delega responsabilidad. Cascada es si borras una PK que es FK de otra tabla, se borra "en  cascada" las  otras tuplas*


# Clase 4
[BD-Clase4.pdf](/img/user/3-Resources/Archivos/PDFs/Facultad/BD-Clase4.pdf)
{t/}

![image-94.png](/img/user/3-Resources/Archivos/image-94.png)
# Clase 5
[BD-Clase5.pdf](/img/user/3-Resources/Archivos/PDFs/Facultad/BD-Clase5.pdf)
<iframe src="/img/user/3-Resources/Archivos/PDFs/Facultad/BD-Clase5.pdf" width="100%" height="900px" title="BD-Clase5.pdf" style="border:1px solid #ccc;"></iframe>
#consulta MEO


# Clase 6
[BD-Clase6.pdf](/img/user/3-Resources/Archivos/PDFs/Facultad/BD-Clase6.pdf)



# Clase 7
[BD-Clase7.pdf](/img/user/3-Resources/Archivos/PDFs/Facultad/BD-Clase7.pdf)


# Clase 8
[BD-Clase8.pdf](/img/user/3-Resources/Archivos/PDFs/Facultad/BD-Clase8.pdf)

![image-95.png](/img/user/3-Resources/Archivos/image-95.png)
#consulta Que los datos sean válidos ejemplo edad no sea negativo

![image-96.png](/img/user/3-Resources/Archivos/image-96.png)
#consulta  Parcialmente cometida es, si se logra la ejecución exitosamente, la SGBD hace chequeos. Si no se cumplen o hay fallos (se rompe) pasa a fallada. En caso que se garantiza que nunca abortará (Los chequeos dieron correcto) pasa a cometida.




# Clase 9

[BD-Clase9.pdf](/img/user/3-Resources/Archivos/PDFs/Facultad/BD-Clase9.pdf)

![image-97.png](/img/user/3-Resources/Archivos/image-97.png)
#consulta  MEO
![image-98.png](/img/user/3-Resources/Archivos/image-98.png)

