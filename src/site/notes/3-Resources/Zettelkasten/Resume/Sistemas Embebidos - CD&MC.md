---
{"dg-publish":true,"permalink":"/3-resources/zettelkasten/resume/sistemas-embebidos-cd-and-mc/","created":"2026-03-04T19:53:45.702-03:00","updated":"2026-03-17T17:27:07.896-03:00"}
---

# Sistemas Embebidos
Compuestos por **Hardware** y **Software**
## Hardware
- Microcontroladores AVR
- Puertos
- Interfaces de comunicación

## Software
- Lenguaje C
- Modularización, planificadores, manejador de dispositivos
- Maquinas de estado finito ([[MEF\|MEF]])
- Sistemas operativos en tiempo real para Sistemas Embebidos ([[RTOS\|RTOS]])

# Definición
*Equipos electrónicos que incluyen un procesador de datos diseñados para satisfacer una función específica*

- El cerebro de un sistema embebido es un microprocesador o microcontrolador
- Diseñado optimizado para reducir tamaño, consumo, costo y maximizar confiabilidad y desempeño

>SASE: Simposio Argentino de Sistemas Embebidos

## Componentes de un sistema embebido
### Hardware
- Microprocesador, Microcontrolador, DSP, FPGA, ASIC, SoC, etc.
- Memorias de almacenamiento volátil y no volátil
- Periféricos analógicos y digitales
- Componentes electrónicos activos (diodos, transistores) y pasivos (resistencias, capacitores, inductores)
- Interfaces eléctricas (Conectores)
- Placa de circuito impreso (PCB)

### Software
1. Capa de abstracción de hardware y manejadores de dispositivos (Drivers)
2. Capa de componentes intermedios como pila de protocolos 
3. Capa de planificación y ejecución de tareas en tiempo real ([[RTOS\|RTOS]])
4. Capa de la aplicación específica

---
# MPU o MCU

## MPU
*Unidad de procesamiento de propósito general*
- Capacidad de cómputo 16, 32 y 64 bits, FPU, reloj de GHz
- Múltiples núcleos, diferentes niveles de memoria Caché L1, L2.
- Poseen MMU para soporte a sistemas operativos
- Sin periféricos específicos integrados, o solo necesarios.
> Ej: Raspberry Pie

## MCU
*Sistema de procesamiento completo destinados a aplicaciones específicas*
- Capacidad de cómputo 8, 16, 32 bits, ALU de punto fijo, reloj <500MHz
- Periféricos integrados en el mismo chip
- Encapsulados entre 6 y 100 terminales
- Bajo consumo, bajo costo
> Ej: Arduino UNO