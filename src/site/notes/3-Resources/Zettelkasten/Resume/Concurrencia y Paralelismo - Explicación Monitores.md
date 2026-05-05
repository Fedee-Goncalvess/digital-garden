---
{"dg-publish":true,"permalink":"/3-resources/zettelkasten/resume/concurrencia-y-paralelismo-explicacion-monitores/","created":"2026-04-29T00:27:18.435-03:00","updated":"2026-04-29T00:58:35.354-03:00"}
---

## N procesos 1 recurso - Monitor como Recurso
### Sin orden - Monitor como Recurso 
Existen N personas que desean utilizar un cajero automático. En este primer caso no se debe tener en cuenta el orden de llegada de las personas (cuando está libre cualquiera lo puede usar). Suponga que hay una función UsarCajero() que simula el uso del cajero.

``` pascal
Monitor Cajero{
	Procedure PasarAlCajero () { 
	UsarCajero (); 
	} 
} 

Process Persona [id: 0..N-1] {
	…. 
	Cajero.PasarAlCajero(); 
	…. 
}
```

El monitor se utiliza representando al mismo recurso. De manera que el monitor solo cumple la función de Exclusión Mutua que ya está implícito en los Monitores.
### Con Orden - Monitor como Acceso
Existen N personas que desean utilizar un cajero automático. En este segundo caso se debe tener en cuenta el orden de llegada de las personas. Suponga que hay una función UsarCajero() que simula el uso del cajero.

En este caso los clientes deben solicitar el uso del cajero, cuando le llega el turno llama a la función UsarCajero() que simule el uso, y luego debe avisar que salió para dejar pasar al siguiente.

**Se debe tener una variable que indique el estado del recurso** (si está libre o alguien lo está ocupando)
- ***si está libre el usuario no debe esperar, debe pasar a usarlo***. 
- ***si está ocupado debe esperar su turno dormido en una variable condición.***

```pascal
Monitor Cajero{ 
	bool libre = true;
	cond cola;
	int esperando = 0; 
	
	Procedure Pasar () { 
		if (not libre) { 
			esperando ++;
			wait (cola);
		} else libre = false;
	} 
	
	Procedure Salir () {
		if (esperando > 0 ) {            
			esperando --; signal (cola);
		} else libre = true;   //Poner en libre solo si no se espera nadie
	} 
}

Process Persona [id: 0..N-1] { 
	Cajero.Pasar (); 
	UsarCajero(); 
	Cajero.Salir(); 
}
```

### Con Prioridad - Monitor como Acceso

## N clientes y M empleados
### Con Orden 
### Interacción entre Procesos

## Barrera 

## N clientes y 1 Servidor

## N clientes y 2 Servidores