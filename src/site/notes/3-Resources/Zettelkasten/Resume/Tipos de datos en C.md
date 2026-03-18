---
{"dg-publish":true,"permalink":"/3-resources/zettelkasten/resume/tipos-de-datos-en-c/","created":"2026-03-18T10:15:55.214-03:00","updated":"2026-03-18T11:42:31.812-03:00"}
---

El [[Format Specifier en C\|Format Specifier]] lo saco de [esta página](https://devdocs.io/c/io/fscanf), incluido con los [tipos de datos.](https://devdocs.io/c/language/arithmetic_types)
C define varios tipos d datos primitivos, y los valores típicos en sistemas de 32/64 bits son:
# Tipos
## Básicos

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
## Derivados
[[Punteros en C\|Punteros en C]]

| Tipo    | Tamaño                    |
| ------- | ------------------------- |
| Puntero | 4/8 bytes                 |
| Array   | `sizeof(tipo) * cantidad` |

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

## Especiales
