---
{"dg-publish":true,"permalink":"/3-resources/zettelkasten/resume/lazos-de-control/"}
---


> [!info] Definición
> Conjunto de elementos que miden una variable del [[3-Resources/Zettelkasten/Resume/Proceso en I&C\|proceso]] y la corrigen automáticamente.


```mermaid
graph TB
	A(Proceso) --"Temperatura de reactor"--> B(Sensor)
	B--"Medición de temperatura"--> C(Transmisor)
	C --"Se envía al controlador"--> D(Controlador)
	D --"Controlador decide si enfriar o calentar"--> E(Actuador)
	E --"Válvula se abre o cierra"--> F(Proceso)
```
