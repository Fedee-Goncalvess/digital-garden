---
{"dg-publish":true,"permalink":"/3-resources/zettelkasten/resume/repaso-modulo-1-concurrencia-y-paralelismo/","created":"2026-05-06T17:11:36.877-03:00","updated":"2026-05-07T15:15:39.473-03:00"}
---

# Dudas
- *Resolver con SENTENCIAS AWAIT ($\langle \rangle$ y/o $\langle \text{await B; S} \rangle$) el siguiente problema. Hay un médico que debe atender a 15 pacientes (de a uno a la vez) de acuerdo con el turno de cada uno de ellos (cada paciente ya conoce su turno). Debe asegurarse de que nunca haya dos pacientes al mismo tiempo en el consultorio. Notas: todos los procesos deben terminar.*
	Hacerlo sin médico es facil es que los procesos esperen el anterior. Pero se debería modelar el médico? 
	El turno es el ID o numero aleatorio?

- Se pueden poner los id de 1..N y los arreglos arrancan con índice 1 o deben arrancar con índice 0. Como lo aclaro? Ejemplo `turno[1:n] = ([n] 0);`
- Importa si uso muchas variables o no simplifico el uso de variables?
- Puedo hacer orden de llegada en await con [[3-Resources/Zettelkasten/Resume/Repaso Módulo 1 - Concurrencia y Paralelismo#N procesos 1 Recurso (Orden de llegada + Prioridad)\|Orden con prioridad]] en vez de con [[3-Resources/Zettelkasten/Resume/Repaso Módulo 1 - Concurrencia y Paralelismo#Ticket\|Ticket]]?
- En monitores, si tengo lógicas distintas en un mismo monitor, podría separarlos en varios monitores? Debería o es indistinto?
- Por qué utiliza **esperar** en las condiciones de estos dos códigos? En el de prioridad no podría simplemente usar *empty(c)*? [[3-Resources/Zettelkasten/Resume/Repaso Módulo 1 - Concurrencia y Paralelismo#N Procesos 1 Recurso (Orden de llegada y monitor Admin)\|N Proceso 1 Recurso Orden de llegada y Admin]], [[3-Resources/Zettelkasten/Resume/Repaso Módulo 1 - Concurrencia y Paralelismo#N Procesos 1 Recurso (Orden de prioridad y monitor Admin)\| N proceso 1 Recurso Orden de prioridad]]

- Hay diferencia en hacer uno u el otro?
```c
 while (unidad[grupo] < P) { 
	P(mutexG[grupo]);
	if ( unidad[grupo] < P){
		unidad[grupo]++;
		V(mutexG[grupo]);
		Hace unidad; 
	}else {
		V(mutexG[grupo]);
		sigo[grupo]=false;
	}				
}
```

```c
P(mutex_P[mi_grupo]); 
while (unidades[mi_grupo] < P) { 
	unidades[mi_grupo]++;
	V(mutex_P[mi_grupo]); 
	// hacer unidad 
	P(mutex_P[mi_grupo]); 
	} 
V(mutex_P[mi_grupo]);
```

- En este no entiendo por que debe ser atómico el actualizar el próximo, si supuestamente están todos los procesos en la línea antes de la sección crítica. Es decir nadie debería poder actualizar el próximo excepto el que está usando el recurso.
- Por qué no puede ser la variable turno una variable local en vez de una compartida?

<div class="transclusion internal-embed is-loaded"><a class="markdown-embed-link" href="/3-resources/zettelkasten/resume/repaso-modulo-1-concurrencia-y-paralelismo/#ticket" aria-label="Open link"><svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="svg-icon lucide-link"><path d="M10 13a5 5 0 0 0 7.54.54l3-3a5 5 0 0 0-7.07-7.07l-1.72 1.71"></path><path d="M14 11a5 5 0 0 0-7.54-.54l-3 3a5 5 0 0 0 7.07 7.07l1.71-1.71"></path></svg></a><div class="markdown-embed">



## Ticket
Se reparten numeros y se espera el turno de cada proceso. Los procesos toman un numero mayor que el de cualquier otro que espera ser atendido; luego esperan hasta que todos los procesos con numero mas chico hayan sido atendidos.
```c
int numero = 1, proximo = 1, turno[1:n] = ( [n] 0 );

process SC [i:1..n] 
{ 
while (true) {   
	< turno[i]=numero; numero=numero+1; > //Cada uno se asigna su numero e incrementa
  < await (proximo == turno[i]); > //Espero que el proximo sea yo
	sección crítica;
	<proximo = proximo + 1; > //Que pase el siguiente
  sección no crítica; 
    } 
}  
```
Esto de abajo nose para que es
```c
// Sabiendo que FA(var,incr): <temp=var; var=var+incr; return(temp)>
//Una forma de implementar el algoritmo Ticket es la siguiente
int numero = 1, proximo = 1, turno[1:n] = ( [n] 0 );
process SC [i:1..n] 
{ 
	while (true) {   
		turno[i]=FA(numero,1);
    while(turno[i]<>proximo)skip;
		sección crítica;
		proximo = proximo + 1;
    sección no crítica; 
     } 
}
```


</div></div>


No me queda claro por que ejecutaria la tarea antes de hacer el chequeo, pero por ahi quiero asegurarme de que todos comiencen la tarea al mismo tiempo. Ademas una vez que cantidad = N despues se queda siempre esperando en el ultimo await, MEO.

<div class="transclusion internal-embed is-loaded"><a class="markdown-embed-link" href="/3-resources/zettelkasten/resume/repaso-modulo-1-concurrencia-y-paralelismo/#barrier-contador-compartido" aria-label="Open link"><svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="svg-icon lucide-link"><path d="M10 13a5 5 0 0 0 7.54.54l3-3a5 5 0 0 0-7.07-7.07l-1.72 1.71"></path><path d="M14 11a5 5 0 0 0-7.54-.54l-3 3a5 5 0 0 0 7.07 7.07l1.71-1.71"></path></svg></a><div class="markdown-embed">



## Barrier - Contador Compartido
N procesos necesitan encontrarse en una barrera:

- Cada proceso incrementa una variable Canitdad al llegar → Cuando (Cantidad == N) todos los procesos estan en la barrera y pueden pasar.
```c
int cantidad=0;
process Worker[i=1..N]
{
	while(true) { 
	código para implementar la tarea i;
  < cantidad = cantidad + 1; > //Puede implementarse con FA(cantidad,1);
  < await (cantidad == N); > // while (cantidad <> N) skip;
	}
}
```


</div></div>

# Variables Compartidas
## Tie-Breaker (2 Procesos)
Protocolo de SC que requiere scheduling sólo débilmente fair y no usa instrucciones especiales.

Usa:
- Una variable por cada proceso para indicar que el proceso comenzo a ejecutar su protocolo de entrada a la seccion critica
- Una variable para romper empates, la cual indica que proceso fue el ultimo en comenzar dicha entrada (Esta variable es compartida y por lo tanto debe accederse de manera protegida)
```c
bool in1 = false, in2 = false; 
int ultimo = 1;
process SC1 {
    while (true) { 
	    ultimo = 1; in1 = true; 
			<await (not in2 or ultimo==2);> //--> Esto podria implementarse con while (in2 and ultimo == 1) skip;
		  sección crítica;
		  in1 = false; 
		  sección no crítica;
	}
}
process SC2 {
    while (true) { 
	    ultimo = 2; in2 = true; 
			<await (not in1 or ultimo==1);>
		  sección crítica;
		  in2 = false; 
		  sección no crítica;
	}
}

```

## Ticket
Se reparten numeros y se espera el turno de cada proceso. Los procesos toman un numero mayor que el de cualquier otro que espera ser atendido; luego esperan hasta que todos los procesos con numero mas chico hayan sido atendidos.
```c
int numero = 1, proximo = 1, turno[1:n] = ( [n] 0 );

process SC [i:1..n] 
{ 
while (true) {   
	< turno[i]=numero; numero=numero+1; > //Cada uno se asigna su numero e incrementa
  < await (proximo == turno[i]); > //Espero que el proximo sea yo
	sección crítica;
	<proximo = proximo + 1; > //Que pase el siguiente
  sección no crítica; 
    } 
}  
```
Esto de abajo nose para que es
```c
// Sabiendo que FA(var,incr): <temp=var; var=var+incr; return(temp)>
//Una forma de implementar el algoritmo Ticket es la siguiente
int numero = 1, proximo = 1, turno[1:n] = ( [n] 0 );
process SC [i:1..n] 
{ 
	while (true) {   
		turno[i]=FA(numero,1);
    while(turno[i]<>proximo)skip;
		sección crítica;
		proximo = proximo + 1;
    sección no crítica; 
     } 
}
```

## Barrier - Contador Compartido
N procesos necesitan encontrarse en una barrera:

- Cada proceso incrementa una variable Canitdad al llegar → Cuando (Cantidad == N) todos los procesos estan en la barrera y pueden pasar.
```c
int cantidad=0;
process Worker[i=1..N]
{
	while(true) { 
	código para implementar la tarea i;
  < cantidad = cantidad + 1; > //Puede implementarse con FA(cantidad,1);
  < await (cantidad == N); > // while (cantidad <> N) skip;
	}
}
```

## N procesos 1 Recurso (Orden de llegada + Prioridad)
Un cajero automático debe ser usado por N personas de a uno a la vez y según el orden de llegada al mismo. En caso de que llegue una persona anciana, la deben dejar ubicarse al principio de la cola.
```c
colaEspecial C;
int Siguiente = -1;

Process Persona [id:0..N-1]
{ 
	int edad=….;
	<if (Siguiente=-1)Siguiente=id 
	else Agregar(C,edad, id)>;
	<await(Siguiente==id)>;
	//Usaelcajero
	<if (empty(C)) Siguiente=-1
else Siguiente=Sacar(C)>;
}
//Agregar se encarga de poner primero a los ancianos

```
# Semáforos


## N procesos agrupados de a M
Primea sección crítica: Cola ordenada *"Sigo yo o me encolo?"*
**COMIENZA PASSING THE BATON**
```c
	P(mutex); //Mutex para la cola ordenada
		if(libre) {libre=false; V(mutex); }// Si 
		else { push(C,id);V(mutex); P(esperando[id]);
```
Asignar grupo: *"Soy del grupo actual, o está lleno?"*
```c
		if (cantidad[grupoGral] == 3)
			grupoGral++;//Si el grupo actual está lleno, soy del grupo sig.
		cantidad[grupoGral]++;//Hay lugar en el grupo actual
		grupo=grupoGral;//Me guardo el grupo al que pertenezco
```
Segunda sección crítica: Siguiente proceso: *"Cola vacía o hay proceso esperando?"*
**TERMINA PASSING THE BATON**
```c
		P(mutex);
		if(C.isEmpty())
			libre=true;
		else { idAux=pop(C); V(esperando[idAux]); }
		V(mutex);
```
Tercera sección crítica: Realizar tarea: *"Mi grupo llegó a las P unidades?"*
```c
while (sigo[grupo]) { 
			P(mutex[grupo]);
			if ( unidad[grupo] < P){
				unidad[grupo]++;
				V(mutex[grupo]);
				Hace unidad; }
			else {
			  V(mutex[grupo]);
				sigo[grupo]=false;
				}
				
		}
```

```c
int grupoGral =1; //Núm grupo actual
int cantidad [5] =([5] 0); // Cant empleados en grupo actual
int unidad[5] = ([5] 0);  // Cant unidades de grupo
bool sigo[5]=([5] true);  // Arreglo de bool para cada grupo terminar

sem mutex=1   // Passing the Baton
Cola C;       // Cola ordenada para passing the baton
sem esperando[15] =([15] 0); //Despierta a cada proceso ordenado
bool libre=1; // No hay nadie en la cola
const P;
sem mutexG[5]=([5] 1);  //Acceder a la cantidad unidades del grupo


process Empleado [id:1..15] {
		int grupo; 
		
		P(mutex); //Mutex para la cola ordenada
		if(libre) {libre=false; V(mutex); }// Si 
		else { push(C,id);V(mutex); P(esperando[id]);
		
		if (cantidad[grupoGral] == 3) grupoGral++; 
		cantidad[grupoGral]++;
		grupo=grupoGral;
		
		P(mutex);
		if(C.isEmpty())
			libre=true;
		else { idAux=pop(C); V(esperando[idAux]); }
		V(mutex);
		
		while (unidad[grupo] < P) { 
			P(mutexG[grupo]);
			if ( unidad[grupo] < P){
				unidad[grupo]++;
				V(mutexG[grupo]);
				Hace unidad; }
			else {
			  V(mutexG[grupo]);
				sigo[grupo]=false;
				}
				
		}
			
		

}
```

# Monitores
## N Procesos 1 Recurso (Orden de llegada y monitor Admin)
Necesito una variable libre y contador de gente que esta esperando para que no acceda al recurso una persona cuando el recurso esta libre pero ya hay gente esperando. La variable libre solo sera true cuando no hay nadie esperando.
```c
Process Proceso[id: 0..N-1] {
  Admin.Pasar();
  UsarRecurso();   // ← fuera del monitor
  Admin.Salir();
}

Monitor Admin {
	boolean libre=true;
	cond cola;
	int esperando=0;
	
	Procedure Pasar {
			if (not libre) { esperando++; wait(cola);}
			else libre=false;
	
	}
	
	Procedure Salir {
			if (esperando > 0) { esperando--; signal(cola);}
			else libre=true;
	}
	
}
```

## N Procesos 1 Recurso (Orden de prioridad y monitor Admin)

Ahora hay una variable de espera para cada proceso, de manera que se pueda respetar la prioridad y despertar al que corresponde.
```c
Process Proceso[id:1..N] {
		Admin.Pasar(id,prioridad);
		UsarRecurso();
		Admin.Salir();
	}
	
Monitor Admin {
		boolean libre =true;
		cond espera[N];
		int idAux, esperando=0;
		Cola cola;
		
		procedure Pasar(id,prioridad: in int) {
				if(not libre) {
						insertarOrdenado(cola,id,prioridad);
						esperando++;
						wait(espera[id]);
				} else libre=false;
		
		procedure Salir() {
			if(esperando > 0) {
				esperando--;
				idAux=pop(cola);
				signal(espera[idAux]); }
			else
				libre=true;
		
		}	
}
```

## Grupos 


```c
Process Alumno[id:1..50] {
		int numGrupo,nota;
		Admin.FormarFila();
		Admin.RecibirNumero(numGrupo);
		RealizaPractica();
		Admin.Termine(numGrupo,nota);
		
}

Process JTP {
		int nota=25, idG;
		Admin.EsperarAlumnos();
		for i:1..50 {
				num=DarNumero();
				Admin.Siguiente(num);
				}
		for i:1..25 {
				Admin.EsperarGrupo(idG);
				Admin.EntregarNota(idG,nota);
				nota--;
		}
				
				
}

Monitor Admin {
		int cantFila=0,N,idG;
		cond vcJTP, esperaFila,recibiNumero;
		int cantG [25]= ([25] 0), NotaG[25];

		procedure FormarFila {
				cantFila++;
				if(cantFila == 50) signal(vcJTP);
				wait(esperaFila);
		}
		
		procedure EsperarAlumnos {
				if (cantFila < 50) wait(vcJTP);
		}
		
		procedure Siguiente (num: in int) {
				signal(esperaFila);
				N=num;
				wait(recibiNumero);
		}
		
		procedure RecibirNumero(num: out int) {
				num=N;
				signal(recibiNumero);
		}
		
		procedure Termine(numG: in int; nota: out int) {
				cantG[numG]++;
				if(cantG[numG] == 2) {
				 push(C,numG);
				 signal(hayGrupo); 
				}
				wait(hayNota[numG]);
				nota=NotaG[numG];
		}
		
		procedure EsperarGrupo (idG: out int) {
				if(empty(C)) wait(hayGrupo);
				idG=pop(C);
			
		}

		procedure EntregarNota(idG: in int;nota: in int) {
				NotaG[idG]=nota;
				signalAll(hayNota[idG]);
	
		}


}
```