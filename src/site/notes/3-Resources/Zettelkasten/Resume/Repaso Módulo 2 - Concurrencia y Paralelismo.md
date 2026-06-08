---
{"dg-publish":true,"permalink":"/3-resources/zettelkasten/resume/repaso-modulo-2-concurrencia-y-paralelismo/","created":"2026-06-08T01:12:58.846-03:00","updated":"2026-06-08T01:57:11.277-03:00"}
---

# PMA

- Si un canal tiene múltiples receptores, si o sí se necesita coordinador. Ya que si deben terminar todos los procesos receptores, podría suceder que al chequear
```java
if (not empty canal){
	receive canal();
}
```

- Si el coordinador se comunica con un solo proceso, puede esperar hasta que se actualice el canal de ese proceso
- Si se comunica con más de un proceso, debe tener un canal global donde pueda recibir si hubo algún cambio entre todos los procesos *(EVITA BUSY WAITING)* 
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

