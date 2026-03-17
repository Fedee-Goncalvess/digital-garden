---
{"dg-publish":true,"permalink":"/3-resources/zettelkasten/resume/i-and-c-sensores-de-deformacion/"}
---

# Funcionamiento
> [!info] Resistencia de un cable
> $R=\frac{\rho  l}{A}$
> ---
> $\rho$: Resistividad material
> $l$: Largo
> $A$: Sección transversal

![image-14.png](/img/user/3-Resources/Archivos/image-14.png)
Tenemos un cable con longiud $L$ y área $A$, y cierta resistividad material $\rho$
![image-15.png](/img/user/3-Resources/Archivos/image-15.png)
Si se le aplica una fuerza de deformación
![image-16.png](/img/user/3-Resources/Archivos/image-16.png)
El cable se deforma, y gana más longitud, y pierde sección transversal.
Esto visto desde la fórmula de resistencia de un cable podemos entonces ver con claridad que la resistencia total del cable aumenta cuando se estira. 
$$ 
R=\frac{\rho  l}{A} \rightarrow \space R\uparrow= \frac{\rho (l+\Delta l)}{A-\Delta A} \space \rightarrow \space R=\frac{\rho  l\uparrow}{A\downarrow}
$$
*¿Por qué se estira?*
A partir de la [[Ley de Hooke\|Ley de Hooke]], podemos hacer uso de esta propiedad en materiales, para mantenernos en la región elástica y medir. Podemos usar un material (naturalmente metales ya que tienen una región de elasticidad más grande) para medir estiramientos o deformaciones. 
 
$\frac{F}{A} = \sigma$ : Esfuerzo (Fuerza sobre área)

$\epsilon=\frac{\Delta L}{L_{0}}$ : Deformación

$E$ : Módulo de yung o elasticidad de material

![image-17.png](/img/user/3-Resources/Archivos/image-17.png)

**Ejemplo**
Se somete un hilo a un esfuerzo longitudinal.
Las magnitudes que varían para que la resistencia cambie son, longitud, área, y resistividad del material:
$$
dR=d \rho (\frac{\rho l}{A})+dL(\frac{\rho l}{A})+dA\frac{\rho l}{A}
$$
$$
dR= \frac{L}{A}d\rho +\frac{\rho}{A} dL+dA (\rho L.A^{-1})
$$
$$
dR= \frac{L}{A}d\rho +\frac{\rho}{A} dL-\frac{l}{A^2}dA
$$
Luego si dividimos por R:
$$
\frac{dR}{R}= \frac{d\rho}{\rho}+\frac{dL}{L} -\frac{dA}{A}
$$

Pero podemos demostrar que todas estas magnitudes pueden depender solo del cambio longitudinal.
Entonces, el cambio de longitud al aplicar una fuerza F a una pieza unidimensional viene dado por la ley de Hooke:
$$
\sigma=\frac{F}{A}=\frac{E.dL}{L}=E.\epsilon
$$
**Pasamos ahora al término de la magnitud de área:**
Si además de una dimensión longitudinal posee una dimensión transversal D, la ley de Poisson establece:
$$
\micro = -\frac{dD/D}{dL/L}
$$

Si el hilo conductor tiene una sección circular de diámetro D:
$$
A=\frac{\pi D^2}{4}
$$
entonces usando $\micro$ y analizando el cambio de sección transversal:
$$
\frac{dA}{A}= \frac{2dD}{D}= -2\micro
\frac{dL}{L}$$
*Mostramos como el cambio de sección transversal puede depender solo de la longitud*

**Pasamos ahora al término de resistividad material**
La variación de resistividad experimentada por un esfuerzo mecánico se conoce como efecto piezorresistivo. 
En el caso de los metales, los cambios porcentuale de resistividad son proporcionales a los de volumen:
$$
\frac{d\rho}{\rho}=C \frac{dV}{V}
$$
siendo C la constante de Bridgman.
Utilizando los resultados anteriores tenemos entonces que
$$
V= \frac{\pi D{^2}}{4}L
$$
Analizando el cambio de volumen del material:
$$
\frac{dV}{V}= \frac{dL}{L}+\frac{2dD}{D}
$$
Tenemos que $\micro = -\frac{dD/D}{dL/L}$ -> $-\micro \frac{dL}{L} = dD/D$
Por lo que el volumen puede quedar también dependiendo exclusivamente de la longitud
$$
\frac{dV}{V}= \frac{dL}{L}+\frac{2dD}{D}=(1-2\micro)\frac{dL}{L}
$$
*Mostramos que el cambio de resistividad material puede depender solo de la longitud, al menos para los metales*

Entonces ahora podemos reemplazar en nuestra ecuación
$$
\frac{dR}{R}= \frac{d\rho}{\rho}+\frac{dL}{L} -\frac{dA}{A}
$$
Reemplazamos:
$$
\frac{dR}{R}= \frac{dL}{L}(1+2\micro + C(1-2\micro)) = \frac{KdL}{L}=K\epsilon
$$
**Para pequeñas deformaciones**
$$
R=R_{0}(1+x)
$$
con $R_0$ la resistencia en reposo y $x=K\epsilon$

