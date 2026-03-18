---
{"dg-publish":true,"permalink":"/2-areas/facultad/ejercicios/cd-and-mc-tp-1-cuestionario-de-c/","created":"2026-03-16T18:47:12.409-03:00","updated":"2026-03-18T11:43:35.663-03:00"}
---

# Cuestionario
## Investigue sobre los distintos tipos de datos en C y en particular indique cuantos bits contiene cada tipo de dato y que rango de valores pueden representar cada tipo.

<div class="transclusion internal-embed is-loaded"><a class="markdown-embed-link" href="/3-resources/zettelkasten/resume/tipos-de-datos-en-c/#enteros" aria-label="Open link"><svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="svg-icon lucide-link"><path d="M10 13a5 5 0 0 0 7.54.54l3-3a5 5 0 0 0-7.07-7.07l-1.72 1.71"></path><path d="M14 11a5 5 0 0 0-7.54-.54l-3 3a5 5 0 0 0 7.07 7.07l1.71-1.71"></path></svg></a><div class="markdown-embed">



### Enteros

| Tipo      | Tamaño     | Formato |
| --------- | ---------- | ------- |
| char*     | 1 Byte     | %c      |
| short     | 2 Bytes    | %hd     |
| int       | 4 Bytes    | %d      |
| long      | 4/8 Bytes* | %lg     |
| long long | 8 Bytes    | %lld    |
- **Se pueden determinar como `signed` o `unsigned`, modifica el rango pero no el tamaño**
- **Unsigned con formato `%u` = 4bytes**
- * el char es en realidad un int, por lo tanto puede utilizarse el formato de char `%c` o puede utilizarse el formato de `%hhd` para interpretarlo como un número.
- ** según arquitectura


</div></div>


<div class="transclusion internal-embed is-loaded"><a class="markdown-embed-link" href="/3-resources/zettelkasten/resume/tipos-de-datos-en-c/#flotantes" aria-label="Open link"><svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="svg-icon lucide-link"><path d="M10 13a5 5 0 0 0 7.54.54l3-3a5 5 0 0 0-7.07-7.07l-1.72 1.71"></path><path d="M14 11a5 5 0 0 0-7.54-.54l-3 3a5 5 0 0 0 7.07 7.07l1.71-1.71"></path></svg></a><div class="markdown-embed">



### Flotantes

| Tipo        | Tamaño      | Formato |
| ----------- | ----------- | ------- |
| float       | 4 Byte      | %f      |
| double      | 8 Bytes     | %lf     |
| long double | 8/16 Bytes* | %Lf     |
- **NO se pueden determinar como signed o unsigned.**
- * según arquitectura
- Pueden dar soporte a los valores `INFINITY`, `-0.0` y `NaN`
	- Solo sirven en casos como `1.0/0.0 == INFINITY`, o `1.0/0.0 == -INFINITY`

</div></div>


<div class="transclusion internal-embed is-loaded"><a class="markdown-embed-link" href="/3-resources/zettelkasten/resume/tipos-de-datos-en-c/#derivados" aria-label="Open link"><svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="svg-icon lucide-link"><path d="M10 13a5 5 0 0 0 7.54.54l3-3a5 5 0 0 0-7.07-7.07l-1.72 1.71"></path><path d="M14 11a5 5 0 0 0-7.54-.54l-3 3a5 5 0 0 0 7.07 7.07l1.71-1.71"></path></svg></a><div class="markdown-embed">



## Derivados
[[Punteros en C\|Punteros en C]]

| Tipo    | Tamaño                    |
| ------- | ------------------------- |
| Puntero | 4/8 bytes                 |
| Array   | `sizeof(tipo) * cantidad` |


</div></div>


## Investigue sobre los modificadores: static, volatile, register, const. Busque un ejemplo de cada caso.

<div class="transclusion internal-embed is-loaded"><a class="markdown-embed-link" href="/3-resources/zettelkasten/resume/modificadores-en-c/" aria-label="Open link"><svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="svg-icon lucide-link"><path d="M10 13a5 5 0 0 0 7.54.54l3-3a5 5 0 0 0-7.07-7.07l-1.72 1.71"></path><path d="M14 11a5 5 0 0 0-7.54-.54l-3 3a5 5 0 0 0 7.07 7.07l1.71-1.71"></path></svg></a><div class="markdown-embed">








</div></div>

## Repase el uso de las sentencias del pre-procesador de C, entre ellas: `#include`, `#define`, `#ifdef` y `typedef`.

<div class="transclusion internal-embed is-loaded"><a class="markdown-embed-link" href="/3-resources/zettelkasten/resume/sentencias-del-pre-procesador-en-c/" aria-label="Open link"><svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="svg-icon lucide-link"><path d="M10 13a5 5 0 0 0 7.54.54l3-3a5 5 0 0 0-7.07-7.07l-1.72 1.71"></path><path d="M14 11a5 5 0 0 0-7.54-.54l-3 3a5 5 0 0 0 7.07 7.07l1.71-1.71"></path></svg></a><div class="markdown-embed">








</div></div>


## ¿Qué es una constante de carácter? ¿qué es una cadena de caracteres?

## ¿Cuál es la diferencia entre una variable local y una global? ¿Por qué utilizaría una u otra? 
![[Diferencia entre variable local y global\|Diferencia entre variable local y global]]

## Describa todos los operadores lógicos de C ¿cúal es la diferencia entre los operadores && y &? ¿entre || y |? ¿y entre ! y ~? ¿Qué es una máscara de bits?
![[Operadores lógicos de C\|Operadores lógicos de C]]

## Qué es un prototipo de función en C? ¿Cuáles son las alternativas para pasar argumentos a una función? ¿Cómo se retorna un valor desde una función?
![[Prototipo de función en C\|Prototipo de función en C]]

## Repase el concepto de punteros y arreglos. Explique con ejemplos la relación entre ambos. 
![[Punteros en C\|Punteros en C]]

## Investigue sobre los tipos de variables struct y union (estructuras y uniones) en C. Busque un ejemplo de cada caso.

<div class="transclusion internal-embed is-loaded"><a class="markdown-embed-link" href="/3-resources/zettelkasten/resume/tipos-de-datos-en-c/#definidos-por-usuario" aria-label="Open link"><svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="svg-icon lucide-link"><path d="M10 13a5 5 0 0 0 7.54.54l3-3a5 5 0 0 0-7.07-7.07l-1.72 1.71"></path><path d="M14 11a5 5 0 0 0-7.54-.54l-3 3a5 5 0 0 0 7.07 7.07l1.71-1.71"></path></svg></a><div class="markdown-embed">



## Definidos por usuario
### Struct
#### Definición
Secuencia de tipos de datos, alocados secuencialmente.
```c
struct Ejemplo {  
char a; // 1  
int b; // 4  
};
```
#### Tamaño
**El tamaño del struct es al menos, tan grande como la suma de los tamaños de sus campos**.
El struct agrega *padding* entre los datos para alinear datos y hacer el acceso más eficiente, por lo que el tamaño del ejemplo de arriba puede no ser 5 bytes, sino 8. 
**Nunca hay padding antes del primer campo**
#### Acceso a los campos
Como hay padding entre los datos, **no se puede utilizar como un array**, pero se puede apuntar al primer campo ya que como se mencionó antes, al inicio del struct no hay padding.

### Union
#### Definición
Secuencia de tipos de datos, alocados solapandose.
```c
union U {
    char c;    // 1 byte
    int i;     // 4 bytes
    double d;  // 8 bytes
};

sizeof(union U) == sizeof(double)  // normalmente 8
```
#### Tamaño
**El tamaño del union es del tamaño del tipo de dato más grande alocado**.
El union también puede agregar *padding*.
**Nunca hay padding antes del primer campo**
#### Acceso a los campos
Como se solapan los datos, el puntero al union siempre apunta al primer y único campo, cual coinciden todos. Es decir un puntero a la unión del ejemplo de arriba apunta tanto al inicio de char, como al inicio de int y double.

#### Problemas
- Si se aloja un dato más grande que el union, el excedente no se especifica y puede no dar una buena representación. 
- Si se guarda un tipo de dato distinto al que luego se lee, se realiza *type punning*. Básicamente se interpreta como otro tipo de dato pero **no es una conversión**. Normalmente se utiliza si solo te interesan los bits y no el valor que es interpretado

### Enum
#### Definición
Define un conjunto de valores simbólicos con nombre que representan enteros

```c
enum Error {
    OK = 0,
    TIMEOUT = 100,
    NOT_FOUND = 404
};
```
#### Tamaño
El tamaño de enum es el de un entero, de 4 bytes
#### Diferencia con `#Define`
El `#Define` es pre-procesador, por lo que el enum es comunmente utilizado en 
- Estados
- Códigos de error
- Opciones/Switch
Ya que es **visible al programador**, es posible debuggear y es más seguro. 
Si se utilizara el `#Define` para códigos de error, al recibir un código de error, el programador vería un número cuando con enum se podría ya declarar fácilmente qué código simboliza qué error.


</div></div>


## ¿Qué son los campos de bit de una estructura y cuál es la utilidad directa a bajo nivel?
![[Campos de bits en C\|Campos de bits en C]]