---
{"dg-publish":true,"permalink":"/3-resources/zettelkasten/resume/sensores/"}
---

# Sistemas de Medida
## Características Estáticas
### Exactitud y Precisión
![image-2.png](/img/user/3-Resources/Archivos/image-2.png)
#### Exactitud
- Cualidad del instrumento de dar lecturas **próximas** al valor verdadero de la magnitud medida.
#### Precisión
- Grado de **reproducibilidad de las medidas** ***ESTO ES LO MÁS IMPORTANTE***

La exactitud se determina mediante calibración estática a partir de un patrón de referencia al menos 10 veces más exacto que el sensor que se calibra

### Sensibilidad
***Pendiente de la curva de calibración***
$$
Sensibilidad = \frac{dy}{dx}
$$
Si la curva es el estilo  $y=mx+b$  la sensibilidad sería la pendiente de la recta $m$ . 

*En sensores, interesa tener una sensibilidad alta y contante*

### Rango y Alcance
#### Rango
Valores máximo y mínimo que pueden ser medidos
#### Alcance
Diferencia entre valor máximo y mínimo de medida

#### Salida a fondo de escala
Diferencia entre valor máximo y mínimo de salida del alcance

![image-1.png](/img/user/3-Resources/Archivos/image-1.png)
Se identifican los límites superior e inferior de cada variable, y luego el campo de medida es el alcance. 

### Repetibilidad / Reproducibilidad 
***Estrechamente asociados a la [[3-Resources/Zettelkasten/Resume/Sensores#Precisión\|precisión]]***

#### Repetibilidad
Grado de correspondencia entre sucesivas mediciones bajo las mismas condiciones y en un período corto

#### Reproducibilidad
Idem que Repetibilidad, pero bajo distintas condiciones y en un período largo de tiempo

### No Linealidad
***Máxima desviación de la curva de calibración con respecto a la línea recta que se haya aproximado.***

Suele expresarse en % con respecto al alcance y suele denominarse como error de linealidad e incluso como linealidad.
$$

\frac{Desviación\space Máxi ma\rightarrow h}{Alcance\rightarrow (Xs-Xi)}100\%
$$

![image-2.png](/img/user/3-Resources/Archivos/image-2.png)
Aquí se ven dos aproximaciones lineales distintas. Cada una con error distinto.

$h$ -> Desviación máxima: Si se utilizara la recta aproximada, podemos ver que para un valor de medida entre$X_{s}$ y $X_{i}$, tenemos $y_{real}(X_0)=y_{0}$ mientras que $y_{aproximado}(X_{0})<y_{real}(X_{0})$. 

La primer imagen utiliza los extremos de la curva como aproximación lineal.
La segunda imagen no especifica, pero tiene una menor desviación.

### Zona Muerta
***Campo de valores de la variable, que no hacen variar la indicación***

![image-3.png](/img/user/3-Resources/Archivos/image-3.png)
En algunos potenciómetros angulares de una vuelta sin fin, el ángulo entre $T_2$ y $T_3$ tiene una zona muerta, donde si vemos la resistencia que presenta en un gráfico, podemos ver que no proporciona variación.

### Histéresis
***Diferencia en la medida, dependiendo del sentido en la que se haya alcanzado***

**Ejemplo:**
En una balanza de 0-100kg, comenzar de 0kg y subir progresivamente hasta 50kg marcará en la balanza 49kg.
Al llegar a 100kg, volvemos a bajar a 50kg y ahora la balanza indica 51kg. 
***Esta curva de calibración presenta histéresis**

![image-4.png](/img/user/3-Resources/Archivos/image-4.png)
Así se vería un gráfico de histéresis.

### Saturación
***Nivel de entrada a partir del cual la sensibilidad disminuye de forma significativa***

![image-5.png](/img/user/3-Resources/Archivos/image-5.png)
A partir de un punto a medir, comienza a perderse sensibilidad

### Resolución
***Incremento mínimo de la variable de entrada que ofrece un cambio medible a la salida***

Es decir, la variación necesaria en magnitud para que la salida sea medible. 

![image-6.png](/img/user/3-Resources/Archivos/image-6.png)

### Medidas de error
#### Error 
$Error=Valor\space medido - Valor\space real$
#### Error relativo
$\frac{Error}{Valor\space real}100\%$

#### Error en referencia al fondo de escala
$\frac{Error}{Valor\space de \space fondo\space de\space escala}100\%$

#### Clase de precisión
$\frac{Error\space máxi mo \space en \space rango\space de \space medida}{Valor\space de \space fondo\space de\space escala}100\%$


### Calibración
#### Calibración a un punto
Consiste en actuar sobre el sensor de forma que para un punto concreto, la salida sea lo más exacta posible. 

**Ejemplo**
Para una balanza, lo ideal es que la salida siempre sea 0kg cuando no tiene ningún peso encima. Si fuera el caso contrario, se debería de hacer este tipo de calibración. Así con velocímetros, acelerómetros, etc. 
![image-7.png\|505](/img/user/3-Resources/Archivos/image-7.png)
Representación de la curva de calibración ideal y la que corresponde a dos instrumentos reales. Se puede observar que el instrumento 1 proporciona una salida que siempre es un cierto nivel $\Delta S_{1}$ , mayor que el ideal. El instrumento 2, además de presentar un cierto nivel menor $\Delta S_{2}$ tiene una sensibilidad diferente a la ideal.

#### Calibración del cero y de la sensibilidad
Para ajustar perfectamente una curva de calibración lineal, se debe ajustar dos puntos o un punto, y la pendiente o sensibilidad. Idealmente un fabricante proporciona mandos externos para modificar el nivel (*offset*) y la sensibilidad o ganancia del sistema (*gain*). 

El procedimiento a seguir es inicialmente ajustar el *offset* para que haya la medición de cero sea verdadera. Y luego se ajusta la *gain* para aumentar o bajar la sensibilidad. Este último paso requiere de otro punto conocido para que la salida sea la deseada.

![image-8.png](/img/user/3-Resources/Archivos/image-8.png)
Calibración del cero y de la ganancia. 
a) Situación original
b) Ajuste del nivel de cero
c) Ajuste de sensibilidad
## Características Dinámicas



