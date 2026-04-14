---
{"dg-publish":true,"permalink":"/3-resources/zettelkasten/resume/i-and-c-sensores-de-iluminacion/","created":"2026-03-20T18:59:44.053-03:00","updated":"2026-03-28T15:00:51.367-03:00"}
---

# Fotoresistencias (LDR)

## Principio de funcionamiento

> [!info] LDR - Light Dependent Resistor Un LDR **no mide intensidad lumínica directamente**. Mide cuántos fotones tienen energía suficiente para excitar electrones. La condición clave es: $$E_{\text{fotón}} \geq E_g$$

---

## Estructura de bandas de energía en semiconductores

Para entender cómo funciona una fotoresistencia, primero hay que entender la física de los semiconductores. En un semiconductor, los electrones **no pueden tener cualquier energía**: existen regiones permitidas y regiones prohibidas.

Hay tres regiones clave:

1. **Banda de valencia** → electrones ligados al átomo (no conducen)
2. **Banda prohibida** ($E_g$) → rango de energías que los electrones **no pueden tener**
3. **Banda de conducción** → electrones libres → permiten conducción eléctrica


> [!info] Banda Prohibida (Band Gap) 
> $$E_g$$
> ---
> Es la energía mínima que hay que entregarle a un electrón para que salte de: $$\text{Banda de valencia} \rightarrow \text{Banda de conducción}$$ Mientras más grande es $E_g$, más energético debe ser el fotón para generar conducción.

---

## La luz como portadora de energía

Un fotón transporta energía según su frecuencia:

$$E_{\text{fotón}} = hf = \frac{hc}{\lambda}$$

donde:

- $h$: constante de Planck
- $f$: frecuencia de la luz
- $c$: velocidad de la luz
- $\lambda$: longitud de onda

Esto implica que:

- **Alta frecuencia (UV)** → fotón muy energético
- **Baja frecuencia (IR)** → fotón poco energético

---

## Condición de fotoconductividad

> [!important] Condición para que baje la resistencia $$E_{\text{fotón}} \geq E_g$$
> 
> - Si $E_{\text{fotón}} < E_g$ → el fotón **no tiene energía suficiente** → no ocurre nada
> - Si $E_{\text{fotón}} \geq E_g$ → el electrón es excitado a la banda de conducción → **baja la resistencia**

Este fenómeno se llama **fotoconductividad**. Es el principio de operación de todos los LDR.

---

## Longitud de onda máxima efectiva

Cada material tiene un $E_g$ distinto, lo que determina qué colores o frecuencias de luz puede "ver". Existe una longitud de onda máxima $\lambda_{\max}$ por encima de la cual los fotones ya no tienen energía suficiente:

$$\lambda_{\max} = \frac{hc}{E_g}$$

Para $\lambda > \lambda_{\max}$, el LDR no responde.

---

## Materiales comunes y su rango espectral

|Material|$E_g$ (eV)|$\lambda_{\max}$ (µm)|Zona espectral|
|---|---|---|---|
|ZnS|3,60|0,345|UV|
|CdS|2,40|0,52|Verde (visible)|
|CdSe|1,80|0,69|Rojo (visible)|
|Si|1,12|1,10|IR cercano|
|Ge|0,67|1,85|IR|

Cada material "ve" un rango distinto del espectro electromagnético según su banda prohibida.

---

## Ejemplo: LDR comercial de CdS

El LDR más común en electrónica utiliza **sulfuro de cadmio (CdS)**:

$$E_g \approx 2{,}4 \ \text{eV} \qquad \Rightarrow \qquad \lambda_{\max} \approx 0{,}52 \ \mu\text{m}$$

Esto lo ubica en el verde del espectro visible. Consecuencias prácticas:

- Responde muy bien a la **luz ambiente** (visible)
- Casi no responde a la **luz infrarroja**

Por eso:

- Luz ambiente → baja $R$
- Oscuridad → alta $R$

---

## ¿Por qué el IR térmico no activa la mayoría de los LDR?

La radiación emitida por objetos calientes (personas, cuerpos a temperatura ambiente) está en:

$$\lambda \approx 8 - 14 \ \mu\text{m}$$

lo que implica una energía de fotón:

$$E_{\text{fotón}} \ll E_g \quad \text{(para CdS, Si, etc.)}$$

Por lo tanto:

- ❌ No hay excitación de electrones
- ❌ No baja la resistencia
- ❌ El LDR no detecta nada

> [!warning] PIR ≠ LDR Los sensores PIR (pasivos de infrarrojo) **no son LDR**. Usan un principio térmico distinto y materiales con $E_g$ muy pequeño, diseñados específicamente para el rango IR térmico.

---

## Resumen conceptual

```
Fotón incidente
      │
      ▼
  E_fotón ≥ E_g ?
      │
   ┌──┴──┐
  NO    SÍ
   │     │
   ▼     ▼
Sin   Electrón excitado
efecto  → Banda de conducción
          → Resistencia baja
```

Lo que define el rango de respuesta de un LDR no es su forma ni su tamaño, sino el **material semiconductor** y su **banda prohibida** $E_g$.

---
# Fotodiodo

> [!info] Caracteristicas
> - Generación de portadores (*corriente*) a partir de incidencia de luz
> - Es **autogenerativo** (no requiere fuente externa)
> - Genera corriente del orden de los nanoamperios $10^{-9}A$, por lo que requiere amplificación

 

---
## Ver también

- [[Ley de Hooke\|Ley de Hooke]]
- [[Galgas extensométricas\|Galgas extensométricas]]
- [[Puente de Wheatstone\|Puente de Wheatstone]]
- [[Semiconductores\|Semiconductores]]

