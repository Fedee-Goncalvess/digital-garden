---
{"dg-publish":true,"permalink":"/3-resources/zettelkasten/resume/repaso-modulo-2-concurrencia-y-paralelismo/","created":"2026-06-08T01:12:58.846-03:00","updated":"2026-06-11T14:39:30.460-03:00"}
---

# PMA
## Recordar
- Existen `channels` que pueden ser compartidos por varios procesos, y actuan como una lista ordenada.
- Se puede utilizar un `empty channel` para saber si esta vacío o no
- Si se necesita una respuesta directa a una persona, se debe realizar un arreglo de channels según id `chan Respuesta[N]();`
- Si un canal tiene múltiples receptores y los procesos deben hacer algo distinto cuando no hay mensajes en el canal, si o sí se necesita coordinador. Ya que, podría suceder que al chequear
- ```java
	if (not empty canal){
		receive canal();
	}
```
- Si un **canal tiene múltiples receptores y los procesos deben finalizar, si o sí se necesita coordinador**. Ya que si deben terminar todos los procesos receptores, podría suceder que al chequear
```java
if (not empty canal){
	receive canal();
}
```

- Si el coordinador se comunica con un solo proceso, puede esperar hasta que se actualice el canal de ese proceso
- Si se comunica con más de un proceso, debe tener un canal global donde pueda recibir si hubo algún cambio entre todos los procesos *(EVITA BUSY WAITING)* 
```c
Process Coordinador{
	while(not termino){
		receive(AVISO)
	}
}
```
- Si debo atender N pedidos, tengo que hacer que el coordinador procese esa cantidad (contarlos) y cuando se procese esa cantidad, avisar a los procesos que esperan solicitudes mediante sus respectivos canales con un identificador de corte.  Ej: id= -1
```java
Process Coordinador {
    int idV;
    int idC;
    texto plato;
    
    while (cantAtendidos < C){
        receive vendedorListo(idV);
        if (not empty (Pedido)){
            receive  Pedido(idC, p);
            send Venta[idV](idC,p);
            cantAtendidos++;
        }else {
            send Venta[idV](0,NOT);
        }
    }
    
    for i= 1..3{
        send Venta[i](-1,"VACIO");
    }
    for i= 1..2{
        send platosCocina(-1,"VACIO");
    }
}
```

## Coordinador debe ser avisado y debe terminar
```java
Cliente [id = 1..N]{
	send PedirAlgo();
	send AvisoCoordinador();
}

Empleado [id = 1..P ]{
	boolean 
	while(not termino)
}

Coordinador{
	While (cantClientesAtendidos < N){
		receive AvisoCoordinador()
		if (canalCliente){
			...
			cantClientesAtendidos++
		}
		[] (canalEmpleado){
			...
		}
		fi
		
		if()
	}
	for i= 0..P{
		send TerminarProcesos("TERMINAR")
	}
	
}
```

# PMS
## Recordar
- No existen canales, son comunicaciones bloqueantes entre procesos. `ProcesoA!port() -> ProcesoB?port()`
- El comodín canal `Proceso[*]` es no determinístico. Es decir, entre muchos procesos va a elegir al azar. No será en orden
- Para hacer **en orden** y **maximizando concurrencia** evitando bloqueo, se debe utilizar un ***buffer***
- Si un proceso se quiere comunicar con cualquiera de un grupo de procesos (cliente-empleados) se necesita un coordinador ya que **PMS debe especificar a cual proceso** se le hace 
- Cuando se hace un recibo `Proceso?` sin condición booleana, si no se sincroniza el mensaje *(todavía nadie mandó ningún mensaje)* se queda **bloqueado**. Por lo que si el proceso no debe estar bloqueado se debe utilizar el *IF FI* o el *DO OD*
- Para recepción se puede utilizar el comodín `Proceso[*]?` pero ***NO SE PUEDE USAR PARA ENVÍO***. Si se quisiera enviar a todos los procesos se debería hacer un *for iterando con una variable i*
- DUDA Esta mal escuchar de todos con el comodín si solo hay un proceso que puede enviar mensaje?
	- Seguramente tengamos que guardarnos en un auxiliar su id y utilizarlo correctamente.

# ADA
## Recordar
- Las ENTRY CALLS son colas ordenadas que no podemos manipular, solo preguntar por la cantidad de entry calls. `nombreEC'count` 
- El main del programa debe tener código, al menos null.
- Para manejar entrys con prioridad, se utiliza un SELECT de ACCEPTS con WHEN (entryPrioritaria'count = 0) -> ACCEPT menor prioridad
- Sintaxis de parametros (A,B: IN integer; C: OUT char)
- Cuando hay clientes y más de un servidor, se necesita coordinador