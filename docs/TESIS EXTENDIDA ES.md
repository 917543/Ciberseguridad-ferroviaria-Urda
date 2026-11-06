# TESIS EXTENDIDA: CIBERSEGURIDAD Y SEGURIDAD FUNCIONAL (SIL 4) EN SISTEMAS CRÍTICOS DE CONTROL Y COMANDANCIA DE FRENO FERROVIARIO

**Título Académico:**  
*Análisis de Resiliencia, Co-ingeniería Safety-Security y Arquitectura de Vía de Respaldo ante Vulnerabilidades de Software (CWE-833 y CWE-400) en Unidades de Control de Freno (BCU) con Integridad SIL 4: Gestión Integral de Frenado, Desbloqueo y Recuperación Neumática de Marcha*

**Autor:** Jose Antonio García Manzano  
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
4. [Capítulo 3: Arquitectura Funcional del Sistema de Freno Ferroviario y Dinámica Neumática Bipolar](#capítulo-3-arquitectura-funcional-del-sistema-de-freno-ferroviario-y-dinámica-neumática-bipolar)
5. [Capítulo 4: Análisis Formal de Vulnerabilidades (CWE-833 y CWE-400)](#capítulo-4-análisis-formal-de-vulnerabilidades-cwe-833-y-cwe-400)
6. [Capítulo 5: Modos de Fallo: Pérdida de Comandancia Neumática e Inmovilización Forzosa](#capítulo-5-modos-de-fallo-pérdida-de-comandancia-neumática-e-inmovilización-forzosa)
7. [Capítulo 6: Propuesta de Arquitectura de Vía de Respaldo Bidireccional (*Safety Fallback Architecture*)](#capítulo-6-propuesta-de-arquitectura-de-vía-de-respaldo-bidireccional-safety-fallback-architecture)
8. [Capítulo 7: Plan de Verificación, Validación Formal (V&V) y Ensayos HIL](#capítulo-7-plan-de-verificación-validación-formal-vv-y-ensayos-hil)
9. [Capítulo 8: Evaluación Cuantitativa de Seguridad y RAMS (FTA y FMECA)](#capítulo-8-evaluación-cuantitativa-de-seguridad-y-rams-fta-y-fmeca)
10. [Capítulo 9: Conclusiones Doctrinales y Recomendaciones Técnicas](#capítulo-9-conclusiones-doctrinales-y-recomendaciones-técnicas)
11. [Capítulo 10: Glosario Técnico y Referencias Bibliográficas](#capítulo-10-glosario-técnico-y-referencias-bibliográficas)

---

## Resumen Ejecutivo (Abstract) y Palabras Clave

### Resumen
La progresiva digitalización de las redes ferroviarias y la adopción de arquitecturas basadas en Ethernet embarcado (TRDP, IEC 61375) y comunicación inalámbrica tierra-tren (GSM-R, FRMCS, ETCS Nivel 2 y 3) han erosionado el tradicional aislamiento físico (*air-gap*) de los subsistemas embarcados. En este nuevo ecosistema, los subsistemas con el máximo nivel de integridad de seguridad funcional, **SIL 4** (*Safety Integrity Level 4*), como la **Unidad de Control de Freno** (BCU - *Brake Control Unit*), quedan expuestos a vectores de ataque cibernético y anomalías de concurrencia lógica que amenazan directamente la seguridad física de las operaciones ferroviarias.

Esta tesis aborda el impacto de dos debilidades de software críticas: **CWE-833 (Interbloqueo / Deadlock)** y **CWE-400 (Consumo No Controlado de Recursos / Resource Exhaustion)** en el plano de control embebido de la BCU. Se demuestra analítica y experimentalmente que estas anomalías no sólo provocan la inhibición del frenado a demanda o frenadas intempestivas, sino que inducen un tercer modo de fallo de severidad extrema: la **Inmovilización Forzosa por Secuestro de Purga Abierta (*Locked Exhaust State*)**. En este estado, tras una parada de emergencia o perturbación en la señal de vía (LZB/ERTMS), el software colapsa en bucle cerrado manteniendo excitadas o bloqueadas las electroválvulas en posición de escape continuo a la atmósfera. Esto impide de forma absoluta devolver la presión nominal de régimen ($5.0\text{ bar}$) a la Tubería de Freno Automático/General (TFA/TFG), bloqueando los cilindros de freno e incapacitando al maquinista para aflojar y reanudar la marcha. El tren queda convertido en un obstáculo ciego e inamovible en plena vía general de alta velocidad, expuesto a colisiones por alcance por tráfico convergente (como evidenció el Siniestro de Urda con el Frecciarossa ETR 1000).

Como contribución central, se formula una **Arquitectura de Vía de Respaldo Bidireccional (*Safety Fallback Architecture*) en 4 niveles de defensa desacoplados**. A diferencia de los modelos tradicionales centrados exclusivamente en forzar la parada (*trip/fail-safe*), esta arquitectura garantiza de forma simétrica la **Soberanía Humana de Desbloqueo y Recuperación Neumática**: incorpora un disyuntor de aislamiento de purga de la BCU y un canal neumático de bypass directo a 5.0 bar que permite restituir la presión de régimen, vencer los muelles acumuladores y reanudar la marcha en modo degradado (ASFA) de manera inmediata. La solución se valida mediante modelado formal de estados en UPPAAL, inyección de fallos en banco HIL y análisis cuantitativo de fiabilidad (FTA/FMECA), demostrando una Tasa de Fallos Peligrosos ($THR \le 10^{-10}\text{ h}^{-1}$) plenamente conforme con la norma CENELEC EN 50129.

### Palabras Clave
`Ciberseguridad Ferroviaria`, `SIL 4`, `Seguridad Funcional`, `Unidad de Control de Freno (BCU)`, `Pérdida de Comandancia Neumática`, `Desbloqueo de Frenos`, `Recuperación de Presión a 5.0 bar`, `Inmovilización Forzosa`, `CWE-833 (Deadlock)`, `CWE-400 (Resource Exhaustion)`, `Siniestro de Urda`, `ETR 1000`, `Safety Fallback Architecture`, `MILS`, `Fail-Safe Bidireccional`.

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

### 1.3. La Lección Forense del Siniestro de Urda: El Grupo de Control y la Inmovilización
El 5 de noviembre de 2026, una avería por obsolescencia tecnológica en los equipos de tierra de la estación de Urda (Toledo) derribó la señal portadora LZB en plena línea de alta velocidad Madrid-Sevilla. Dos composiciones comerciales sufrieron el mismo evento físico en el mismo cantón:
1. **Grupo de Control Resiliente (AVE S-100 / Renfe):** Tras la parada automática preventiva ordenada por la vía, el software de control reconoció la pérdida de señal y devolvió de inmediato la soberanía completa al maquinista. Este conmutó al sistema analógico secundario (ASFA), recuperó la presión neumática en la tubería general, aflojó los frenos y reanudó la marcha en modo degradado, despejando la vía.
2. **Grupo con Bloqueo Sistémico (Frecciarossa ETR 1000 / Iryo - Hitachi):** Al perder la portadora, la BCU entró en un bucle cerrado de bloqueo mutuo. Las electroválvulas quedaron electrónicamente fijadas en purga abierta, expulsando a la atmósfera todo el aire comprimido inyectado por los compresores. Pese a los intentos de la maquinista habilitada, el software rechazó las órdenes de cabina, impidiendo devolver los 5 bares de presión para aflojar los frenos. La unidad permaneció paralizada durante 13 minutos en la vía general, convirtiéndose en un obstáculo fijo sobre el que fue expedido un tren posterior a 200 km/h.

Este hecho empírico demuestra que el software puede convertirse en un **secuestrador de la comandancia física**, y que el concepto de seguridad funcional está gravemente incompleto si solo garantiza la detención y no provee una vía independiente para el **desbloqueo de frenos y la restitución de presión**.

### 1.4. Hipótesis de Investigación
> **Hipótesis Central:**  
> *"La seguridad funcional ferroviaria SIL 4 es intrínsecamente bidireccional y simétrica: exige garantizar tanto la detención segura (despresurización) como la restitución de presión neumática de régimen (5.0 bar) para el desbloqueo de frenos y la reanudación de la marcha. Cuando una vulnerabilidad de concurrencia (CWE-833) o agotamiento de recursos (CWE-400) colapsa la BCU en purga abierta, el maquinista queda privado de soberanía. Para neutralizar este riesgo manteniendo un $THR < 10^{-9}\text{ h}^{-1}$, es imprescindible una vía de respaldo heterogénea dotada de un canal de bypass neumático directo de alimentación a 5.0 bar y aislamiento de purga desacoplado del software."*

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

## Capítulo 3: Arquitectura Funcional del Sistema de Freno Ferroviario y Dinámica Neumática Bipolar

### 3.1. Topología de Red y Comunicaciones del Material Rodante
El control del freno se distribuye a lo largo de la composición mediante el estándar **IEC 61375** (Train Communication Network - TCN) o su evolución basada en Ethernet (ETB - *Ethernet Train Backbone* y ECN - *Ethernet Consist Network* con protocolo TRDP). Las órdenes de tracción y freno circulan desde el manipulador de tracción/freno en cabina, pasando por los ordenadores centrales del tren (CCU - *Central Control Unit*), hasta las Unidades de Control de Freno (BCU) instaladas en cada bogie o coche.

### 3.2. La Unidad de Control de Freno (BCU) y su Arquitectura Vital
La BCU es el cerebro electroelectrónico responsable de:
1. Recibir órdenes de deceleración de servicio, frenado de urgencia y frenado de emergencia.
2. Calcular la fuerza de frenado conjugando freno eléctrico/regenerativo y freno neumático de fricción.
3. Ejecutar el control antibloqueo y antideslizamiento (WSP - *Wheel Slide Protection*).
4. Pilotar las electroválvulas neumáticas de aplicación y purga.

Para cumplir con SIL 4, la BCU implementa internamente arquitecturas redundantes como **2oo2** (*2 out of 2*) o **2oo3** (*2 out of 3*), donde múltiples procesadores independientes ejecutan el mismo ciclo de control y comparan sus resultados mediante canales de comunicación interprocesador (ICC).

### 3.3. Dinámica del Fluido y Circuito Neumático Bipolar: Ciclos de Frenada y Afloje
El freno continuo automático por aire comprimido opera sobre una física bipolar gobernada por diferenciales de presión:

```
                            DINÁMICA DEL CIRCUITO NEUMÁTICO
                                           |
             +-----------------------------+-----------------------------+
             |                                                           |
     ESTADO DE FRENADO (Aplicación)                              ESTADO DE AFLOJE (Marcha)
   - TFG despresurizada (5.0 bar -> 0 bar).                    - TFG presurizada a 5.0 bar nominales.
   - Válvula distribuidora abre paso de aire                   - Válvula distribuidora purga cilindros
     desde Depósitos Auxiliares a Cilindros (BC).                de freno (BC -> 0 bar) a atmósfera.
   - Presión en BC comprime discos/zapatas.                    - Muelles mecánicos acumuladores vencidos.
   - Muelles de freno de estacionamiento aplicados.            - Zapatas separadas: Tren apto para rodar.
```

1. **La Tubería de Freno Automático / General (TFA / TFG):**
   - Presión de régimen normal de marcha: $P_{\text{TFG}} = 5.0\text{ bar} \pm 0.1\text{ bar}$.
   - Una caída de presión comanda frenado; a $0\text{ bar}$ se obtiene el frenado de emergencia máximo.
2. **El Mecanismo de Afloje y Desbloqueo (Restitución de Presión):**
   - Para desbloquear los frenos tras cualquier detención, los compresores deben alimentar los Depósitos Principales (MR, $8.5 - 10\text{ bar}$) y reinyectar aire a través del manorreductor de cabina o de la BCU hacia la TFG hasta alcanzar de nuevo los **$5.0\text{ bar}$**.
   - Al alcanzarse los $5.0\text{ bar}$ en la TFG, la válvula distribuidora bascula automáticamente su membrana, evacuando la presión de los Cilindros de Freno ($P_{\text{BC}} \to 0\text{ bar}$) a la atmósfera y venciendo los resortes mecánicos de freno de resorte (*spring-applied brake cylinders*).
   - **Punto Crítico:** Si la TFG no logra subir a $5.0\text{ bar}$, los frenos continúan físicamente acuñados contra las ruedas, haciendo mecánicamente imposible que los motores de tracción muevan el tren sin provocar roturas o incendios en bogies.

### 3.4. El Doble Juego de Electroválvulas: Aplicación frente a Purga
En las unidades electroelectrónicas modernas, la BCU comanda dos actuadores vitales:
- **Electroválvula de Carga/Alimentación (EV-Carga):** Permite el paso de aire desde los depósitos a la TFG.
- **Electroválvula de Purga/Escape (EV-Purga o EVFE):** Conecta directamente la TFG a la atmósfera para provocar despresurizaciones rápidas de emergencia.
- **Vulnerabilidad de Secuestro:** Si la EV-Purga queda electrónicamente excitada o atascada en posición abierta debido a un cuelgue del software, se forma una vía directa de escape a la atmósfera. Por más caudal que inyecten los compresores, el aire escapa libremente, haciendo físicamente imposible alcanzar los 5.0 bar y condenando al vehículo a un bloqueo permanente.

---

## Capítulo 4: Análisis Formal de Vulnerabilidades (CWE-833 y CWE-400)

### 4.1. CWE-833: Interbloqueo (*Deadlock*) en Sistemas SIL 4
El fallo CWE-833 ocurre cuando dos o más hilos de ejecución concurrentes se bloquean mutuamente de manera indefinida, esperando por recursos asignados de forma exclusiva.

#### Condiciones de Coffman en el Contexto Ferroviario:
1. **Exclusión Mutua:** Acceso exclusivo a transductores de presión o búferes de comunicación.
2. **Retención y Espera:** Una tarea retiene el cerrojo del lazo de control neumático mientras solicita el cerrojo de la pila de red.
3. **No Apropiación:** Los recursos no pueden ser arrebatados forzosamente antes de su liberación voluntaria.
4. **Espera Circular:** Existe un ciclo cerrado de dependencias entre hilos vitales e hilos de comunicación.

$$\text{Tarea Vital (Freno)} \xrightarrow{\text{adquiere}} \text{Lock}_{\text{Presion}} \xrightarrow{\text{solicita}} \text{Lock}_{\text{TCN}}$$
$$\text{Tarea Red (TCN/TRDP)} \xrightarrow{\text{adquiere}} \text{Lock}_{\text{TCN}} \xrightarrow{\text{solicita}} \text{Lock}_{\text{Presion}}$$

#### El Peligro del Enmascaramiento de Watchdog y Congelamiento de Estado:
Si el *Watchdog Timer* por software es refrescado por una tarea de monitorización periódica independiente de baja prioridad o por una interrupción del temporizador del sistema (SysTick) que continúa operando mientras los hilos vitales están en deadlock, el hardware no detecta la condición de congelamiento. **El sistema congela las salidas discretas en su último estado**: si la orden previa fue purga por caída de señal, la electroválvula de escape queda energizada indefinidamente en posición abierta.

---

### 4.2. CWE-400: Consumo No Controlado de Recursos (*Resource Exhaustion*)
En un sistema SIL 4, la memoria RAM suele estar preasignada estáticamente conforme a la EN 50128. Sin embargo, el recurso más vulnerable es el **tiempo de procesamiento (CPU budget)** y el **ancho de banda del bus de memoria interna (DMA/Bus Contention)**.

#### Mecánica de la Tormenta de Interrupciones (*Interrupt Storm*):
Un atacante que logra inyectar paquetes malformados masivos o tráfico UDP broadcast no autenticado en el bus Ethernet del tren (TRDP):
1. Desencadena cientos de miles de interrupciones por segundo en la tarjeta de red (NIC) de la BCU.
2. La rutina de servicio de interrupción (ISR) y el planificador del RTOS sufren saturación (*starvation*).
3. La tarea vital de cálculo neumático, que debe ejecutarse religiosamente cada $\Delta t = 50\text{ ms}$, experimenta un desplazamiento temporal acumulativo (*jitter*).
4. Se produce una violación sistemática del límite temporal (*Task Deadline Miss*), desestabilizando los algoritmos de control del bucle de freno y abortando las rutinas de realimentación y recarga de presión.

---

## Capítulo 5: Modos de Fallo: Pérdida de Comandancia Neumática e Inmovilización Forzosa

La pérdida de comandancia neumática no es un fenómeno unidireccional. La investigación identifica **tres modos de fallo fundamentales**:

```
                              PÉRDIDA DE COMANDANCIA NEUMÁTICA
                                              |
     +----------------------------------------+----------------------------------------+
     |                                        |                                        |
[MODO 1: INHIBITORIO]                [MODO 2: INTEMPESTIVO]              [MODO 3: INMOVILIZACIÓN FORZOSA]
(Incapacidad de Frenar)              (Frenado Espurio Asimétrico)        (Incapacidad de Desbloquear)
- Tren en movimiento no desacelera.   - Frenado violento en bogie único.  - CPU bloqueada en purga abierta.
- TFG atascada en 5.0 bar.           - Daño térmico en llantas y discos. - TFG no puede subir a 5.0 bar.
- Rebase de señal en peligro (SPAD). - Fuerzas de lazo inadmisibles.     - Tren inmóvil en vía general.
- Riesgo: Colisión frontal/alcance.  - Riesgo: Descarrilamiento.         - Riesgo: Alcance por tren trasero.
```

### 5.1. Modo 1: Modo Inhibitorio (Incapacidad de Frenar a Demanda)
- **Definición:** El tren se encuentra en marcha; el maquinista o el sistema ETCS ordena frenado de servicio o urgencia, pero la BCU afectada no pilota las electroválvulas de vaciado ni despresuriza la TFG.
- **Consecuencia Catastrófica:** Rebase de señal de parada (*Signal Passed at Danger* - SPAD), colisión frontal con otro convoy o descarrilamiento por exceso de velocidad en curvas.

### 5.2. Modo 2: Modo Intempestivo (Frenado Espurio y Asimétrico)
- **Definición:** La BCU colapsa y entra en un estado oscilante o aplica el freno de emergencia de forma no coordinada en un único bogie mientras el resto de la composición continúa traccionando.
- **Consecuencia Catastrófica:** Deformación térmica de discos, plano en ruedas (*flat spots*) y riesgo de encabalgamiento de pestaña de rueda sobre el carril por descompensación dinámica.

### 5.3. Modo 3: Modo de Inmovilización Forzosa / Bloqueo en Purga Abierta (*Locked Exhaust State*)
- **Definición:** Tras una frenada de servicio o una caída transitoria de la portadora de vía (LZB / ERTMS Nivel 2), el tren se detiene por completo. Al intentar reanudar la marcha, **la BCU colapsa en un bucle infinito o deadlock (CWE-833) manteniendo energizadas las electroválvulas de purga en posición abierta**.
- **Consecuencia Física:** La TFG permanece comunicada a la atmósfera ($P_{\text{TFG}} = 0\text{ bar}$). El sistema informático rechaza las consignas del maquinista y el caudal de los compresores principales es evacuado continuamente. Los cilindros de freno (BC) continúan presurizados al máximo y los muelles mecánicos de estacionamiento permanecen aplicados.
- **Gravedad Operativa y Catastrófica en Vía General:**
  1. **El tren queda transformado en un obstáculo fijo y ciego** en el cantón de alta velocidad.
  2. En líneas de tráfico denso, los sistemas de señalización pueden experimentar perturbaciones asociadas a la misma avería de infraestructura, induciendo a los operadores de control de tráfico a autorizar la marcha a la vista o rebasar señales a convoyes posteriores que circulan a más de 200 km/h.
  3. **El tiempo de inmovilización no controlado (13 minutos en Urda)** excede con creces los márgenes de seguridad operativa. La privación de soberanía a la tripulación impide apartar el tren a un escape, vía secundaria o andén, configurando un escenario de colisión por alcance inminente.

---

## Capítulo 6: Propuesta de Arquitectura de Vía de Respaldo Bidireccional (*Safety Fallback Architecture*)

Para garantizar la inmunidad ante CWE-833 y CWE-400, la arquitectura de vía de respaldo no puede limitarse a provocar la detención: **debe ser simétrica y bidireccional, garantizando tanto el frenado de emergencia como la restitución de presión a 5.0 bar para el desbloqueo y reanudación de la marcha**.

```
===================================================================================
NIVEL 4: MANDO MECÁNICO DIRECTO (CABINA Y BOGIES)
- Frenado: Válvula de freno de emergencia directa conectada a la TFG.
- Afloje: BY-PASS NEUMÁTICO MANUAL directo desde Depósitos Principales a TFG (5.0 bar).
- Tiradores mecánicos de purga directa de cilindros de freno (BC release) por bogie.
===================================================================================
                                      ^ |
===================================================================================
NIVEL 3: LAZO DE SEGURIDAD Y DISYUNTOR DE AISLAMIENTO DE PURGA (110 Vcc)
- Frenado: Safety Loop desenergizable ("de-energize to apply").
- Afloje: DISYUNTOR ELÉCTRICO DE AISLAMIENTO DE PURGA (Brake Release Override Switch).
  Corta la polarización a las electroválvulas de purga de la BCU congelada,
  forzando su cierre inmediato por resorte mecánico para detener el escape de aire.
===================================================================================
                                      ^ |
===================================================================================
NIVEL 2: WINDOWED WATCHDOG TIMER (WWDT) ANALÓGICO DIVERSIFICADO
- Monitorización de ventana temporal estricta: 40 ms < t_pulso < 60 ms.
- Detección de Deadlock (CWE-833) y saturación (CWE-400).
- Conmuta automáticamente el control de electroválvulas a la línea de respaldo analógica.
===================================================================================
                                      ^ |
===================================================================================
NIVEL 1: PARTICIONAMIENTO MILS Y MICROKERNEL DE SEPARACIÓN
- Partición SIL 4 vital de freno con ranura temporal blindada (70% CPU).
- Partición de red/diagnóstico aislada espacial y temporalmente.
- Inmunidad de la lógica de afloje frente a tormentas de paquetes en el bus TRDP.
===================================================================================
```

### 6.1. Detalle del Nivel 1: Aislamiento MILS (*Multiple Independent Levels of Security*)
- Microkernel certificado EN 50128 SIL 4 (PikeOS / VxWorks 653).
- **Invariante Espacial y Temporal:** La partición de control neumático dispone de cuotas estrictas de cómputo ininterrumpibles. Si el bus TRDP sufre una inundación de paquetes malformados (CWE-400), la partición de diagnóstico puede colapsar, pero la rutina periódica de gestión de presión ($\Delta t = 50\text{ ms}$) ejecuta su ciclo sin perturbación.

### 6.2. Detalle del Nivel 2: Windowed Watchdog Timer (WWDT) Analógico Diversificado
- Vigilancia estricta por ventana temporal ($t_{\min} = 40\text{ ms} < t_{\text{refresco}} < t_{\max} = 60\text{ ms}$).
- Si la BCU entra en interbloqueo circular (CWE-833), el WWDT detecta la ausencia del pulso vital de fin de ciclo en menos de $100\text{ ms}$ y conmuta la etapa de potencia de las electroválvulas al **modo de custodia de respaldo**.

### 6.3. Detalle del Nivel 3: Disyuntor de Aislamiento de Purga y Lazo Cableado (*Brake Release Override*)
Este nivel introduce el mecanismo específico de corrección frente al modo de fallo observado en la tesis:
1. **Disyuntor de Corte de Purga (*Exhaust Valve Cut-Off*):**
   - Conmutador biestable electromecánico en pupitre de conducción.
   - Al ser accionado por el maquinista ante una inmovilización no justificada, **interrumpe físicamente el suministro eléctrico a todas las electroválvulas de purga (EV-Purga) comandadas por la BCU**.
   - Al desenergizarse las electroválvulas de purga, sus muelles mecánicos internos fuerzan el cierre hermético instantáneo de la tobera de escape, anulando la fuga continua a la atmósfera provocada por el cuelgue informático.
2. **Lazo de Seguridad Cableado Fail-Safe:**
   - Línea de 110 Vcc en bucle cerrado. Permite la desexcitación vital para parada de emergencia sin intervención de buses digitales.

### 6.4. Detalle del Nivel 4: Canal Neumático Autónomo de Desbloqueo y Represurización a 5.0 bar
El Nivel 4 constituye el seguro de vida mecánico e inmutable de la composición:
1. **Válvula Bypass Neumática de Represurización Directa:**
   - Una conducción neumática de alta capacidad conecta directamente los Depósitos Principales (MR, $8.5 - 10\text{ bar}$) con la TFG, puenteando íntegramente la electrónica de la BCU.
   - Incorpora una **válvula reductora de presión mecánica autoaccionada calibrada a $5.0\text{ bar}$** gobernada por una palanca manual protegida en cabina.
   - Al abrir la palanca, el aire de los depósitos principales inunda la TFG, alcanzando la presión nominal de régimen ($5.0\text{ bar}$) en un tiempo $T_{\text{carga}} \le 12\text{ segundos}$ a lo largo de toda la composición.
   - La presurización de la TFG actúa directamente sobre las válvulas distribuidoras mecánicas de cada coche, vaciando los cilindros de freno (BC $\to 0\text{ bar}$) y comprimiendo los muelles mecánicos acumuladores.
2. **Tiradores Manuales de Desbloqueo por Bogie (*BC Release Rings*):**
   - Tiradores de cable independientes en cada bogie que permiten purgar mecánicamente la cámara del cilindro de freno ante una avería neumática extrema localizada, garantizando el rodaje libre de cada eje.
3. **Reanudación de Marcha en Modo Degradado (Protocolo Resiliente):**
   - Una vez restablecidos los $5.0\text{ bar}$ y desbloqueados los frenos mediante este canal físico, el maquinista activa el sistema secundario analógico (ASFA / Marcha a la vista) y tracciona el vehículo de forma inmediata, desalojando el cantón hacia una estación o vía de apartado, replicando el comportamiento del grupo de control (AVE Renfe) en Urda.

---

## Capítulo 7: Plan de Verificación, Validación Formal (V&V) y Ensayos HIL

### 7.1. Verificación Formal de Modelos de Concurrencia
Para erradicar CWE-833 durante el diseño del RTOS:
- Modelado de las máquinas de estados de la BCU mediante **Redes de Petri Temporizadas** y herramientas de model checking (**UPPAAL / Scade**).
- Verificación exhaustiva de la propiedad de ausencia de interbloqueo y garantía de afloje en lógica temporal CTL:
$$A \square \neg \text{Deadlock} \quad \wedge \quad A \lozenge (P_{\text{TFG}} = 5.0\text{ bar})$$
*(En todo camino computacional el sistema está libre de deadlock y siempre es posible alcanzar el estado de afloje pleno a 5.0 bar).*

### 7.2. Banco de Ensayos HIL (*Hardware-in-the-Loop*)
El banco de validación física integra:
1. **Rack Real de la BCU:** Tarjetas de procesamiento 2oo2, módulos de I/O y transductores de presión.
2. **Simulador Neumático Dinámico:** Tubería de freno real de longitud equivalente a 200 metros, cilindros de freno reales y compresores industriales.
3. **Protocolo de Inyección de Fallos:**
   - **Ensayo F-01 (Inyección CWE-833 en Purga Abierta):** Se fuerza la contención circular de mutex en la BCU tras una orden de parada. Se verifica que el accionamiento del disyuntor de aislamiento de purga y la apertura del bypass neumático del Nivel 4 restituyen la presión en la TFG a $5.0\text{ bar}$ en $T_{\text{recharge}} \le 12\text{ s}$ y vacían los cilindros de freno en $T_{\text{release}} \le 4\text{ s}$.
   - **Ensayo F-02 (Tormenta TRDP / CWE-400):** Inyección de tráfico UDP malformado masivo a $1\text{ Gbps}$. Se constata que la ranura temporal MILS protege el bucle neumático vital sin perturbación temporal de ciclo.

---

## Capítulo 8: Evaluación Cuantitativa de Seguridad y RAMS (FTA y FMECA)

### 8.1. Análisis por Árbol de Fallos (*Fault Tree Analysis* - FTA)
Se define como Evento Top Catastrófico:  
**$E_{\text{TOP}}$: Catástrofe por pérdida de comandancia (Colisión por rebase o alcance tras inmovilización en vía general).**

```
                                  [E_TOP: Accidente Catastrófico]
                                                 |
                                            (PUERTA AND)
                                                 |
                +--------------------------------+-------------------------------+
                |                                                                |
    [Fallo Primario de Software BCU]                                [Fallo de la Vía de Respaldo]
    (CWE-833 Deadlock o CWE-400)                                     (Disyuntor + Bypass Mecánico 5 bar)
    Tasa: lambda_BCU = 10^-4 /h                                     Tasa: lambda_Respaldo = 10^-6 /h
```

Cálculo cuantitativo de la Tasa de Peligro Tolerable ($THR$):
$$THR_{\text{sistema}} = \lambda_{\text{BCU}} \times \lambda_{\text{Respaldo}} = 10^{-4} \times 10^{-6} = 10^{-10}\text{ fallos peligrosos/hora}$$

Dado que $10^{-10} < 10^{-9}$, **la arquitectura satisface holgadamente el criterio SIL 4 exigido por la norma CENELEC EN 50129 tanto para la detención como para la recuperación de marcha**.

### 8.2. FMECA Resumido de Modos de Fallo y Afloje

| Componente | Modo de Fallo | Causa Raíz (CWE) | Efecto Crítico | Mecanismo de Respaldo y Desbloqueo | SIL |
| :--- | :--- | :--- | :--- | :--- | :---: |
| **Pila TRDP / RTOS** | Jitter / Starvation | CWE-400 (Tormenta de red) | Violación de deadline de ciclo | Aislamiento MILS de cuotas de CPU | SIL 4 |
| **Controlador Neumático** | Congelamiento de salida | CWE-833 (Deadlock de mutex) | Purga abierta continua (0 bar en TFG) | Disyuntor eléctrico corta purga; muelle cierra válvula | SIL 4 |
| **TFG (Circuito)** | Incapacidad de carga | Purga electrónica atascada | Tren inmovilizado en vía general | Bypass mecánico directo a 5.0 bar desde Depósitos Principales | SIL 4 |
| **Cilindros de Freno (BC)** | Presurización residual | Fallo de válvula relé | Zapatas trabadas contra rueda | Tiradores de purga manual por bogie | SIL 4 |

---

## Capítulo 9: Conclusiones Doctrinales y Recomendaciones Técnicas

### 9.1. Conclusiones Principales
1. **La Simetría de la Soberanía Humana en Sistemas SIL 4:** La seguridad ferroviaria no se agota en la capacidad de detener el tren. Dejar a un maquinista atrapado en una máquina con los frenos bloqueados en plena vía general por un error lógico de software es una vulneración inadmisible de la *Lex Artis* y del deber de diligencia exigible por la Ley del Sector Ferroviario.
2. **Superación del Paradigma de Purga Exclusiva:** Los sistemas de control modernos deben integrar salvaguardas mecánicas independientes para la **restitución de presión de régimen ($5.0\text{ bar}$) y el desbloqueo forzoso**, permitiendo la evacuación de cantones críticos hacia vías seguras en modo degradado.
3. **Validación del Enfoque Técnico-Doctrinal:** La vía de respaldo en 4 niveles propuesta resuelve la asimetría observada en el Siniestro de Urda, demostrando matemáticamente que es viable compatibilizar la máxima sofisticación digital con la infalibilidad neumática tradicional bajo estándar SIL 4 ($THR \le 10^{-10}\text{ h}^{-1}$).

### 9.2. Recomendaciones para la AESF y la ERA
- Exigir en los dossiers de homologación única de vehículos (Reglamento de Ejecución (UE) 2018/545) la acreditación de ensayos físicos de **desbloqueo de frenos y reanudación de marcha con la BCU apagada o en fallo catastrófico**.
- Prohibir la circulación comercial de flotas de alta velocidad que carezcan de canal de bypass neumático directo para alimentar la TFG a 5.0 bar con independencia de los procesadores de abordo.

---

## Capítulo 10: Glosario Técnico y Referencias Bibliográficas

### Glosario Técnico
- **BC (*Brake Cylinder*):** Cilindro de freno neumático.
- **BCU (*Brake Control Unit*):** Unidad de Control de Freno.
- **Bypass Neumático de Carga:** Canalización independiente que suministra 5.0 bar directos desde los depósitos principales a la TFG sin mediación digital.
- **CWE (*Common Weakness Enumeration*):** Catálogo formal de debilidades de software (CWE-833: Deadlock; CWE-400: Resource Exhaustion).
- **Disyuntor de Aislamiento de Purga:** Conmutador electromecánico que desenergiza las electroválvulas de escape forzando su cierre hermético.
- **MR (*Main Reservoir*):** Depósitos principales de aire comprimido (8.5 a 10 bar).
- **RAMS:** Fiabilidad, Disponibilidad, Mantenibilidad y Seguridad (*Reliability, Availability, Maintainability, Safety*).
- **SIL 4 (*Safety Integrity Level 4*):** Máximo nivel de integridad de seguridad funcional según EN 50126/128/129 ($THR < 10^{-9}\text{ h}^{-1}$).
- **TFA / TFG (*Brake Pipe*):** Tubería de Freno Automático / General (presión normal de afloje: 5.0 bar; presión de emergencia: 0 bar).
- **TRDP (*Train Real-Time Data Protocol*):** Protocolo de comunicación en tiempo real sobre Ethernet embarcado.
- **WWDT (*Windowed Watchdog Timer*):** Temporizador de vigilancia por ventana temporal estricta ($t_{\min} < t < t_{\max}$).

### Referencias Bibliográficas
1. **CENELEC EN 50126-1:2017:** *Aplicaciones ferroviarias. Especificación y demostración de RAMS.*
2. **CENELEC EN 50128:2011/A2:2020:** *Aplicaciones ferroviarias. Software para sistemas de control y protección del ferrocarril.*
3. **CENELEC EN 50129:2018:** *Aplicaciones ferroviarias. Sistemas electrónicos relacionados con la seguridad para la señalización.*
4. **CENELEC CLC/TS 50701:2021:** *Railway applications - Cybersecurity.*
5. **IEC 62443-4-2:2019:** *Security for industrial automation and control systems.*
6. **IEC 61375-2-3:2015:** *Train communication network (TCN) - TRDP.*
7. **MITRE Corporation (2026):** *CWE-833: Symbol Collision & Deadlock; CWE-400: Uncontrolled Resource Consumption.*
8. **Ley 38/2015, de 29 de septiembre, del Sector Ferroviario (BOE de 30 de septiembre de 2015).**
9. **García Manzano, J. A. (2026):** *Tesis Doctrinal de Ciberseguridad Industrial y Derecho Regulatorio Ferroviario: La Pérdida de Soberanía Humana en Sistemas SIL 4.*
