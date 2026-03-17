---
{"dg-publish":true,"permalink":"/2-areas/facultad/ejercicios/cd-and-mc-tp-1-ejercicios-de-avr/"}
---


# Ejercicios de Simulación
## Analice el programa ejemplo de la Fig.1. Explique qué hacen las sentencias de C:

```c
DDRD = 0xFF;
DDRC &= ~(1<<PORTC0);
PORTC |= (1<<PORTC0);
```

¿Qué representan `DDRx`, `PORTCx`? ¿Dónde y cómo están definidos?

### Respuesta 
#### DDRx
Data Direction Register (Registro X)
- Contienen un arreglo que indican el comportamiento del Port X (que es bidireccional)
- El puerto X tiene 8 puertos por lo que va de 0-7
- 0->Entrada
- 1->Salida 
- Con DDRD = 0xFF estamos indicando que todos los 8 bits de configuración del puerto D están en modo de Output
#### PORTCx 
Puerto C para **escritura**. Este puerto se utiliza para escribir. Contiene los 8 pines de PORTC7 a PORTC0. 

#### PINC
Puerto C para **lectura**. Este puerto se utiliza para leer, y tambien contiene los 8 pines de PINC7 a PINC0.
#### 
<div class="transclusion internal-embed is-loaded"><div class="markdown-embed">

<div class="markdown-embed-title">

# Sentencia de Pull Up interno

</div>


## Entradas Digitales
Para [[|microcontroladores]] en los puertos de entrada, suelen tener definidos por defecto una configuración de pull up interna, con el objetivo de evitar tener puertos flotantes. Donde estos puertos quedan configurados como entrada, pero nunca se les establece tensión por defecto por lo que "flotan" entre alto y bajo con alta impedancia. En otras palabras, no tiene referencia a nada. Por lo que cualquier pequeña tensión que se le de influye si es realmente HIGH o LOW.

### Ejemplo Puertos I/O de Microchip ATMega/AVR
```c
DDRC &= ~(1<<PORTC0);
PORTC |= (1<<PORTC0);
```
Se configura el Data Direction Register para indicar que el pin 0 del puerto C debe ser de entrada. 
- `1<<PORTC0`: Desplazamos la máscara 1 a la posición del puerto C pin 0. 
	- `00000001`
- `~(1<<PORTC0)`: Negamos toda la máscara
	- `11111110`
- `DDRC &= ~(1<<PORTC0)`: And para forzar la configuración del pin 0 del puerto C en modo entrada.
	- `XXXXXXXX & 11111110 = XXXXXXX0`
- `PORTC |= (1<<PORTC0)`: Misma idea pero para forzar valor 1 en pin 0 del puerto C
	- Esto es configurar el pin 0 del puerto C como Pull Up resistor interno. Es decir ahora tendrá por default una tensión alta.


</div></div>



## ¿Qué condición se evalúa en la expresión dentro del `if`?

```c
if (PINC & (1<<PINC0)
```

### Respuesta
La condición evalúa que el PIN 0 del puerto C esté en alto, sin importar su configuración.

## Explique qué hace la siguiente sentencia de C dentro del `else`:

```c
PORTD |= (1<<PORTD0) | (1<<PORTD2) | (1<<PORTD4) | (1<<PORTD6);
```
#### Respuesta
Analizo del puerto D de escritura, y pongo todos los puertos 0,2,4 y 6 en 1, dejarlos encendidos por 100ms, y luego dejarlos todos en 0.

|  X  | **1** |  X  | **1** |  X  | **1** |  X  | **1** |
| :-: | :---: | :-: | :---: | :-: | :---: | :-: | :---: |
|  0  |   0   |  0  |   0   |  0  |   0   |  0  |   0   |


### ¿Cómo sería la sintaxis para establecer el nivel lógico de estos bits a **nivel bajo** sin afectar el estado lógico del resto de los bits del puerto?
#### Respuesta
```c
PORTD &= ~((1<<PORTD0) | (1<<PORTD2) | (1<<PORTD4) | (1<<PORTD6));
```
- Entonces tenemos, primero 
	- `(1<<PORTD0) | (1<<PORTD2) | (1<<PORTD4) | (1<<PORTD6); = = 01010101` 
- Luego lo negamos
	- `~(01010101) = 10101010`
- Y por último hacemos and con PORTD 
	- `XXXXXXXX & 10101010 = X0X0X0X0`

## Explique cómo funciona la función:

```c
_delay_ms()
```

de la biblioteca **AVR Libc ()***
### Respuesta

<div class="transclusion internal-embed is-loaded"><div class="markdown-embed">

<div class="markdown-embed-title">

# _delay_ms

</div>



Hay dos posibilidades internamente de `_delay_ms`

# Moderno (`__builtin_avr_delay_cycles`)
Esta es la versión utilizada actualmente, que es la más precisa.

##### ***Código***
```
__tmp = ((F_CPU) / 1e3) * __ms;
__ticks_dc = (uint32_t)(ceil(fabs(__tmp)));
__builtin_avr_delay_cycles(__ticks_dc);
```

Simplemente calcula cuántos ciclos de reloj equivalen al tiempo pedido y le dice al compilador que genere exactamente esa cantidad de NOPs/loops. Es la versión más precisa.
`__ms` son los milisegundos que se pasan en el argumento de `_delay_ms()`

**Ejemplo:** `F_CPU = 16000000`, `_delay_ms(1)`
```
__tmp = (16000000 / 1000) * 1 = 16000 ciclos
```



## Lógica
Con el [[3-Resources/Zettelkasten/Resume/F_CPU\|F_CPU]] ya definido, la función toma este valor y lo divide por 1000, ya que F_CPU son ciclos por segundo (Hz) y nosotros estamos haciendo delays de milisegundos (ms). Una vez esto, calcula la cantiad de ciclos/instrucciones NOPs, o loops que debe realizar para simular el retardo especificado en el argumento. Es decir, si el CPU tarda 1 ms en realizar una instrucción, cuando se utilice `_delay_ms(10)` deberá realizar 10 instrucciones NOPs para que el programa simule con software, un delay de 10ms. 

# Compatible/Legacy

##### ***Código***
```
__tmp = ((F_CPU) / 4e3) * __ms;
_delay_loop_2(__ticks);
```

Divide por **4** porque `_delay_loop_2` es un loop que consume **4 ciclos por iteración**. Entonces calcula cuántas iteraciones del loop se necesitan.

`__ms` son los milisegundos que se pasan en el argumento de `_delay_ms()`

**Ejemplo:** `F_CPU = 16000000`, `_delay_ms(1)`
```
__tmp = (16000000 / 4000) * 1 = 4000 iteraciones del loop
4000 iteraciones × 4 ciclos = 16000 ciclos  ✓
```
**Ejemplo:** `F_CPU = 16000000`, `_delay_ms(2)`
```
__tmp = (16000000 / 4000) * 2 = 8000 iteraciones del loop
8000 iteraciones × 4 ciclos = 32000 ciclos  ✓
```


## Lógica
En el caso de que no exista `__builtin_avr_delay_cycles`, se utiliza un loop escrito que se sabe con exactitud que tarda 4 ciclos.  
```c
; _delay_loop_2 en ensamblador AVR: 
loop: 
	sbiw r24, 1 ; 2 ciclos (resta 1 al contador) 
	brne loop ; 2 ciclos (salta si no es cero) 
; Total: 4 ciclos por vuelta 
```
Con esto en mente se puede aprovechar este loop, y determinar cuantas veces debería repetir este loop, para que la cantidad de ciclos sean los necesarios para el delay a cierta [[3-Resources/Zettelkasten/Resume/F_CPU\|F_CPU]].  


# Caso Especial (Delay demasiado largo)
##### ***Código***
```c
else if (__tmp > 65535) // No entra en un uint16_t 
{ 
	__ticks = (uint16_t)(__ms * 10.0); 
	while(__ticks) { 
		_delay_loop_2(((F_CPU) / 4e3) / 10); // espera 1/10 ms 
		__ticks--; 
	} 
} 
```

## Lógica
En este caso, cuando los ms indicados ene la argumento pasan el límite de uint16_t, se fraccionan los ms y se hace un loop de delays. Es decir, se fraccionan los ms pedidos que son demasiado grandes, en delays mas cortos repetidos hasta llenar los ms indicados.

</div></div>

## Analice el resultado de la compilación: errores, advertencias, memoria de datos y de programa utilizada. 

## Analice las dependencias externas: examine y comprenda qué función cumple la línea:

```c
#include <avr/io.h>
```

## Simule el programa paso por paso con el simulador integrado de **Microchip Studio 7**. Examine las ventanas de registros del MCU, de ciclos de reloj consumidos y el comportamiento de los puertos I/O utilizados.

## Realice en **Proteus**, un circuito que incluya el MCU, ocho pulsadores y ocho LEDs para simular el programa desarrollado. Simule y verifique el comportamiento del mismo. Utilice el archivo `.elf` para depurar el programa paso a paso.