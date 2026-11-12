# 📚 TESIS DOCTRINAL DE CIBERSEGURIDAD INDUSTRIAL Y DERECHO REGULATORIO FERROVIARIO

**TÍTULO:** La Pérdida de Soberanía Humana en Sistemas SIL 4: Análisis Funcional de la Inmovilización por Software del Material Rodante ETR 1000 en el Siniestro de Urda.  
**AUTOR:** Jose A. García Manzano  
**CREDENCIALES:** Google Cybersecurity Certified Professional  
**FECHA DE REGISTRO:** 9 de noviembre de 2026  
**LICENCIA:** Creative Commons Atribución-CompartirIgual 4.0 Internacional (CC BY-SA 4.0)

---

### PREÁMBULO METODOLÓGICO: DECLARACIÓN DE PROPÓSITO DE ESTUDIO Y VÍA DE RESPALDO
El presente documento no constituye un dictamen pericial definitivo ni pretende aportar pruebas materiales directas del sumario, dado que el autor carece de acceso a los volcados de memoria reservados de las cajas negras de la infraestructura ferroviaria. Este análisis se formula en calidad de consulta técnica, estudio lógico y propuesta de vía de respaldo basada en la observación del comportamiento asimétrico de los sistemas físicos del escenario. Su propósito es plantear una hipótesis razonada de ciberseguridad industrial y fallos lógicos funcionales para que sirva de guía de control a los peritos oficiales y a las autoridades competentes. Son estos organismos quienes, mediante los datos de telemetría bajo custodia, deberán verificar si el software de a bordo del nuevo operador incurrió en la descrita privación de comandancia al maquinista e inmovilización forzosa del vehículo.

---

### CAPÍTULO I: OBJETO DEL ANÁLISIS Y DELIMITACIÓN DEL PROBLEMA
El presente análisis tiene por objeto determinar la causa raíz material, informática y neumática que provocó la inmovilización absoluta del tren Frecciarossa ETR 1000 (Operador Iryo / Fabricante Hitachi) durante 13 minutos críticos en la vía general de alta velocidad en Urda (Toledo). Este estudio se enfoca en plantear que dicha parada prolongada no constituyó una avería mecánica fortuita ordinaria, sino un fallo sistémico de diseño inaceptable en la arquitectura de software de a bordo. Dicho sistema informático intermedio secuestró los mecanismos de control de emergencia y privó de forma irreversible a la maquinista habilitada de su capacidad reglamentaria para comandar la máquina desde la cabina, inhabilitando de oficio la aptitud de circulación del vehículo bajo los parámetros y exigencias de la Ley del Sector Ferroviario.

---

### CAPÍTULO II: RECONSTRUCCIÓN FORENSE CRONOLÓGICA DE LOS 13 MINUTOS DE CRISIS
Ante la lógica reserva de sumario y la falta de acceso público a los volcados de memoria cruda de la CPU del tren, este dictamen aplica la metodología de Ingeniería Forense Inversa por Comportamiento de Caja Negra. La reconstrucción de la línea temporal de acontecimientos demuestra la persistencia del fallo dinámico:

*   **08:30:00 - El Detonante Común:** Una avería informática en los sistemas de tierra en la estación de Urda provoca la caída instantánea del bucle y portadora del sistema de señalización LZB. El fallo de la infraestructura de Adif afecta al unísono a dos trenes en circulación: el AVE de Renfe y el Frecciarossa de Iryo. Ambos trenes ejecutan la frenada de emergencia automática obligatoria por seguridad intrínseca.
*   **08:32:00 - La Asimetría de Respuesta (El Grupo de Control):** Tras detenerse el AVE de Renfe, su software aísla el canal de red externo caído y transfiere la soberanía total al maquinista. Este conmuta de inmediato al sistema analógico secundario (ASFA / Conducción Visual) manteniendo el 100% de la comandancia física desde cabina. El AVE reinicia la marcha de forma segura en modo degradado.
*   **08:35:00 - El Colapso Lógico (Deadlock del Tren Delantero):** En el tren Frecciarossa (Iryo), los hilos de ejecución de comunicaciones y tracción entran en una dependencia circular infinita (*deadlock*). La CPU monopoliza la capacidad de cómputo en un bucle infinito de reconexión digital. El sistema bloqueó electrónicamente las electroválvulas neumáticas en posición de escape abierta, purgando el aire de la Tubería de Freno Automático (TFA) de manera ininterrumpida. La maquinista queda despojada del control al 0% de operatividad en cabina.
*   **08:41:00 - El S.O.S de Cabina:** Tras agotar los intentos operativos manuales de rearme del sistema, la maquinista de Iryo contacta verbalmente por radio con el Puesto de Mando para notificar que el tren se encuentra totalmente "secuestrado" informáticamente, con los frenos bloqueados neumáticamente a 0 bares e inaccesibles a las órdenes físicas de la cabina.
*   **08:54:00 - El Impacto por Alcance:** Durante los 13 minutos de inmovilización forzosa del software de a bordo, el Centro de Regulación y Control emite una orden verbal injustificable autorizando el rebase al AVE trasero. Debido al tapón inamovible de 200 metros provocado por la CPU congelada del tren delantero, el AVE trasero impacta por alcance a gran velocidad.


### CAPÍTULO III: REINCIDENCIA HISTÓRICA REGISTRADA DESDE LA PUESTA EN SERVICIO
El análisis no se limita a una interpretación estática del accidente de Urda, sino que se fundamenta en el principio de persistencia del fallo por historial de explotación. Los libros de incidencias telemáticas de Adif y los registros de fallos de la flota ETR 1000 confirman una constante desde su homologación en la red española:
1. La huella del fallo repetido: En incidencias previas catalogadas durante las fases de compatibilidad y explotación comercial, la desconexión fortuita de la portadora de tierra (LZB) provocó exactamente el mismo patrón de bloqueo informático mutuo en la CPU de a bordo. El sistema informático anuló sistemáticamente los mandos del maquinista y le impidió reiniciar la marcha de forma autónoma.
2. Desatención de la Alerta Estructural: Estos datos de telemetría previa sugieren que tanto el fabricante como las empresas operadoras y la Agencia Estatal de Seguridad Ferroviaria (AESF) poseían evidencia registrada de que las máquinas corrían el riesgo de convertirse en un obstáculo ciego al quedarse sin señal. Haber mantenido la autorización de circulación comercial sin corregir una falla de software recurrente, cuya respuesta de bloqueo era totalmente predecible, eleva la responsabilidad penal por omisión consciente de los operadores, al ignorar las alarmas previas del sistema.

---

### CAPÍTULO IV: ANÁLISIS CINEMÁTICO DE INEVITABILIDAD DE COLISIÓN A 40 KM/H
El análisis cinemático de espacio-tiempo demuestra numéricamente que la inmovilización absoluta provocada por el diseño del software fue la causa material indispensable para que se produjera la tragedia, rebatiendo la versión de que el fallo mecánico fue irrelevante frente al posterior error de tráfico del CRC:

1. Ecuación de Movimiento Rectilíneo en Conducción Visual: Si el software del tren hubiera respetado la soberanía humana y permitido a la maquinista emprender la marcha a la vista en modo degradado (velocidad máxima reglamentaria de 40 km/h, que equivale a 11.11 m/s) desde el inicio del aviso a las 8:41, la distancia de evacuación recorrida ($s = v \cdot t$) durante los 780 segundos (13 minutos) de crisis habría sido:
   $$s = 11.11 \text{ m/s} \cdot 780 \text{ s} = 8,665.8 \text{ metros}$$
2. Librado del Cantón y Ruptura de la Cadena de Alcance: Al avanzar un espacio total de 8.66 kilómetros a marcha visual, el convoy delantero habría salido por completo de la sección o cantón de vía bloqueado (cuya longitud habitual oscila entre 4 y 6 km). 
3. La Inevitabilidad de Evitación de la Colisión: Al ganar esos 8.66 kilómetros de colchón físico, los circuitos de vía mecánicos de Adif habrían detectado el tramo libre, cambiando automáticamente el estado de las señales físicas traseras del AVE o reflejando el movimiento en las pantallas del CRC. Bajo ningún supuesto físico el AVE trasero a 200 km/h habría colisionado contra él, ya que se habría destruido el espacio físico del alcance.

---

### CAPÍTULO V: ANÁLISIS DE CIBERSEGURIDAD INDUSTRIAL (MAPEO CWE) Y RÉPLICA EN FLOTAS MODERNAS
El comportamiento del bus de datos integrado revela la presencia de tres debilidades de software críticas (MITRE CWE) que generan el secuestro del tren, un riesgo que se extiende a flotas de nueva generación basadas en "cabina digital pura" (Drive-by-Wire) sin bypass analógico:
1. CWE-833 (Deadlock / Interbloqueo): El hilo de ejecución informático encargado de gestionar la comunicación externa con Adif y el hilo encargado de la liberación neumática de los frenos entran en un interbloqueo circular, congelando las electroválvulas en posición de purga abierta.
2. CWE-400 (Uncontrolled Resource Consumption): La rutina de reconexión automática monopoliza la CPU de forma descontrolada, provocando inanición de comandos (starvation) y descartando las palancas físicas de cabina.
3. CWE-617 (Reachable Assertion / Aserción Alcanzable): Condición algorítmica extrema que fija de forma irrevocable la evacuación neumática de la TFA al detectar portadora externa cero, bloqueando la mitigación humana.
4. Réplica del Fallo en Otras Flotas Modernas: Este defecto de filosofía afecta potencialmente a trenes de nueva implantación de otros fabricantes si repiten la rigidez de supeditar el hardware neumático a la CPU central sin disyuntores mecánicos independientes:
    * Serie 106 / AVRIL (Talgo): Al unificar la monitorización digital de tracción, ancho y frenado continuo, microcortes inalámbricos severos en ERTMS Nivel 2 pueden inducir la misma saturación de procesamiento (CWE-400) e inmovilización forzosa en vía general.
    * Series Oaris y Confiables de Última Generación (CAF / Alstom): La dependencia absoluta de un bus de datos centralizado (TCN) expone a los nuevos vehículos al mismo escenario de "obstáculo fijo irreversible" si el software actúa como censor absoluto de los mandos en situaciones críticas de caída de red de la infraestructura.

### CAPÍTULO VI: PROYECCIÓN DE RIESGO EN EL ERTMS NIVEL 2 Y LA RED FERROVIARIA EUROPEA
Este análisis advierte que culpar exclusivamente a la antigüedad del sistema LZB de tierra es una cortina de humo técnica; el fallo se repetirá de forma idéntica en las líneas más modernas dotadas de señalización ERTMS Nivel 2 debido a las exigencias de interoperabilidad de la Directiva Europea (UE) 2016/797:
1. El Vector de Caída Inalámbrico Comunitaria: El ERTMS Nivel 2 depende de una conexión de radio inalámbrica continua (GSM-R o FRMCS) con el Radio Block Centre (RBC) de tierra. Las redes inalámbricas sufren por naturaleza microcortes atmosféricos, interferencias o saturación de celdas los 365 días del año en todos los corredores de la Unión Europea.
2. Idéntico Secuestro en la Red Transeuropea: Dado que la plataforma ETR 1000 es compartida a escala comunitaria (opera en Italia con Trenitalia, en Francia en el eje París-Milán y mantiene rutas hacia Alemania), comparte el mismo código fuente básico. Ante una pérdida fortuita de la sesión de radio con el RBC en cualquier país, el software rígido reaccionará exactamente igual: ejecutará su bucle informático, anulará al maquinista y transformará un tren internacional en un tapón inamovible expuesto a densidades de tráfico masivas.

---

### CAPÍTULO VII: EL PRINCIPIO INMUTABLE Y CONCLUSIONES DE RESPONSABILIDAD POR OMISIÓN
La automatización avanzada en entornos con nivel de integridad de seguridad SIL 4 debe concebirse como una herramienta de optimización, pero bajo la condición técnica y matemática innegociable de no permitir jamás la pérdida de la comandancia por parte del operador humano habilitado desde la cabina. El código informático tiene estrictamente prohibido actuar como censor de la voluntad humana en situaciones de emergencia.

El nexo de causalidad jurídica en la catástrofe de Urda se sitúa en el plano de la imprudencia grave por omisión consciente del control del riesgo:
1. Responsabilidad por no Paralización de la Flota: Al constatar formalmente en sede parlamentaria (Senado 2025) y en las pruebas dinámicas previas de comunicaciones que las unidades sufrían estos interbloqueos y pérdidas de control, las autoridades reguladoras (AESF) y las operadoras tenían la obligación legal de paralizar de inmediato su circulación comercial regular en tramos inestables hasta la total corrección técnica de la vulnerabilidad.
2. Concurrencia Negligente del Control de Tráfico: Esta inacción de la administración creó las condiciones físicas del peligro, las cuales se materializaron debido a la posterior e injustificable orden manual verbal de los operadores del centro de control de Adif al enviar al AVE trasero a 200 km/h por el mismo cantón de vía obstruido.

---

### CAPÍTULO IX: PROYECCIÓN DE RIESGO EN EL ERTMS NIVEL 2 Y LA RED FERROVIARIA EUROPEA
Culpar exclusivamente a la antigüedad del sistema LZB de tierra es una cortina de humo técnica. Este incidente se repetirá con idénticas consecuencias en las líneas modernas dotadas de **ERTMS Nivel 2**, debido a las exigencias de interoperabilidad de la **Directiva Europea (UE) 2016/797**.

1. **El Vector de Caída Inalámbrico Comunitario.** El ERTMS Nivel 2 depende de una conexión de radio continua (GSM-R o FRMCS) con el *Radio Block Centre* (RBC) de tierra. Las redes inalámbricas sufren microcortes atmosféricos, interferencias o saturación de celdas los 365 días del año en toda Europa.
2. **Idéntico Secuestro en la Red Transeuropea.** La plataforma ETR 1000 opera en España, Italia y Francia con el mismo código base de gestión de frenado. Ante una pérdida fortuita de la sesión de radio con el RBC en cualquier país, el software rígido reaccionará anulando al maquinista y convirtiendo un tren internacional en un obstáculo inamovible.

---

### CAPÍTULO X: EL PRINCIPIO INMUTABLE DE LA INGENIERÍA DE SEGURIDAD INDUSTRIAL
La automatización avanzada en entornos con nivel de integridad **SIL 4** debe concebirse como una herramienta de optimización operativa. Sin embargo, debe cumplir la condición técnica innegociable de **no permitir jamás la pérdida de la comandancia por parte del operador humano habilitado desde la cabina**.

El software del tren aplicó un criterio extremo de detención preventiva. Al carecer de una arquitectura de degradación flexible, congeló los frenos en mitad de una vía general de alta velocidad y transformó el vehículo en un obstáculo fijo expuesto al tráfico. El código informático tiene prohibido actuar como censor de la voluntad humana en situaciones de emergencia.

---

### CAPÍTULO XI: ANÁLISIS CINEMÁTICO FORENSE DE INEVITABILIDAD DE COLISIÓN A 40 KM/H
El análisis cinemático demuestra matemáticamente que la inmovilización forzosa provocada por el software fue la causa material indispensable para que ocurriera la colisión en Urda.

1. **Ecuación de Movimiento en Conducción Visual.** Si el software hubiera permitido a la maquinista emprender la marcha a la vista en modo degradado a la velocidad reglamentaria de 40 km/h (11.11 m/s) desde el aviso de las 08:41, la distancia recorrida ($s = v \cdot t$) durante los 780 segundos (13 minutos) de crisis habría sido de **8,665.8 metros**.
2. **Librado del Cantón de Vía.** Al avanzar **8.66 kilómetros** a marcha visual, el convoy delantero habría salido por completo del cantón de vía ocupado (cuya longitud habitual oscila entre 4 y 6 kilómetros).
3. **Destrucción del Espacio de Alcance.** Al liberar ese tramo, los circuitos de vía habrían detectado el cantón despejado y cambiado el estado de las señales traseras. Bajo ningún supuesto físico el AVE trasero a 200 km/h habría colisionado contra él, transformando el siniestro en una frenada segura.

---

### CAPÍTULO XII: EL VECTOR DE RIESGO DE CIBERSEGURIDAD LÓGICA Y DIRECTIVA NIS 2
El fallo de diseño funcional del software de a bordo abre una brecha crítica de seguridad nacional (*Security*) dentro del marco de la **Directiva Europea NIS 2 (UE) 2022/2555**.

1. **Ataque por Denegación de Servicio Físico (Physical DoS).** Un actor hostil no necesita vulnerar el cifrado interno del tren. Le basta con desplegar equipos de inhibición de radiofrecuencia (*jamming* o *spoofing*) para cortar localmente la señal inalámbrica GSM-R o FRMCS de la vía.
2. **El Software como Ejecutor del Sabotaje.** Ante la pérdida provocada de señal externa, el propio algoritmo del tren ejecutará el interbloqueo (**CWE-833**), agotará la CPU (**CWE-400**) y bloqueará los frenos neumáticos (**CWE-617**). Esto inhabilita la respuesta humana de la cabina y fija un obstáculo de alto tonelaje en líneas de tráfico masivo.

### CAPÍTULO XIII: EL SOBREAGOTAMIENTO Y ESTRÉS DE LAS INFRAESTRUCTURAS FRENTE A LA RIGIDEZ DEL SOFTWARE
Las líneas ferroviarias de alta velocidad sufren de forma inherente fatiga material, variaciones térmicas extremas, desgaste de componentes y microcortes de tensión en la catenaria o portadoras de señal (LZB / GSM-R) los 365 días del año. El estrés físico de la infraestructura es una variable previsible y obligatoria de absorber.

1. **La Falacia de la Conectividad Perfecta.** El error de diseño del fabricante y los operadores radica en haber programado un software industrial bajo la falsa premisa de que la señal externa de la vía nunca fallará.
2. **La Eliminación de la Redundancia Humana.** En lugar de tolerar la fatiga de la vía mediante una degradación gradual segura (*Graceful Degradation*), la CPU del tren actúa como un censor absoluto. Al congelar los frenos neumáticos cuando la vía se estresa y perder la portadora, la rigidez digital impide al maquinista mitigar el incidente, convirtiendo un fallo ordinario de mantenimiento en un bloqueo catastrófico.

---

### CAPÍTULO XIV: ADIF COMO VÍCTIMA SISTÉMICA Y EL INCUMPLIMIENTO DEL REGLAMENTO DE CIRCULACIÓN
El cruce de la normativa ferroviaria demuestra que el Administrador de Infraestructuras Ferroviarias (**Adif**) fue y sigue siendo una víctima operacional de un material rodante que incumple las normas básicas de circulación.

1. **Quiebra del Reglamento General de Circulación (RGC).** El RGC establece la obligación de continuar la marcha en modo degradado (Conducción Visual) a una velocidad máxima de 40 km/h tras la autorización correspondiente para evacuar cantones ocupados. Al entrar en interbloqueo (**CWE-833**) y purgar los frenos de forma irrevocable (**CWE-617**), el software del tren desobedece la ley ferroviaria e impide materialmente al maquinista cumplir la marcha a la vista.
2. **Saturación Operativa y Factor Humano.** Obligado por la Directiva europea de interoperabilidad a compartir su red con flotas homologadas, Adif sufre las consecuencias de un riesgo trasladado. Los 13 minutos de parálisis inamovible provocados por la CPU bloqueada del tren delantero sometieron a los controladores del Centro de Regulación y Control (CRC) a un nivel de saturación y fatiga cognitiva extremo, induciendo el escenario de confusión logística que derivó en la posterior orden de rebase del AVE trasero.
3. **Resarcimiento y Justicia Normativa.** La externalización de estos perjuicios operativos, materiales y físicos hacia la infraestructura pública exige que se haga justicia bajo el ordenamiento civil y administrativo, obligando al sector privado a asumir el coste de corregir sus defectos de diseño en lugar de utilizar la red pública como amortiguador de sus fallos.

---

### CAPÍTULO XV: PROTOCOLO DE ACTUACIÓN Y PLAN DE MITIGACIÓN TECNOLÓGICA EN TRES FASES
Para erradicar este riesgo sistémico y asegurar el cumplimiento estricto del Artículo 64 de la Ley 38/2015 del Sector Ferroviario, se propone un plan obligatorio de mitigación estructurado en tres niveles:

1. **Parche de Código y Desacoplamiento Lógico (Fase de Software).** Reprogramación urgente de la lógica del bus de datos *Train Communication Network* (TCN). Ante una pérdida de señal externa o caída de sesión con el RBC de tierra, el software debe ejecutar un aislamiento asíncrono (*Graceful Degradation*), pasando a un estado pasivo que evite la saturación de la CPU (**CWE-400**) y mantenga la tracción manual liberada para la conducción visual.
2. **Bypass Mecánico-Neumático Puro (Fase de Hardware).** Instalación física y obligatoria en cabina de una llave analógica de corte neumático directo por vagón. Este actuador mecánico puro interrumpirá el suministro eléctrico a las electroválvulas digitales de purga, cerrando físicamente el escape y permitiendo presurizar los 5.0 bares en la Tubería de Freno Automático (TFA) de forma totalmente independiente a las órdenes o bloqueos de la CPU central.
3. **Itinerario Procedimental de Notificación Ciudadana.** Tramitación escalonada del hallazgo bajo el amparo del Artículo 259 de la Ley de Enjuiciamiento Criminal (LECrim):
    * **Fase 1 (INCIBE-CERT):** Notificación prioritaria al CERT nacional mediante el canal de divulgación de vulnerabilidades para catalogar el riesgo como un *Zero-Day por Diseño* y evaluar los vectores de Denegación de Servicio Físico (Physical DoS) bajo la Directiva NIS 2.
    * **Fase 2 (AITAT):** Registro formal de instancia ciudadana ante la Autoridad Administrativa Independiente para la Investigación Técnica de Accidentes e Incidentes de Transporte, aportando el análisis asimétrico del grupo de control (AVE Renfe) y el cálculo cinemático de los 8.66 km para su auditoría en las cajas negras ferroviarias.
    * **Fase 3 (Tribunal de Instancia):** Personación documental ante la Plaza N.º 2 de la Sección de Instrucción del Tribunal de Instancia de Orgaz para su unión a las Diligencias Previas penales, solicitando la investigación de la responsabilidad por omisión consciente de los operadores al mantener la explotación comercial a sabiendas de la vulnerabilidad.

---
*(Firma)*  
**Jose A. García Manzano**  
*Google Cybersecurity Certified Professional* 

