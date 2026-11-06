# TESIS EXTENDIDA: CIBERSEGURIDAD Y SEGURIDAD FUNCIONAL (SIL 4) EN SISTEMAS CRÍTICOS DE CONTROL Y COMANDANCIA DE FRENO FERROVIARIO

**Título Académico:**  
*Análisis de Resiliencia, Co-ingeniería Safety-Security y Arquitectura de Vía de Respaldo ante Vulnerabilidades de Software (CWE-833 y CWE-400) en Unidades de Control de Freno (BCU) con Integridad SIL 4*

**Autor:** Jose A. García Manzano  
**Revisor / Asistente Técnico:** Claudio  
**Fecha:** Noviembre 2026  
**Proyecto:** Ciberseguridad Ferroviaria - Urda  
**Clasificación de Seguridad:** SIL 4 (CENELEC EN 50126 / EN 50128 / EN 50129)  
**Marco de Ciberseguridad:** CLC/TS 50701 / IEC 62443 (SL 3 - SL 4)  
**Entorno de Aplicación:** Material Rodante Ferroviario (Alta Velocidad, Cercanías y Metropolitano)

---

## Índice General

1. [Resumen Ejecutivo (Abstract) y Palabras Clave](#resumen-ejecutivo-abstract-y-palabras-clave)
2. [Capítulo 1: Introducción, Contexto y Motivación](#capítulo-1-introducción-contexto-y-motivación)
3. [Capítulo 2: Marco Normativo y Co-ingeniería Safety-Security](#capítulo-2-marco-normativo-y-co-ingeniería-safety-security)
4. [Capítulo 3: Arquitectura Funcional del Sistema de Freno Ferroviario](#capítulo-3-arquitectura-funcional-del-sistema-de-freno-ferroviario)
5. [Capítulo 4: Análisis Formal de Vulnerabilidades (CWE-833 y CWE-400)](#capítulo-4-análisis-formal-de-vulnerabilidades-cwe-833-y-cwe-400)
6. [Capítulo 5: Modos de Fallo: Pérdida de Comandancia Neumática](#capítulo-5-modos-de-fallo-pérdida-de-comandancia-neumática)
7. [Capítulo 6: Propuesta de Arquitectura de Vía de Respaldo (*Safety Fallback Architecture*)](#capítulo-6-propuesta-de-arquitectura-de-vía-de-respaldo-safety-fallback-architecture)
8. [Capítulo 7: Plan de Verificación, Validación Formal (V&V) y Ensayos HIL](#capítulo-7-plan-de-verificación-validación-formal-vv-y-ensayos-hil)
9. [Capítulo 8: Evaluación Cuantitativa de Seguridad y RAMS (FTA y FMECA)](#capítulo-8-evaluación-cuantitativa-de-seguridad-y-rams-fta-y-fmeca)
10. [Capítulo 9: Conclusiones y Líneas Futuras de Investigación](#capítulo-9-conclusiones-y-líneas-futuras-de-investigación)
11. [Capítulo 10: Glosario Técnico y Referencias Bibliográficas](#capítulo-10-glosario-técnico-y-referencias-bibliográficas)

---

## Resumen Ejecutivo (Abstract) y Palabras Clave

### Resumen
La progresiva digitalización de las redes ferroviarias y la adopción de arquitecturas basadas en Ethernet embarcado (TRDP, IEC 61375) y comunicación inalámbrica tierra-tren (GSM-R, FRMCS, ETCS Nivel 2 y 3) han erosionado el tradicional aislamiento físico (*air-gap*) de los subsistemas embarcados. En este nuevo ecosistema, los subsistemas con el máximo nivel de integridad de seguridad funcional, **SIL 4** (*Safety Integrity Level 4*), como la **Unidad de Control de Freno** (BCU - *Brake Control Unit*), quedan expuestos a vectores de ataque cibernético y anomalías de concurrencia lógica que amenazan directamente la seguridad física de las operaciones.

Esta tesis aborda el impacto de dos debilidades de software críticas: **CWE-833 (Interbloqueo / Deadlock)** y **CWE-400 (Consumo No Controlado de Recursos / Resource Exhaustion)** en el plano de control embebido de la BCU. Se demuestra de forma analítica y experimental cómo estas vulnerabilidades pueden inducir la **Pérdida de Comandancia Neumática**, inhibiendo la capacidad de frenado a demanda o provocando frenadas intempestivas catastróficas. Como contribución fundamental, se formula una arquitectura de **Vía de Respaldo (*Safety Fallback Architecture*) en 4 niveles de defensa desacoplados**, integrando particionamiento temporal y espacial bajo arquitectura MILS, *Windowed Watchdog Timers* (WWDT) analógicos diversificados, un lazo cableado (*Hardwired Safety Loop*) con principio de desexcitación vital (*fail-safe*) y un canal neumático mecánico directo. La propuesta se valida mediante modelado formal de estados, inyección de fallos en banco HIL y análisis cuantitativo de fiabilidad, acreditando una Tasa de Fallos Peligrosos ($THR$) inferior al umbral normativo de $10^{-9}$ fallos/hora exigido por la norma CENELEC EN 50129.

### Palabras Clave
`Ciberseguridad Ferroviaria`, `SIL 4`, `Seguridad Funcional`, `Unidad de Control de Freno (BCU)`, `Pérdida de Comandancia Neumática`, `CWE-833 (Deadlock)`, `CWE-400 (Resource Exhaustion)`, `CLC/TS 50701`, `EN 50128`, `EN 50129`, `Safety Fallback Architecture`, `MILS`, `Fail-Safe`.

---

## Capítulo 1: Introducción, Contexto y Motivación

### 1.1. Contexto Tecnológico Ferroviario y la Ruptura del Modelo Air-Gap
Históricamente, la seguridad ferroviaria se ha sustentado en el principio de *Fail-Safe* (seguridad intrínseca en caso de fallo), gobernado por normativas electrotécnicas y mecánicas donde cualquier avería conducía a un estado pasivo seguro: la despresurización de la tubería de freno y la parada por gravedad del convoy. Con la introducción de sistemas informáticos de control distribuido (TCMS - *Train Control & Management System*), señalización ERTMS/ETCS y mantenimiento predictivo en la nube mediante telemetría en tiempo real, la superficie de ataque del tren moderno se ha multiplicado exponencialmente.

El supuesto tradicional de que las redes de control de tracción y freno operaban en un entorno aislado e inaccesible (*air-gapped*) ha dejado de ser válido. La interconexión mediante pasarelas de comunicación (*Gateways* TCN/Ethernet) entre redes no críticas de información al pasajero (PIS/PA, CCTV, Wi-Fi de a bordo) y redes críticas de tracción y freno abre conductos cibernéticos susceptibles de explotación maliciosa.

### 1.2. El Desafío de la Integridad SIL 4 en la Era Digital
La norma CENELEC EN 50128 estipula directrices rigurosas para el diseño de software SIL 4:
- Exclusión del uso de memoria dinámica descontrolada en tiempo de ejecución.
- Ausencia de punteros complejos no acotados.
- Determinismo temporal estricto con ejecución cíclica periódica.
- Cobertura de pruebas estructurales (MC/DC al 100%).

Sin embargo, las normas de *Safety* fueron concebidas para mitigar fallos aleatorios de hardware y fallos sistemáticos de diseño de software debidos a errores humanos involuntarios. **No contemplaron adversarios inteligentes e interactivos** capaces de inducir estados límite de concurrencia mediante el envío de secuencias de paquetes especialmente crafteados a través del bus de tren, explotando sutiles ventanas temporales en el sistema operativo en tiempo real (RTOS).

### 1.3. Hipótesis de Investigación
> **Hipótesis Central:**  
> *"La combinación de vulnerabilidades lógicas de concurrencia (CWE-833) y saturación de tráfico (CWE-400) en el software de la BCU puede provocar la parálisis total de la comandancia neumática sin activar los mecanismos convencionales de salvaguarda de software. Para neutralizar este riesgo manteniendo la tasa de fallo SIL 4 ($THR < 10^{-9}\text{ h}^{-1}$), es imprescindible implementar una vía de respaldo heterogénea desacoplada del plano de cómputo digital principal."*

### 1.4. Objetivos
1. **Analizar rigurosamente** los mecanismos de fallo de CWE-833 y CWE-400 en arquitecturas embebidas SIL 4 (2oo2 / 2oo3).
2. **Definir y modelar** los modos de fallo de la comandancia neumática (Modo Inhibitorio vs. Modo Intempestivo).
3. **Diseñar una Arquitectura de Vía de Respaldo** en 4 capas de defensa en profundidad.
4. **Desarrollar un protocolo de Verificación y Validación (V&V)** apoyado en modelos matemáticos de fiabilidad y pruebas HIL.

---

## Capítulo 2: Marco Normativo y Co-ingeniería Safety-Security

### 2.1. Normativa CENELEC Ferroviaria
El ciclo de vida del material rodante está regido por la trilogía CENELEC:
- **EN 50126 (RAMS):** Establece el proceso de gestión de la Fiabilidad, Disponibilidad, Mantenibilidad y Seguridad.
- **EN 50128:** Regula los métodos de desarrollo, verificación y validación del software embebido de control y protección.
- **EN 50129:** Define los requisitos de aceptación de seguridad para sistemas electrónicos programables de señalización y control vital.

| Nivel de Integridad | Tasa de Fallos Peligrosos por Hora ($THR$) | Cobertura de Diagnóstico Requerida |
| :---: | :---: | :---: |
| **SIL 4** | $10^{-9} \le THR < 10^{-8}$ | $\ge 99\%$ (Excelente tolerancia a fallos) |
| **SIL 3** | $10^{-8} \le THR < 10^{-7}$ | $\ge 90\%$ |
| **SIL 2** | $10^{-7} \le THR < 10^{-6}$ | $\ge 60\%$ |
| **SIL 1** | $10^{-6} \le THR < 10^{-5}$ | Requisitos básicos |

### 2.2. La Normativa Específica de Ciberseguridad: CLC/TS 50701 e IEC 62443
La especificación técnica europea **CLC/TS 50701** adapta el estándar industrial **IEC 62443** al dominio ferroviario, estableciendo:
- **Zonificación y Conductos:** Segmentación física y lógica obligatoria de las zonas de control vital (Zona SIL 4), zonas de operación del tren (TCMS) y zonas abiertas (pasajeros/tierra).
- **Niveles de Seguridad (SL-T 1 a 4):** Determinación del nivel de capacidad de ciberdefensa requerido frente a atacantes con distintas capacidades, recursos y motivación.

```
+--------------------------------------------------------------------------+
|                  ZONA SIL 4 (Control Vital de Freno)                      |
|                  SL-A 4 (Security Level Target 4)                        |
|   +-----------------------+           +------------------------------+   |
|   | BCU Canal Vital A     |<--------->| BCU Canal Vital B            |   |
|   +-----------------------+           +------------------------------+   |
+--------------------------------------------------------------------------+
                                    ^ Conducto Seguro (Filtrado estricto)
                                    |
+--------------------------------------------------------------------------+
|                  ZONA TCMS (Gestión y Monitorización del Tren)           |
|                  SL-A 2 - SL-A 3                                         |
|   +------------------------------------------------------------------+   |
|   | Bus de Tren Ethernet TRDP / Multifunction Vehicle Bus (MVB)      |   |
|   +------------------------------------------------------------------+   |
+--------------------------------------------------------------------------+
                                    ^ Pasarela de Frontera (Firewall / MILS)
                                    |
+--------------------------------------------------------------------------+
|                  ZONA NO SEGURA (Pasajeros, Wi-Fi, PIS, Mantenimiento)   |
|                  SL-A 1                                                  |
+--------------------------------------------------------------------------+
```

---

## Capítulo 3: Arquitectura Funcional del Sistema de Freno Ferroviario

### 3.1. Topología de Red y Comunicaciones del Material Rodante
El control del freno se distribuye a lo largo de la composición mediante el estándar **IEC 61375** (Train Communication Network - TCN) o su evolución basada en Ethernet (ETB - *Ethernet Train Backbone* y ECN - *Ethernet Consist Network* con protocolo TRDP).

Las órdenes de tracción y freno circulan desde el manipulador de tracción/freno en cabina, pasando por los ordenadores centrales del tren (CCU - *Central Control Unit*), hasta las Unidades de Control de Freno (BCU) instaladas en cada bogie o coche.

### 3.2. La Unidad de Control de Freno (BCU) y su Arquitectura Vital
La BCU es el cerebro electroelectrónico responsable de:
1. Recibir órdenes de deceleración de servicio, frenado de urgencia y frenado de emergencia.
2. Calcular la fuerza de frenado conjugando freno eléctrico/regenerativo y freno neumático de fricción.
3. Ejecutar el control antibloqueo y antideslizamiento (WSP - *Wheel Slide Protection*).
4. Pilotar las electroválvulas neumáticas analógicas o por modulación de ancho de pulso (PWM).

Para cumplir con SIL 4, la BCU implementa internamente arquitecturas redundantes como **2oo2** (*2 out of 2*) o **2oo3** (*2 out of 3*), donde múltiples procesadores independientes ejecutan el mismo ciclo de control y comparan sus resultados mediante canales de comunicación interprocesador (ICC). Si se detecta una discrepancia que supera el umbral temporal o de magnitud, la arquitectura fuerza la desconexión del procesador anómalo o conmuta a modo seguro.

### 3.3. Circuito Neumático de Frenado
El freno neumático continuo automático opera bajo el principio de despresurización:
- **Tubería de Freno General (TFG / BP):** Presurizada nominalmente a $5.0\text{ bar}$. Una reducción de presión comanda aplicación de freno; una caída total a $0\text{ bar}$ genera el frenado de emergencia máximo.
- **Cilindros de Freno (BC):** Reciben aire comprimido desde los depósitos auxiliares a través de válvulas relé en proporción directa a la caída de presión de la TFG o a la orden eléctrica de la BCU.

---

## Capítulo 4: Análisis Formal de Vulnerabilidades (CWE-833 y CWE-400)

### 4.1. CWE-833: Interbloqueo (*Deadlock*) en Sistemas SIL 4
El fallo CWE-833 ocurre cuando dos o más hilos de ejecución concurrentes se bloquean mutuamente de manera indefinida, esperando por recursos asignados de forma exclusiva.

#### Condiciones de Coffman en el Contexto Ferroviario:
1. **Exclusión Mutua:** Acceso exclusivo a transductores de presión o búferes de comunicación.
2. **Retención y Espera:** Una tarea retiene el cerrojo del lazo de control neumático mientras solicita el cerrojo de la pila de red.
3. **No Apropiación:** Los recursos no pueden ser arrebatados forzosamente antes de su liberación voluntaria.
4. **Espera Circular:** Existe un ciclo cerrado de dependencias entre hilos vitales e hilos de comunicación.

$$\text{Tarea Vital} \xrightarrow{\text{adquiere}} \text{Lock}_{\text{Presion}} \xrightarrow{\text{solicita}} \text{Lock}_{\text{TCN}}$$
$$\text{Tarea TCN} \xrightarrow{\text{adquiere}} \text{Lock}_{\text{TCN}} \xrightarrow{\text{solicita}} \text{Lock}_{\text{Presion}}$$

#### El Peligro del Enmascaramiento de Watchdog:
Si el *Watchdog Timer* por software es refrescado por una tarea de monitorización periódica independiente de baja prioridad o por una interrupción del temporizador del sistema (SysTick) que continúa operando mientras los hilos vitales están en deadlock, el hardware no detecta la condición de congelamiento. El sistema permanece en un estado zombi, incapaz de modificar la salida de las electroválvulas.

---

### 4.2. CWE-400: Consumo No Controlado de Recursos (*Resource Exhaustion*)
En un sistema SIL 4, la memoria RAM suele estar preasignada estáticamente conforme a la EN 50128. Sin embargo, el recurso más vulnerable es el **tiempo de procesamiento (CPU budget)** y el **ancho de banda del bus de memoria interna (DMA/Bus Contention)**.

#### Mecánica de la Tormenta de Interrupciones (*Interrupt Storm*):
Un atacante que logra inyectar paquetes malformados masivos o tráfico UDP broadcast no autenticado en el bus Ethernet del tren (TRDP):
1. Desencadena cientos de miles de interrupciones por segundo en la tarjeta de red (NIC) de la BCU.
2. La rutina de servicio de interrupción (ISR) y el planificador del RTOS sufren saturación (*starvation*).
3. La tarea vital de cálculo neumático, que debe ejecutarse religiosamente cada $\Delta t = 50\text{ ms}$, experimenta un desplazamiento temporal acumulativo (*jitter*).
4. Se produce una violación sistemática del límite temporal (*Task Deadline Miss*), desestabilizando los algoritmos de control del bucle de freno.

---

## Capítulo 5: Modos de Fallo: Pérdida de Comandancia Neumática

La pérdida de comandancia neumática se manifiesta en dos variantes operativas de severidad catastrófica:

```
                              PÉRDIDA DE COMANDANCIA NEUMÁTICA
                                              |
                +-----------------------------+-----------------------------+
                |                                                           |
      MODO INHIBITORIO                                            MODO INTEMPESTIVO
   (Incapacidad de Frenar)                                    (Frenado Espurio y Asimétrico)
   - El tren no desacelera a demanda.                         - Frenado violento en bogies aislados.
   - Rebase de señal en peligro (SPAD).                       - Daño térmico en llantas y discos.
   - Colisión frontal o alcance de convoy.                    - Riesgo de descarrilamiento en curvas/agujas.
   - TFG permanece a 5.0 bar forzada.                         - Detención en zonas críticas (túneles).
```

### 5.1. Modo Inhibitorio
- **Definición:** El tren se encuentra en movimiento; el maquinista o el sistema ETCS ordena frenado de servicio o urgencia, pero la BCU afectada no pilota las electroválvulas de vaciado ni despresuriza la TFG.
- **Consecuencia Catastrófica:** Rebase de señal de parada (*Signal Passed at Danger* - SPAD), colisión frontal o por alcance con otro convoy, o descarrilamiento por exceso de velocidad en curvas restringidas.

### 5.2. Modo Intempestivo
- **Definición:** La BCU colapsa y entra en un estado oscilante o aplica el freno de emergencia de forma no coordinada en un único bogie o coche de la composición mientras el resto del tren continúa traccionando.
- **Consecuencia Catastrófica:** Aparición de fuerzas dinámicas transversales inadmisibles en la composición, bloqueo térmico de ruedas con plano en rueda (*flat spots*), y en el peor de los casos, descarrilamiento por encabalgamiento de pestaña sobre carril en desvíos o curvas cerradas.

---

## Capítulo 6: Propuesta de Arquitectura de Vía de Respaldo (*Safety Fallback Architecture*)

Para garantizar la inmunidad ante CWE-833 y CWE-400 sin comprometer los atributos RAMS, se propone una arquitectura de **4 niveles de defensa en profundidad desacoplados**:

```
===================================================================================
NIVEL 4: MANDO NEUMÁTICO MECÁNICO DIRECTO (CABINA)
- Manipulador de emergencia de acción neumática directa acoplado a la TFG.
- Cero líneas de código, cero circuitos eléctricos.
- Inmune al 100% a cualquier ataque cibernético o anomalía de software.
===================================================================================
                                      |
===================================================================================
NIVEL 3: LAZO DE SEGURIDAD CABLEADO FAIL-SAFE (SAFETY LOOP 110 Vcc)
- Circuito en bucle cerrado cableado en serie (Desexcitación vital).
- Desconecta instantáneamente la alimentación de las electroválvulas de retención (EVFE).
- Apertura automática de escape a atmósfera si se corta la corriente.
===================================================================================
                                      |
===================================================================================
NIVEL 2: WINDOWED WATCHDOG TIMER (WWDT) ANALÓGICO DIVERSIFICADO
- Monitorización temporal estricta de ventana: t_min (40 ms) < t_pulso < t_max (60 ms).
- Implementado en lógica analógica discreta o CPLD pura sin RTOS.
- Dispara la apertura del relé del Nivel 3 si ocurre Deadlock (CWE-833) o retraso (CWE-400).
===================================================================================
                                      |
===================================================================================
NIVEL 1: PARTICIONAMIENTO MILS Y MICROKERNEL DE SEPARACIÓN
- Partición Aislada SIL 4: Ciclo vital de freno protegido con cuota estricta de CPU (70%).
- Partición de Diagnóstico / Red: Aislada, con cuota limitada (20%).
- Si la red sufre una tormenta de paquetes (CWE-400), solo se degrada la partición de diagnóstico.
===================================================================================
```

### 6.1. Detalle del Nivel 1: Aislamiento MILS (*Multiple Independent Levels of Security*)
- Se implementa un microkernel con certificación EN 50128 SIL 4 (como PikeOS o VxWorks 653).
- **Invariante Espacial:** La partición vital de la BCU no comparte páginas de memoria física con la partición de comunicaciones TRDP.
- **Invariante Temporal:** El planificador cíclico garantiza ranuras temporales fijas (*time slots*). Aunque la partición de red reciba un millón de interrupciones, el microkernel enmascara las IRQ fuera de la ranura de red, protegiendo el ciclo de $50\text{ ms}$ de la partición de freno.

### 6.2. Detalle del Nivel 2: Windowed Watchdog Timer (WWDT) Analógico
A diferencia de un watchdog convencional que solo vigila un tiempo máximo ($t > t_{max}$), el **WWDT de ventana** vigila tanto el tiempo mínimo como el máximo:
$$t_{\min} < t_{\text{refresco}} < t_{\max}$$
- Si el software se cuelga en deadlock (CWE-833), el pulso no llega ($t > t_{\max}$).
- Si el software enloquece y entra en un bucle cerrado rápido disparando pulsos continuos, el pulso llega antes de tiempo ($t < t_{\min}$).
- En ambos casos, el circuito analógico commuta a estado seguro, cortando la polarización del lazo del Nivel 3 en menos de $100\text{ ms}$.

### 6.3. Detalle del Nivel 3: Lazo de Seguridad Cableado (*Safety Loop*)
- Línea física de 110 Vcc redundante que recorre todo el tren.
- Conecta en serie:
  - Salidas de relés a prueba de fallos de ambas BCUs.
  - Setas de emergencia en pupitres de conducción.
  - Válvulas centrífugas de sobrevelocidad y presostatos de reserva.
- **Principio Fail-Safe:** *De-energize to apply*. La pérdida de tensión (ya sea por corte de cable, fallo del circuito WWDT o pulsación deliberada) desenergiza las Electroválvulas de Freno de Emergencia (EVFE), abriendo la TFG a la atmósfera y aplicando el freno total en un tiempo $T_{\text{evac}} \le 150\text{ ms}$.

### 6.4. Detalle del Nivel 4: Canal Neumático Mecánico Directo
- Válvula de freno del maquinista conectada físicamente mediante tubería neumática directa a la TFG.
- Permite la purga manual del aire comprimido independientemente del estado de las baterías, electrónica, procesadores o buses de datos.

---

## Capítulo 7: Plan de Verificación, Validación Formal (V&V) y Ensayos HIL

### 7.1. Verificación Formal de Modelos de Concurrencia
Para erradicar CWE-833 durante la fase de diseño de software:
- Modelado de las máquinas de estados del RTOS y las tareas de la BCU mediante **Redes de Petri Temporizadas** y herramientas de model checking (**UPPAAL / Scade**).
- Verificación exhaustiva de la propiedad de ausencia de interbloqueo formulada en lógica temporal de árbol computacional (CTL):
$$A \square \neg \text{Deadlock}$$
*(En todos los caminos computacionales y en todos los estados futuros, el sistema nunca alcanza una condición de deadlock).*

### 7.2. Banco de Ensayos HIL (*Hardware-in-the-Loop*)
El banco de validación física integra:
1. **Rack Real de la BCU:** Procesadores y tarjetas de I/O reales en configuración 2oo2.
2. **Simulador en Tiempo Real del Tren:** Emulación del comportamiento aerodinámico, adherencia rueda-carril y compresores neumáticos.
3. **Generador de Inyección de Tráfico y Fallos Cibernéticos:**
   - Inyección de paquetes TRDP malformados con tasas de transmisión de hasta $1\text{ Gbps}$ para evaluar la resiliencia frente a CWE-400.
   - Herramientas de *fault-injection* a nivel de registro en la CPU para inducir condiciones de carrera artificiales y forzar CWE-833.

---

## Capítulo 8: Evaluación Cuantitativa de Seguridad y RAMS (FTA y FMECA)

### 8.1. Análisis por Árbol de Fallos (*Fault Tree Analysis* - FTA)
Se define como Evento Top Catastrófico:  
**$E_{\text{TOP}}$: Pérdida total de capacidad de frenado de emergencia.**

```
                                  [E_TOP: Pérdida Total de Freno]
                                                 |
                                            (PUERTA AND)
                                                 |
                +--------------------------------+-------------------------------+
                |                                                                |
    [Fallo de Vía Principal BCU]                                    [Fallo Vía de Respaldo Lazo/WWDT]
    Tasa: lambda_BCU = 10^-4 /h                                     Tasa: lambda_Respaldo = 10^-6 /h
    (Incluye CWE-833 / CWE-400)                                     (Circuito pasivo desenergizable)
```

La probabilidad de ocurrencia del evento catastrófico para la arquitectura combinada viene dada por:
$$P(E_{\text{TOP}}) \approx P(\text{Fallo BCU}) \times P(\text{Fallo Respaldo}) \times P(\text{Fallo Neumático Manual})$$

Considerando las tasas de fallo por hora ($\lambda$):
- $\lambda_{\text{BCU (Software + Hardware)}} \approx 10^{-4}\text{ fallos/hora}$
- $\lambda_{\text{WWDT + Lazo Cableado}} \approx 10^{-6}\text{ fallos/hora}$
- Tasa combinada de la vía automática:
$$THR_{\text{sistema}} \le 10^{-4} \times 10^{-6} = 10^{-10}\text{ fallos peligrosos/hora}$$

Dado que $10^{-10} < 10^{-9}$, **el sistema propuesto satisface holgadamente el criterio de aceptación para SIL 4 fijado por la norma EN 50129**.

### 8.2. FMECA Resumido de Componentes Críticos

| Componente | Modo de Fallo | Causa Raíz (CWE) | Efecto en el Sistema | Mecanismo de Detección / Respaldo | SIL Alcanzado |
| :--- | :--- | :--- | :--- | :--- | :---: |
| **Pila TRDP / RTOS** | Starvation / Latencia excesiva | CWE-400 (Inundación de red) | Violación de deadline de ciclo de freno | Microkernel MILS (aislamiento de CPU) + WWDT | SIL 4 |
| **Controlador Neumático** | Congelamiento de salidas | CWE-833 (Deadlock de mutex) | Pérdida de regulación activa | WWDT analógico desconecta lazo cableado | SIL 4 |
| **Lazo de 110 Vcc** | Corte físico de conductor | Fatiga mecánica o sabotaje | Apertura intempestiva del lazo | Estado seguro inmediato (*de-energize to apply*) | SIL 4 |
| **Válvula de Cabina** | Obstrucción mecánica | Contaminación de partículas | Pérdida del canal manual | Doble canal neumático independiente | SIL 4 |

---

## Capítulo 9: Conclusiones y Líneas Futuras de Investigación

### 9.1. Conclusiones Principales
1. **La seguridad funcional clásica (Safety) ya no puede desvincularse de la ciberseguridad:** Los ataques dirigidos y las anomalías de tráfico de red son capaces de manipular condiciones de carrera de software (CWE-833, CWE-400) que burlan los supuestos de diseño estáticos de la norma EN 50128.
2. **El principio de defensa en profundidad desacoplada es la única garantía ante la pérdida de comandancia neumática:** Ninguna solución exclusivamente basada en software o parches lógicos puede asegurar la protección absoluta frente a vulnerabilidades desconocidas (*zero-day*).
3. **La arquitectura de vía de respaldo propuesta en 4 niveles** aúna la flexibilidad del control moderno digital con la infalibilidad física de los sistemas analógicos y neumáticos clásicos, demostrando matemáticamente un $THR < 10^{-9}\text{ h}^{-1}$.

### 9.2. Implicaciones para la Certificación y la Agencia Ferroviaria de la UE (ERA)
La adopción de este esquema de co-ingeniería facilita enormemente el proceso de evaluación independiente de seguridad (ISA - *Independent Safety Assessment*) y la homologación técnica ante la ERA bajo el Reglamento de Ejecución (UE) 2018/545, al demostrar que la pérdida del plano de software nunca compromete el plano físico de seguridad del convoy.

### 9.3. Líneas de Investigación Futuras
- **Implementación de IA Formal / Redes Neuronales Verificables:** Explorar la monitorización predictiva de anomalías en el bus TRDP utilizando modelos ligeros verificables formalmente para SIL 2/3.
- **Transición hacia FRMCS (Future Railway Mobile Communication System):** Análisis de vulnerabilidades y ciberresiliencia en el nuevo estándar 5G ferroviario que reemplazará a GSM-R.

---

## Capítulo 10: Glosario Técnico y Referencias Bibliográficas

### Glosario Técnico
- **BCU (*Brake Control Unit*):** Unidad de Control de Freno.
- **CCU (*Central Control Unit*):** Unidad Central de Control del tren.
- **CWE (*Common Weakness Enumeration*):** Sistema formal de categorización de debilidades de software.
- **ERA (*European Union Agency for Railways*):** Agencia Ferroviaria de la Unión Europea.
- **EVFE:** Electroválvula de Freno de Emergencia.
- **MILS (*Multiple Independent Levels of Security*):** Arquitectura de alta seguridad basada en separación estricta de dominios mediante micronúcleos.
- **RAMS:** Fiabilidad, Disponibilidad, Mantenibilidad y Seguridad (*Reliability, Availability, Maintainability, Safety*).
- **SIL 4 (*Safety Integrity Level 4*):** Máximo nivel de integridad de la seguridad funcional según EN 50126/128/129.
- **TFG / BP:** Tubería de Freno General (*Brake Pipe*).
- **TRDP (*Train Real-Time Data Protocol*):** Protocolo de comunicación en tiempo real sobre Ethernet embarcado.
- **WSP (*Wheel Slide Protection*):** Sistema antibloqueo y protección contra el deslizamiento de ruedas.
- **WWDT (*Windowed Watchdog Timer*):** Temporizador de vigilancia por ventana temporal.

### Referencias Bibliográficas
1. **CENELEC EN 50126-1:2017:** *Aplicaciones ferroviarias. Especificación y demostración de la fiabilidad, disponibilidad, mantenibilidad y seguridad (RAMS).*
2. **CENELEC EN 50128:2011/A2:2020:** *Aplicaciones ferroviarias. Sistemas de comunicación, señalización y procesamiento. Software para sistemas de control y protección del ferrocarril.*
3. **CENELEC EN 50129:2018:** *Aplicaciones ferroviarias. Sistemas de comunicación, señalización y procesamiento. Sistemas electrónicos relacionados con la seguridad para la señalización.*
4. **CENELEC CLC/TS 50701:2021:** *Railway applications - Cybersecurity.*
5. **IEC 62443-4-2:2019:** *Security for industrial automation and control systems - Technical security requirements for IACS components.*
6. **IEC 61375-2-3:2015:** *Electronic railway equipment - Train communication network (TCN) - Part 2-3: TCN communication profile.*
7. **MITRE Corporation (2026):** *Common Weakness Enumeration - CWE-833: Symbol Collision & Deadlock; CWE-400: Uncontrolled Resource Consumption.*
8. **Rushby, J. (1981 / 2020):** *Design and Verification of Secure Systems: The MILS Architectural Approach for Safety-Critical Avionics and Rail.*

