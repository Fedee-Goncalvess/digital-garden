---
{"dg-publish":true,"permalink":"/3-resources/zettelkasten/resume/cy-p-acciones-atomicas/","created":"2026-03-28T21:05:04.498-03:00","updated":"2026-03-28T21:14:21.413-03:00"}
---

Una **acción atómica** hace una transformación de estado indivisibles.

Existen atomicidades de *grano fino* o de *grano grueso*.

## Grano Fino
Divide el código en muchas secciones críticas pequeñas, cada una protegiendo solo lo estrictamente necesario.
- **Mayor cantidad de *locks***
- **Mayor paralelismo**
- **Se protegen operaciones muy puntuales**

## Grano Grueso
Protege *bloques grandes de código* con un solo ***lock***
- **Muchas operaciones bajo mismo *lock***
- **Reduce paralelismo**
- **Simplifica razonamiento**