# Estudio Funcional y Propuesta de Vía de Respaldo: Vulnerabilidades SIL 4 (CWE-833, CWE-400) y Pérdida de Comandancia Neumática

**Proyecto de Tesis:** Ciberseguridad Ferroviaria  
**Autor:** Jose A. García Manzano  
**Revisor/Asistente:** Claudio  
**Fecha:** Noviembre 2026  
**Clasificación:** SIL 4 (CENELEC EN 50126 / EN 50128 / EN 50129 / CLC/TS 50701 / IEC 62443)

---

## 1. Introducción y Objeto del Estudio

El presente estudio funcional analiza el impacto de vulnerabilidades de software críticas en sistemas embebidos ferroviarios con nivel de integridad de la seguridad **SIL 4**, centrándose específicamente en la **Unidad de Control de Freno (BCU - *Brake Control Unit*)** y el subsistema de **Comandancia Neumática** del material rodante.

El objetivo principal es:
1. Evaluar formalmente los vectores de fallo y ataque representados por **CWE-833 (Deadlock / Interbloqueo)** y **CWE-400 (Uncontrolled Resource Consumption / Agotamiento No Controlado de Recursos)**.
2. Determinar las condiciones bajo las cuales estas anomalías provocan la **Pérdida de Comandancia Neumática**.
3. Diseñar y proponer una **Arquitectura de Vía de Respaldo (Safety Fallback Architecture)** independiente, diversificada y a prueba de fallos (*fail-safe*) que garantice la detención segura del tren incluso ante el colapso total del plano de control software.

---

## 2. Marco Normativo y Definiciones Operativas

| Norma | Ámbito de Aplicación | Relevancia en el Estudio |
| :--- | :--- | :--- |
| **EN 50126** | RAMS ferroviario (Fiabilidad, Disponibilidad, Mantenibilidad, Seguridad) | Definición de matrices de riesgo, tasas de fallo tolerables ($THR < 10^{-9}$ fallos peligrosos/hora para SIL 4). |
| **EN 50128** | Software para sistemas de control y protección ferroviaria | Técnicas de diseño preventivo para software SIL 4 (prohibición de punteros dinámicos sin acotar, determinismo temporal, análisis estático). |
| **EN 50129** | Sistemas electrónicos relacionados con la seguridad | Requisitos para arquitecturas de hardware tolerantes a fallos (2oo2, 2oo3). |
| **CLC/TS 50701 / IEC 62443** | Ciberseguridad ferroviaria | Zonificación, conductos de comunicación y análisis de amenazas que impacten en la seguridad funcional (*Safety-Security Co-engineering*). |

---

## 3. Análisis Funcional de las Vulnerabilidades

### 3.1. CWE-833: Interbloqueo (*Deadlock*) en Arquitecturas SIL 4

#### Mecanismo del Fallo
En los sistemas SIL 4 (comúnmente implementados sobre arquitecturas **2oo2** o **2oo3** ejecutando RTOS certificados como PikeOS, VxWorks 653 o Integrity-178), coexisten hilos de alta criticidad para:
- Lectura de transductores de presión de la Tubería de Freno General (TFG / BP) y cilindros de freno (BC).
- Algoritmo de cálculo de esfuerzo de frenado y antibloqueo (WSP - *Wheel Slide Protection*).
- Canales de sincronización inter-procesador (Inter-Channel Communication - ICC).
- Interfaz de bus de tren (WTB, MVB o Ethernet TRDP).

Un **CWE-833** surge por inversión o contención circular de bloqueos (mutex/semáforos) entre el ciclo de procesamiento vital y la rutina de intercambio de datos con el bus de comunicaciones:
$$\text{Hilo A (Control Vital)} \xrightarrow{\text{retiene}} \text{Mutex}_{presión} \xrightarrow{\text{espera}} \text{Mutex}_{bus}$$
$$\text{Hilo B (Comunicaciones TCN)} \xrightarrow{\text{retiene}} \text{Mutex}_{bus} \xrightarrow{\text{espera}} \text{Mutex}_{presión}$$

#### Consecuencia en la Comandancia Neumática
- **Congelamiento de estado:** Las electroválvulas proporcionales o de aplicación/afloje quedan fijadas en su último estado de excitación.
- **Enmascaramiento del fallo:** Si el mecanismo de *Watchdog* de software se alimenta de una tarea de prioridad superior no afectada por el deadlock, el sistema no disparará la transición al estado seguro de manera inmediata.

---

### 3.2. CWE-400: Consumo No Controlado de Recursos (*Resource Exhaustion*)

#### Mecanismo del Fallo / Vector Cibernético
Aunque la norma EN 50128 restringe estrictamente la gestión de memoria dinámica en SIL 4, los controladores de interfaz de red (NIC/MAC) y las pilas de protocolos (TRDP, CAN, CIP) manejan buffers circulares e interrupciones (ISR - *Interrupt Service Routines*).

Un ataque de denegación de servicio o malformación de tráfico (*Flooding / Malformed Packet Storm*):
1. Genera una **tormenta de interrupciones (Interrupt Storm)** en el procesador de comunicaciones.
2. Monopoliza el ancho de banda del bus de memoria interna (DMA/RAM starvation).
3. Provoca que la tarea periódica de ciclo cerrado de freno neumático ($\Delta t = 50\text{ ms} - 100\text{ ms}$) exceda su *deadline* temporal (*Jitter / Task Deadline Violation*).

---

## 4. Peligro Crítico: Pérdida de Comandancia Neumática

La **pérdida de comandancia neumática** se clasifica en dos modos de fallo de criticidad catastrófica:

1. **Modo Inhibitorio (Incapacidad de frenar a demanda):**
   - El maquinista o el sistema de protección automática (ETCS / ATP / EBICAB) comanda freno de servicio o urgencia, pero la orden no se traduce en la despresurización de la TFG o el pilotaje de las electroválvulas neumáticas debido al bloqueo de la BCU.
2. **Modo Intempestivo (Frenado espurio e incontrolado):**
   - Disparo descontrolado o asimétrico del freno de emergencia en bogies aislados, con riesgo de deformación térmica de discos, aplastamiento de ruedas (*wheel flats*) o detención en zonas de alto riesgo (túneles, puentes, tramos neutros sin catenaria).

---

## 5. Propuesta de Arquitectura de Vía de Respaldo (*Safety Fallback Architecture*)

Para mitigar CWE-833 y CWE-400 sin comprometer los requisitos RAMS, se propone una **solución en 4 capas de defensa desacopladas**:

```
+-------------------------------------------------------------------------+
|                  NIVEL 4: MANDO NEUMÁTICO MECÁNICO DIRECTO              |
|        Manipulador de freno de emergencia en cabina con escape directo   |
+-------------------------------------------------------------------------+
                                    |
+-------------------------------------------------------------------------+
|             NIVEL 3: LAZO DE SEGURIDAD CABLEADO (SAFETY LOOP)            |
|       Hardwired 110V DC De-energize to apply (Independiente de Software) |
+-------------------------------------------------------------------------+
                                    |
+-------------------------------------------------------------------------+
|          NIVEL 2: WINDOWED WATCHDOG TIMER ANALÓGICO DIVERSIFICADO        |
|    Detección estricta de ventana temporal (t_min < t < t_max) sin RTOS  |
+-------------------------------------------------------------------------+
                                    |
+-------------------------------------------------------------------------+
|         NIVEL 1: SEPARACIÓN Y AISLAMIENTO MILS (MICROKERNEL SEGURO)     |
|   Plano de Control SIL 4 aislado de interfaces de diagnóstico (CWE-400) |
+-------------------------------------------------------------------------+
```

### 5.1. Nivel 1: Aislamiento Físico y de Particiones MILS (Prevención CWE-400)
- **Particionamiento Temporal y Espacial:** Uso de un microkernel de separación certificado (ARINC 653 / IEC 61508 / EN 50128). La partición de red/diagnóstico dispone de cuotas estrictas de CPU y memoria garantizadas. Si se inunda de paquetes, solo colapsa dicha partición sin restar un solo ciclo a la partición de control neumático SIL 4.
- **Control de Flujo por Hardware:** Transceptores con aislamiento óptico y limitación física de tasa de tramas (*Hardware Rate Limiting*).

### 5.2. Nivel 2: Windowed Watchdog Timer (WWDT) Analógico (Detección CWE-833)
- Un circuito oscilador analógico o CPLD simple (libre de código ejecutable complejo) monitoriza el pulso vital generado *exclusivamente* al final de la secuencia completa del cálculo neumático.
- Si la secuencia se congela por deadlock (CWE-833) o se retrasa (CWE-400), el WWDT corta la corriente de alimentación del relé de retención neumática en menos de $150\text{ ms}$.

### 5.3. Nivel 3: Lazo de Seguridad Cableado (*Hardwired Safety Loop*)
- Línea física de 110 Vcc en bucle cerrado que conecta en serie:
  - Presostatos de seguridad.
  - Salidas de relés a prueba de fallos de la BCU y EVC.
  - Setas de emergencia de ambas cabinas.
- **Principio Fail-Safe:** Principio de "desexcitación para aplicar" (*de-energize to apply*). La ausencia o corte de corriente provoca la apertura instantánea de las electroválvulas de freno de emergencia (EVFE), evacuando la Tubería de Freno General a atmósfera directamente sin intervención de buses digitales.

### 5.4. Nivel 4: Canal Neumático Autónomo
- Válvula de freno directa con conexionado neumático directo a la TFG en cada pupitre de conducción, permitiendo al operador vaciar la tubería por acción puramente mecánica/neumática, anulando cualquier interferencia de naturaleza lógica o cibernética.

---

## 6. Plan de Verificación y Validación (V&V) para la Tesis

1. **Inyección de Fallos de Software:**
   - Pruebas dirigidas de inyección de inversión de prioridad y mutex contrapuestos para emular CWE-833 en banco HIL (*Hardware-in-the-Loop*).
   - Inyección de tráfico DoS masivo en la interfaz Ethernet/MVB para verificar la estanqueidad temporal frente a CWE-400.
2. **Medición de Tiempos de Respuesta:**
   - Medición de la latencia de desexcitación del lazo de emergencia: target $T_{response} \le 150\text{ ms}$.
   - Verificación del comportamiento de la curva de vaciado neumático (presión nominal $5.0\text{ bar} \to 0\text{ bar}$).
3. **Análisis de Modos de Fallo y Efectos (FMEA / FMECA) y Árbol de Fallos (FTA):**
   - Demostración cuantitativa de que la combinación de fallo de software + fallo de lazo cableado cumple la tasa $THR < 10^{-9}$ fallos peligrosos/hora requerida para SIL 4.
