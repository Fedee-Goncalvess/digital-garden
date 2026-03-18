---
{"dg-publish":true,"permalink":"/3-resources/zettelkasten/resume/explicacion-modelo-logico/","created":"2026-03-18T19:09:40.007-03:00","updated":"2026-03-18T19:58:32.174-03:00"}
---

***La idea principal es pasar del modelo conceptual al modelo lógico.*** 

# Que es
El modelo conceptual intenta representar de la forma más descriptiva posible un dominio determinado que no se pueden representar en un [[SGBD\|SGBD]].
Una vez este modelo conceptual esté realizado, buscamos pasar éste modelo conceptual a un modelo lógico, que ya es más cercano a un modelo representable en algún [[SGBD\|SGBD]].

# Cómo lo hacemos
Para ello debemos resolver jerarquías, atributos compuestos, y atributos polivalentes de nuestro modelo conceptual.
Es decir, en un modelo lógico **no odemos tener jerarquías, atributos compuestos o atributos polivalentes**.

## Jerarquía
Dependiendo del tipo de jerarquía, hay dos opciones que solucionan cualquier jerarquía y un caso especial para la Total Exclusiva.
![image-20.png\|564\|538x332](/img/user/3-Resources/Archivos/image-20.png)
#### Total Exclusiva (T,E):
- Dejar todo
- Dejar sólo los hijos
- Dejar sólo el padre

#### Total Superpuesta (T,S): 
**No se puede eliminar al padre**
- Dejar todo
- Dejar sólo al padre

#### Parcial Exclusiva (P,E): 
**No se puede eliminar al padre**
- Dejar todo
- Dejar sólo al padre
#### Parcial Superpuesta (P,S): 
**No se puede eliminar al padre**
- Dejar todo
- Dejar sólo al padre

### Dejar todo
- Aparecen las relaciones **esUn**
- Si entidad hijo **tiene identificador**, no estoy obligado a bajar el del padre
- Si entidad hijo **no tiene identificador, estoy obligado a bajar el del padre**
![image-21.png\|544](/img/user/3-Resources/Archivos/image-21.png)
En este caso, docente no tiene identificador propio. En cambio noDocente sí lo tiene.

***Cardinalidad***
- Los hijos siempre son (1,1)
- Los padres siempre son (0,1)

### Dejar solo al padre
- Todos los atributos hijos pasan al padre
- Deben pasar como **no obligatorios**
- Si un hijo tenía identificador, deja de ser identificador y pasa a ser opcional ya que **nunca un identificador puede ser opcional**
![image-22.png\|491](/img/user/3-Resources/Archivos/image-22.png)
### Dejar solo a los hijos
- Se deben bajar los atributos del padre a cada uno de los hijos
![image-23.png\|523x190](/img/user/3-Resources/Archivos/image-23.png)


## Atributos Compuestos
Dado un atributo compuesto, se tienen dos posibilidades para resolver este atributo compuesto.
La mejor solución es dependiente del dominio en el que esté. Es decir, si es importante algún campo del atributo compuesto que se consultará recurrentemente la mejor opción es considerar atributos individuales.
![image-24.png](/img/user/3-Resources/Archivos/image-24.png)
### Considerar atributos individuales
Todos los atributos simples del compuesto bajan a la entidad
**Ejemplo**
En una remisería se necesita consultar la dirección del cliente, esta es la mejor opción, ya que las consultas son más eficazes.
![image-25.png](/img/user/3-Resources/Archivos/image-25.png)

### Considerar todo en un sólo atributo
Dejo solo un atributo que represente todo el atributo compuesto
**Ejemplo**
La dirección de un alumno no es algo que se consulte recurrentemente a menos sea una emergencia o algo muy particular, puede dejarse almacenado todo junto.
![image-26.png\|383](/img/user/3-Resources/Archivos/image-26.png)
## Atributos Polivalentes
Si una entidad posee un atributo que puede contener más del mismo, se debe agregar una entidad y una interrelación
![image-27.png](/img/user/3-Resources/Archivos/image-27.png)
**Observar cardinalidad:**
- Siempre conviene dejar la cardinalidad en ambos como (0,n)
- En algunos casos donde la entidad que era el atributo polivalente se especifique con cardinalidad (1,x), debo si o sí agregarle un identificador externo de la entidad. Es decir en este ejemplo agregarle dni o legajo.
![image-28.png](/img/user/3-Resources/Archivos/image-28.png)
