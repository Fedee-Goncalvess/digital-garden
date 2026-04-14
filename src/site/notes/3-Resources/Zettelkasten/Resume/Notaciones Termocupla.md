---
{"dg-publish":true,"permalink":"/3-resources/zettelkasten/resume/notaciones-termocupla/","created":"2026-03-23T17:00:39.802-03:00","updated":"2026-03-23T17:01:02.044-03:00"}
---

# Termocupla – Resumen de conceptos clave

## 1. Qué mide una termocupla
- Una termocupla **no mide temperatura absoluta**.
- Mide una **diferencia de temperatura** entre dos uniones:
  - Unión caliente (punto de medición)
  - Unión fría (referencia)

## 2. Principio físico
- Funciona por el **efecto Seebeck**.
- Dos metales distintos generan una **fuerza electromotriz (fem)** cuando existe un gradiente térmico.
- El voltaje generado depende de:
  - Los materiales
  - La diferencia de temperatura entre las uniones

## 3. Relación voltaje – temperatura
- El voltaje es del orden de **microvoltios por grado**.
- Para una termocupla tipo K:
  - Sensibilidad aproximada: ~41 µV/°C
- El voltaje corresponde a:
  
  V ↔ (T_caliente − T_referencia)

## 4. Unión fría (temperatura de referencia)
- La referencia **no está en la punta caliente**.
- Está en el punto donde:
  - Los metales de la termocupla
  - Se conectan con cobre (instrumento)

## 5. Método antiguo (sin compensación)
- La unión fría se mantiene físicamente a **0 °C** (baño de hielo).
- El voltaje medido corresponde directamente a la temperatura de la unión caliente.
- Condición fundamental:
  - Todas las uniones metal–cobre deben estar a la **misma temperatura**.

## 6. Dónde se mide el voltaje
- El voltaje se mide **en los extremos de la termocupla**, no en la unión caliente.
- El multímetro se conecta entre los dos metales.
- La unión caliente es un solo nodo eléctrico → no se mide tensión ahí.

## 7. Compensación de unión fría (CJC)
- Los instrumentos modernos:
  - Miden la temperatura de la unión fría con un sensor interno
  - Calculan el voltaje equivalente
  - Lo suman al voltaje medido
- Así reconstruyen la **temperatura absoluta**.

## 8. Qué hace un multímetro con medición de temperatura
- Usa una termocupla (generalmente tipo K).
- Mide el voltaje generado.
- Aplica compensación de unión fría internamente.
- Convierte el voltaje a temperatura usando la curva del tipo de termocupla.
- El tipo de termocupla está **predefinido** (no se detecta automáticamente).

## 9. Errores típicos
- Olvidar que la termocupla mide ΔT, no T absoluta.
- No mantener las uniones de referencia a la misma temperatura.
- Usar una termocupla de tipo distinto al que espera el instrumento.
- Gradientes térmicos en los bornes del instrumento.

## 10. Frase clave
> La termocupla genera voltaje por diferencia de temperatura;  
> el instrumento se encarga de reconstruir la temperatura real.

