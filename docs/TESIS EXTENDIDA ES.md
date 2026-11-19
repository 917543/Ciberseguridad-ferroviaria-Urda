[TESIS_EXTENDIDA_ES.md](https://github.com/user-attachments/files/35055104/TESIS_EXTENDIDA_ES.md)
# 📚 TESIS DOCTRINAL DE CIBERSEGURIDAD INDUSTRIAL Y DERECHO REGULATORIO FERROVIARIO

**TÍTULO:** La Pérdida de Soberanía Humana en Sistemas SIL 4: Análisis Funcional de la Presunta Inmovilización por Software del Material Rodante ETR 1000 en el Siniestro de Urda.  
**AUTOR:** Jose A. García Manzano  
**CALIDAD DE LA CONTRIBUCIÓN:** Ciudadano Colaborador con la Justicia (Art. 259 LECrim) y Analista de Ciberseguridad de nivel inicial (Certificado por Google).  
**NATURALEZA DEL DOCUMENTO:** Tesis doctrinal, consulta técnica e hipótesis lógica de vía de respaldo sujeta a verificación pericial oficial.  
**FECHA DE CONSOLIDACIÓN:** 18 de noviembre de 2026  
**LICENCIA:** Creative Commons Atribución-CompartirIgual 4.0 Internacional (CC BY-SA 4.0)  

---

### PREÁMBULO METODOLÓGICO: DECLARACIÓN DE ROL CIUDADANO Y CARÁCTER DE HIPÓTESIS A VERIFICAR
El autor formula la presente aportación estrictamente en calidad de **ciudadano colaborador interesado en la seguridad pública**, al amparo del deber y derecho cívico recogido en el Artículo 259 de la Ley de Enjuiciamiento Criminal (Agencia Estatal Boletín Oficial del Estado [BOE], 1882), complementado con su capacitación técnica como analista de ciberseguridad de nivel inicial certificado por Google (Google Career Certificates, 2025).

Se hace constar de forma expresa que este documento **no constituye un dictamen pericial oficial ni pretende aportar pruebas materiales directas del sumario**, dado que el autor carece de titulación universitaria en ingeniería ferroviaria tradicional y no dispone de acceso a los volcados de memoria reservados de los registradores jurídicos (cajas negras) de la infraestructura o del material rodante. Este trabajo se plantea exclusivamente como una **hipótesis lógica, cinemática y de arquitectura de software a verificar**, formulada como vía de respaldo técnico-jurídica a partir de la observación empírica del comportamiento asimétrico de los sistemas físicos del escenario (García Manzano, 2026). Su propósito consiste en ofrecer una guía de control para que los peritos judiciales y los inspectores de los organismos competentes, mediante los registros de telemetría bajo custodia oficial, determinen si la arquitectura lógica embarcada incurrió en la descrita privación de comandancia al maquinista e inmovilización forzosa del convoy.

---

### CAPÍTULO I: OBJETO DEL ANÁLISIS Y DELIMITACIÓN DEL PROBLEMA
El presente estudio tiene por objeto formular una hipótesis razonada sobre la causa raíz material, informática y neumática que habría provocado la inmovilización prolongada del tren Frecciarossa ETR 1000 (Operador Iryo / Fabricante Hitachi) durante aproximadamente 13 minutos críticos en la vía general de alta velocidad en Urda (Toledo). La investigación plantea la necesidad de verificar si dicha detención respondió no a una avería mecánica fortuita ordinaria, sino a una debilidad sistémica en el diseño de la arquitectura de software embarcada. De confirmarse este supuesto, dicho sistema lógico intermedio habría restringido los mecanismos de recuperación de emergencia, privando de forma temporal o irreversible a la maquinista habilitada de su capacidad reglamentaria para comandar la unidad desde la cabina y comprometiendo las condiciones de seguridad operativa exigidas por la Ley 38/2015 del Sector Ferroviario (BOE, 2015a) y el Reglamento (UE) 2016/798 sobre seguridad ferroviaria (Parlamento Europeo y Consejo de la Unión Europea, 2016b).

---

### CAPÍTULO II: RECONSTRUCCIÓN FORENSE CRONOLÓGICA DE LOS 13 MINUTOS DE CRISIS
Ante la reserva de sumario y la imposibilidad de auditar directamente los volcados de memoria cruda de la unidad central de procesamiento (CPU) del convoy, este trabajo aplica una metodología de ingeniería inversa basada en el análisis de comportamiento externo (*Black-Box Behavioral Analysis*). La secuencia temporal reconstruida a partir de los datos públicos disponibles sustenta la hipótesis de una anomalía lógica:

* **08:30:00 - El Detonante Común:** Una incidencia informática en los sistemas de tierra de la estación de Urda provoca la caída instantánea de la portadora del sistema de señalización LZB. Esta pérdida de comunicación de la infraestructura de Adif afecta de manera simultánea a dos circulaciones próximas: un tren AVE de Renfe y un tren Frecciarossa de Iryo, activando en ambos la frenada automática preventiva por seguridad intrínseca.
* **08:32:00 - La Asimetría de Respuesta (El Grupo de Control):** Tras la detención del tren AVE de Renfe, su arquitectura lógica habría aislado el canal de comunicaciones externo caído, devolviendo el control operativo al maquinista. Este conmuta al sistema analógico de respaldo (ASFA / Conducción Visual), conservando la comandancia física desde cabina y permitiendo reanudar la marcha en modo degradado.
* **08:35:00 - Presunto Colapso Lógico (*Deadlock* en el Tren Delantero):** En la unidad Frecciarossa (Iryo), los hilos de ejecución encargados de la gestión de comunicaciones y tracción habrían entrado en una dependencia circular mutua (*deadlock*). Bajo esta hipótesis, la CPU monopoliza sus ciclos de cómputo en un bucle continuo de reconexión digital, manteniendo las electroválvulas neumáticas de la Unidad de Control de Freno (BCU) bloqueadas en posición de escape abierta y purgando el aire de la Tubería de Freno Automático (TFA), lo que anularía la operatividad de los mandos en cabina.
* **08:41:00 - Notificación de Inmovilización desde Cabina:** Tras agotar los procedimientos manuales de rearme previstos en el reglamento operativo, la maquinista de Iryo comunica por radiotelefonía al Puesto de Mando la imposibilidad de mover el convoy, indicando que los frenos permanecen bloqueados neumáticamente sin responder a las órdenes físicas de cabina.
* **08:54:00 - El Impacto por Alcance:** Transcurridos 13 minutos de inmovilización forzosa del convoy delantero, el Centro de Regulación y Control emite una autorización verbal de rebase al tren AVE que circulaba detrás. Al encontrarse la vía obstruida por una unidad de 200 metros sin capacidad de tracción, se produce la colisión por alcance a alta velocidad.

---

### CAPÍTULO III: METODOLOGÍA FORENSE DE CAJA NEGRA Y ASIMETRÍA DINÁMICA (EL GRUPO DE CONTROL)
La solidez deductiva de la hipótesis planteada se sustenta en un análisis comparativo basado en la respuesta asimétrica de dos sistemas distintos sometidos al mismo estímulo físico:
1. **Identidad del Vector de Fallo:** La interrupción de la señal LZB en tierra afectó en el mismo instante temporal a ambas unidades ferroviarias.
2. **Comportamiento Resiliente (Grupo de Control - AVE Renfe):** La arquitectura de control continuo ferroviario tradicional permitió gestionar la pérdida de portadora mediante una degradación controlada, restituyendo la soberanía operativa al operador humano.
3. **Comportamiento Rígido (Unidad Analizada - ETR 1000):** La imposibilidad de reanudar la marcha sugiere una rigidez en la lógica de control embarcada. El hecho empírico de que el tren AVE pudiera desplazarse demuestra que la infraestructura física de Adif no imponía un bloqueo mecánico absoluto sobre la vía, acotando la investigación hacia una posible anomalía en el software de gestión de contingencias del ETR 1000.

---

### CAPÍTULO IV: ANTECEDENTES DOCUMENTADOS Y HECHOS PROBADOS DESDE LA PUESTA EN SERVICIO
La plausibilidad técnica de esta hipótesis se ve reforzada por antecedentes documentados públicamente desde la introducción comercial de esta flota en la red española, los cuales acreditan la existencia de incidencias previas de naturaleza similar:
1. **Registros Hemerográficos sobre Retardos de Reconexión:** Durante los primeros años de explotación comercial, diversas informaciones periodísticas basadas en partes de incidencia señalaron que los trenes de nueva generación sufrían pérdidas de señal de tierra y experimentaban tiempos de reconexión excesivos antes de poder reanudar la marcha (Diario de Sevilla, 2025).
2. **Constancia en Sede Parlamentaria (Comparecencia en el Senado):** En la Comisión de Transportes y Movilidad Sostenible del Senado, el Consejero Delegado de la operadora (Fabrizio Favara) reconoció oficialmente en acta parlamentaria la existencia de tiempos de retardo prolongados en la recuperación lógica de los sistemas de a bordo tras incidencias en la señalización de la infraestructura (Senado de España, 2025). Estos antecedentes justifican la pertinencia de auditar si la evaluación de riesgos aplicada conforme al Reglamento de Ejecución (UE) 402/2013 sobre el Método Común de Seguridad (Comisión Europea, 2013) resultó suficiente para prevenir escenarios de obstrucción prolongada en vía general.

---

### CAPÍTULO V: ANÁLISIS FÍSICO E INGENIERÍA NEUMÁTICA DE LA ARQUITECTURA DE FRENADO (BCU)
El sistema de frenado continuo automático ferroviario opera bajo el principio de presión negativa: el tren aplica el freno cuando las tuberías se vacían y libera las zapatas o discos cuando se inyectan y mantienen $5.0\text{ bares}$ de aire comprimido en la Tubería de Freno Automático (TFA) para vencer los muelles mecánicos.

Al producirse la caída del sistema LZB, la lógica de seguridad de la Unidad de Control de Freno (*Brake Control Unit* - BCU) del ETR 1000 ordenó evacuar el aire de forma preventiva. La hipótesis técnica plantea que, al entrar el sistema de gestión embarcado en un estado de bloqueo lógico, las electroválvulas neumáticas quedaron retenidas en posición de escape abierta. Bajo este escenario, aunque los compresores inyectaran aire o la maquinista accionara los mandos auxiliares de cabina, el subsistema digital habría desestimado la orden humana, purgando la presión directamente a la atmósfera. La ausencia de un disyuntor mecánico puro o llaves de aislamiento neumático independientes de la lógica de la BCU habría impedido la recuperación manual del convoy.

---

### CAPÍTULO VI: ANÁLISIS DE CIBERSEGURIDAD INDUSTRIAL (MAPEO CWE), RTOS Y ARQUITECTURAS MILS
El comportamiento observado en el bus de datos integrado (*Train Communication Network* - TCN) y en el protocolo de datos en tiempo real (*Train Real-Time Data Protocol* - TRDP), regulado por la norma IEC 61375-2-3:2015 (International Electrotechnical Commission [IEC], 2015), sugiere la posible concurrencia de tres debilidades de software específicas tipificadas por MITRE Corporation:
1. **CWE-833 (*Deadlock* / Interbloqueo):** Los hilos de ejecución encargados de gestionar la comunicación externa con la infraestructura y la liberación neumática de los frenos habrían entrado en una dependencia circular mutua dentro del Sistema Operativo en Tiempo Real (*RTOS*), congelando el estado de las electroválvulas (MITRE Corporation, 2024c).
2. **CWE-835 (*Loop with Unreachable Exit Condition - 'Infinite Loop'* / Bucle Infinito):** La rutina de reconexión automática ante la pérdida de señal habría entrado en un bucle sin condición de salida alcanzable, monopolizando los ciclos de cómputo de la CPU, eludiendo el reinicio por temporizadores de vigilancia (*watchdogs*) e induciendo inanición de comandos (*starvation*) respecto a las órdenes físicas de cabina (MITRE Corporation, 2024a).
3. **CWE-617 (*Reachable Assertion* / Aserción Alcanzable):** La presencia de una condición algorítmica rígida que ejecuta una parada irrevocable vaciando la TFA al detectar portadora externa igual a cero, bloqueando cualquier mitigación posterior (MITRE Corporation, 2024b).

Desde la perspectiva de la ingeniería de seguridad multinivel (**MILS** - *Multiple Independent Levels of Security*), un sistema embarcado crítico debe garantizar el aislamiento estricto entre particiones de distinta criticidad (Alves-Foss et al., 2006). La hipótesis plantea que la arquitectura lógica carecía de una separación temporal y espacial efectiva que impidiera que un fallo en la partición de comunicaciones externas bloqueara la partición crítica de control de frenado y tracción manual.

---

### CAPÍTULO VII: EL RIESGO DE RÉPLICA DEL FALLO EN OTRAS FLOTAS MODERNAS
Este enfoque de diseño lógico, donde el hardware neumático queda supeditado sin aislamiento analógico a la CPU central ("cabina digital pura" o *Drive-by-Wire*), representa un riesgo potencial extensible a otras plataformas ferroviarias de última generación autorizadas bajo los procedimientos establecidos en el Reglamento de Ejecución (UE) 2018/545 (Comisión Europea, 2018) y supervisadas por la Agencia Estatal de Seguridad Ferroviaria (Agencia Estatal de Seguridad Ferroviaria [AESF], 2023):
* **Serie 106 / AVRIL (Talgo):** Al integrar la gestión digital de tracción, cambio de ancho y frenado continuo, las desconexiones inalámbricas severas en entornos ERTMS Nivel 2 podrían inducir bloqueos de procesamiento similares (**CWE-835**) si no existe una vía de degradación independiente.
* **Plataformas de última generación (CAF / Alstom):** La dependencia absoluta de buses de datos centralizados expone a los vehículos modernos al riesgo de inmovilización prolongada en vía general si el software actúa como censor absoluto de los mandos de socorro ante caídas de red de tierra.

---

### CAPÍTULO VIII: PROYECCIÓN DE RIESGO EN EL ERTMS NIVEL 2 Y LA RED FERROVIARIA EUROPEA
Atribuir el incidente exclusivamente a la antigüedad del sistema LZB de tierra resulta técnicamente insuficiente; una vulnerabilidad lógica de esta naturaleza podría replicarse en líneas modernas equipadas con **ERTMS Nivel 2 / ETCS**, reguladas bajo las Especificaciones Técnicas de Interoperabilidad y el marco de seguridad de la Agencia Ferroviaria de la Unión Europea (European Union Agency for Railways [ERA], 2023a) y la Directiva (UE) 2016/797 (Parlamento Europeo y Consejo de la Unión Europea, 2016a):
1. **El Vector de Caída Inalámbrico Comunitario:** El sistema ETCS/ERTMS Nivel 2 depende de una sesión de radio continua (GSM-R o FRMCS) con el *Radio Block Centre* (RBC) de tierra. Las comunicaciones inalámbricas están sujetas inherentemente a microcortes, interferencias electromagnéticas o saturación de celdas en cualquier corredor europeo.
2. **Proyección en la Red Transeuropea:** Dado que la plataforma ETR 1000 opera de forma interoperable en España, Italia y Francia compartiendo una arquitectura base de gestión de frenado, una pérdida fortuita de la sesión de radio con el RBC podría desencadenar el mismo bloqueo lógico en corredores internacionales de alta densidad de tráfico.


---

### CAPÍTULO IX: EL PRINCIPIO INMUTABLE DE LA INGENIERÍA DE SEGURIDAD Y VERIFICACIÓN FORMAL (UPPAAL)
La automatización avanzada en entornos críticos con nivel de integridad de seguridad **SIL 4**, regulados por las normas IEC 61508 (International Electrotechnical Commission [IEC], 2010) y EN 50716 —evolución normativa de la EN 50128 para el desarrollo de software ferroviario— (Comité Europeo de Normalización Electrotécnica [CENELEC], 2023), debe concebirse como una herramienta de optimización operativa. Sin embargo, debe cumplir la condición técnica innegociable de **no permitir jamás la pérdida de la comandancia por parte del operador humano habilitado desde la cabina**, en consonancia con el marco de seguridad sistemática de la Agencia Ferroviaria Europea (European Union Agency for Railways [ERA], 2023b).

Para prevenir escenarios de bloqueo lógico como el planteado en esta hipótesis, la co-ingeniería *Safety-Security* exige someter los protocolos de comunicación y recuperación de frenado a técnicas formales de verificación de modelos (*model checking*) mediante autómatas temporizados en entornos como **UPPAAL** (Behrmann et al., 2004). El modelado formal permite demostrar matemáticamente la ausencia de estados de interbloqueo (*deadlocks*) y garantizar que, ante cualquier retardo o pérdida de señal externa, el sistema transita de forma determinista hacia un estado de degradación segura que preserva la soberanía de control del maquinista.

---

### CAPÍTULO X: CONCLUSIONES SOBRE LA RESPONSABILIDAD DIRECTA POR OMISIÓN CRÍTICA
El nexo de causalidad jurídica en el siniestro de Urda no puede evaluarse bajo el prisma de la imprevisibilidad absoluta. En el derecho regulatorio del transporte ferroviario, los antecedentes documentados en sede parlamentaria (Senado de España, 2025) y en los registros hemerográficos previos (Diario de Sevilla, 2025) obligan a analizar una posible omisión en el control continuo del riesgo bajo los preceptos del Código Civil (BOE, 1889) y el Reglamento (UE) 2016/798 (Parlamento Europeo y Consejo de la Unión Europea, 2016b):
1. **Deber de Mitigación ante Riesgos Conocidos:** Al existir constancia pública de que las unidades experimentaban retardos prolongados en la recuperación lógica tras pérdidas de señal de tierra, los operadores y fabricantes debían aplicar el Método Común de Seguridad para la evaluación y valoración del riesgo (Comisión Europea, 2013), adoptando restricciones operativas cautelares hasta garantizar la subsanación del código.
2. **Concurrencia en la Cadena del Accidente:** Esta vulnerabilidad latente habría generado la obstrucción física prolongada en vía general, escenario que posteriormente se materializó en colisión tras la decisión humana del centro de control al autorizar el rebase del tren AVE trasero por el mismo cantón ocupado.

---

### CAPÍTULO XI: ANÁLISIS CINEMÁTICO FORENSE DE INEVITABILIDAD DE COLISIÓN A 40 KM/H
El análisis cinemático de espacio-tiempo demuestra matemáticamente que la inmovilización forzosa atribuida al bloqueo lógico constituye un factor determinante en la cadena causal del alcance en Urda:
1. **Ecuación de Movimiento en Conducción Visual:** Si la arquitectura embarcada hubiera preservado la soberanía humana y permitido a la maquinista emprender la marcha a la vista en modo degradado a la velocidad reglamentaria de $40\text{ km/h}$ ($11.11\text{ m/s}$) desde la notificación de las 08:41, la distancia recorrida ($s = v \cdot t$) durante los $780\text{ segundos}$ (13 minutos) de crisis habría alcanzado los **$8,665.8\text{ metros}$**.
2. **Evacuación del Cantón de Vía:** Al desplazarse **$8.66\text{ kilómetros}$** en marcha visual degradada, el convoy delantero habría liberado por completo el cantón de vía ocupado (cuya longitud habitual en alta velocidad oscila entre 4 y 6 kilómetros).
3. **Ruptura de la Geometría del Alcance:** Al despejar dicho tramo, los circuitos de vía habrían detectado la liberación del cantón y modificado el aspecto de las señales de protección posteriores. Bajo estas condiciones cinemáticas, el tren AVE trasero circulando a $200\text{ km/h}$ no habría coincidido espacialmente con el convoy delantero en ese punto, transformando el escenario de colisión en una detención controlada.

---

### CAPÍTULO XII: EL VECTOR DE RIESGO DE CIBERSEGURIDAD LÓGICA Y DIRECTIVA NIS 2
Más allá del fallo funcional accidental, la rigidez algorítmica descrita abre una brecha crítica de ciberseguridad industrial (*Security*) evaluable bajo la **Directiva (UE) 2022/2555 (NIS 2)** (Parlamento Europeo y Consejo de la Unión Europea, 2022), la especificación técnica ferroviaria **CLC/TS 50701:2021** (CENELEC, 2021), la norma de seguridad de componentes **IEC 62443-4-2:2019** (IEC, 2019) y las directrices de protección de sistemas de control industrial **NIST SP 800-82** y **NIST CSF 2.0** (National Institute of Standards and Technology [NIST], 2023, 2024):
1. **Vector de Ataque por Denegación de Servicio Físico (*Physical DoS*):** Como advierten los informes de ciberseguridad ferroviaria de la Agencia de la Unión Europea para la Ciberseguridad (European Union Agency for Cybersecurity [ENISA], 2023), la Estrategia de Ciberseguridad Ferroviaria de la ERA (ERA, 2022) y los entregables de investigación de *Shift2Rail* y *Europe's Rail Joint Undertaking* (Europe's Rail Joint Undertaking, 2023), la dependencia de enlaces inalámbricos expone al material rodante a interferencias intencionadas. Un actor hostil no requiere vulnerar el cifrado interno del bus del tren; le bastaría desplegar equipos de inhibición de radiofrecuencia (*jamming* o *spoofing*) sobre la señal GSM-R o FRMCS de la vía.
2. **El Software como Ejecutor Involuntario del Sabotaje:** Ante la pérdida inducida de portadora externa, el propio algoritmo del convoy ejecutaría el interbloqueo (**CWE-833**), entraría en bucle infinito (**CWE-835**) y bloquearía los frenos neumáticos (**CWE-617**), inhabilitando la respuesta humana en cabina y fijando un obstáculo de alto tonelaje en corredores críticos.

---

### CAPÍTULO XIII: EL SOBREAGOTAMIENTO Y ESTRÉS DE LAS INFRAESTRUCTURAS FRENTE A LA RIGIDEZ DEL SOFTWARE
Las líneas ferroviarias de alta velocidad soportan de manera inherente fatiga material, variaciones térmicas, desgaste de componentes y microcortes de tensión en la catenaria o portadoras de señal a lo largo de todo el año. Esta variabilidad física de la infraestructura constituye un parámetro previsible que los sistemas embarcados deben absorber sin colapsar.
1. **La Falacia de la Conectividad Continua Perfecta:** La hipótesis plantea que el error de diseño reside en programar una lógica industrial bajo la premisa idealizada de que la señal externa de tierra mantendrá una disponibilidad ininterrumpida.
2. **La Eliminación de la Redundancia Humana:** En lugar de gestionar las pérdidas de portadora mediante una degradación gradual controlada (*Graceful Degradation*), una arquitectura rígida que bloquea los frenos neumáticos cuando la infraestructura pierde comunicación impide al maquinista mitigar el incidente, transformando una incidencia ordinaria de señalización en una obstrucción crítica.

---

### CAPÍTULO XIV: ADIF COMO VÍCTIMA SISTÉMICA Y EL INCUMPLIMIENTO DEL REGLAMENTO DE CIRCULACIÓN
El análisis del marco operativo ferroviario sugiere que el Administrador de Infraestructuras Ferroviarias (**Adif**) actúa como receptor pasivo de un riesgo trasladado cuando circula por su red un material rodante incapaz de cumplir los procedimientos degradados reglamentarios:
1. **Quiebra Operativa del Reglamento de Circulación Ferroviaria (RCF):** El Real Decreto 664/2015 establece la obligación de continuar la marcha en modo degradado (Conducción Visual) a una velocidad máxima de $40\text{ km/h}$ tras la autorización correspondiente para evacuar cantones ocupados (BOE, 2015b). Si el software embarcado entra en interbloqueo (**CWE-833**) y mantiene purgados los frenos de forma irrevocable (**CWE-617**), impide materialmente al maquinista ejecutar la marcha a la vista exigida por la norma.
2. **Saturación Operativa y Factor Humano:** Obligado por el marco europeo de interoperabilidad a permitir el acceso de flotas homologadas, el administrador de infraestructuras asume el impacto operativo de las inmovilizaciones prolongadas. Los 13 minutos de bloqueo inamovible atribuidos a la unidad delantera habrían sometido a los operadores del Centro de Regulación y Control (CRC) a una elevada carga cognitiva y saturación de alarmas, contribuyendo al escenario de confusión logística previo a la autorización de rebase del convoy trasero.
3. **Equidad Regulatoria y Prevención:** La externalización de estos riesgos operativos y materiales hacia la infraestructura pública exige revisar los requisitos de homologación para garantizar que ningún material rodante utilice la red general sin disponer de mecanismos analógicos que aseguren su evacuación autónoma.

---

### CAPÍTULO XV: PROTOCOLO DE ACTUACIÓN Y PLAN DE MITIGACIÓN TECNOLÓGICA EN TRES FASES
Para erradicar este riesgo sistémico y garantizar el cumplimiento estricto del Artículo 64 de la Ley 38/2015 del Sector Ferroviario (BOE, 2015a) y el Reglamento (UE) 2016/798 (Parlamento Europeo y Consejo de la Unión Europea, 2016b), se propone un plan de mitigación estructurado en tres niveles:

1. **Parche de Código y Desacoplamiento Lógico (Fase de Software):** Revisión y actualización de la lógica del bus de datos *Train Communication Network* (TCN) y del protocolo TRDP. Ante una pérdida de señal externa o caída de sesión con el RBC de tierra, el sistema debe ejecutar un aislamiento asíncrono (*Graceful Degradation*) supervisado por temporizadores *watchdog*, pasando a un estado pasivo que evite el bucle infinito (**CWE-835**) y mantenga la tracción manual liberada para la conducción visual.
2. **Bypass Mecánico-Neumático Puro (Fase de Hardware):** Implementación física en cabina de una llave analógica de aislamiento neumático directo independiente de la Unidad de Control de Freno (BCU). Este actuador mecánico puro permitiría interrumpir el control electrónico sobre las electroválvulas de purga, cerrando el escape y permitiendo presurizar los $5.0\text{ bares}$ en la Tubería de Freno Automático (TFA) para liberar el convoy en situaciones de emergencia.
3. **Itinerario Procedimental de Notificación Ciudadana:** Tramitación escalonada de esta hipótesis técnica bajo el amparo del Artículo 259 de la Ley de Enjuiciamiento Criminal (BOE, 1882):
    * **Fase 1 (INCIBE-CERT):** Comunicación técnica al CERT nacional mediante el canal de divulgación coordinada de vulnerabilidades para evaluar el riesgo como un posible *Zero-Day por Diseño* y analizar los vectores de Denegación de Servicio Físico (*Physical DoS*) bajo la Directiva NIS 2.
    * **Fase 2 (AITAT):** Presentación formal de aportación ciudadana ante la Autoridad Administrativa Independiente para la Investigación Técnica de Accidentes e Incidentes de Transporte, solicitando la verificación en los registradores jurídicos (cajas negras) de la hipótesis de bloqueo lógico y del cálculo cinemático de los $8.66\text{ km}$.
    * **Fase 3 (Tribunal de Instancia):** Remisión documental ante la Plaza N.º 2 de la Sección de Instrucción del Tribunal de Instancia de Orgaz para su valoración en el marco de las Diligencias Previas penales, a fin de que los peritos oficiales auditen el comportamiento del software embarcado y el control previo de riesgos documentado.

---

### REFERENCIAS BIBLIOGRÁFICAS, NORMATIVAS Y TÉCNICAS (ESTÁNDAR APA 7.ª EDICIÓN)

#### Marco Normativo, Regulatorio y Agencias de Seguridad (Nacional y Europeo)
* Agencia Estatal Boletín Oficial del Estado. (1882). *Real Decreto de 14 de septiembre de 1882 por el que se aprueba la Ley de Enjuiciamiento Criminal* (Art. 259). Boletín Oficial del Estado, núm. 260. https://boe.es
* Agencia Estatal Boletín Oficial del Estado. (1889). *Real Decreto de 24 de julio de 1889 por el que se publica el Código Civil* (Art. 1902). Boletín Oficial del Estado, núm. 206. https://boe.es
* Agencia Estatal Boletín Oficial del Estado. (2015a). *Ley 38/2015, de 29 de septiembre, del sector ferroviario* (Art. 64). Boletín Oficial del Estado, núm. 234. https://boe.es
* Agencia Estatal Boletín Oficial del Estado. (2015b). *Real Decreto 664/2015, de 17 de julio, por el que se aprueba el Reglamento de Circulación Ferroviaria*. Boletín Oficial del Estado, núm. 171. https://boe.es
* Agencia Estatal de Seguridad Ferroviaria. (2023). *Guía para la autorización de puesta en el mercado de vehículos ferroviarios y supervisión de sistemas embarcados*. Ministerio de Transportes y Movilidad Sostenible. https://seguridadferroviaria.es
* Alves-Foss, J., Oman, P. W., Taylor, C., & Harrison, W. S. (2006). The MILS architecture for high-assurance embedded systems. *International Journal of Embedded Systems*, 2(3-4), 239–247. https://doi.org
* Comisión Europea. (2013). *Reglamento de Ejecución (UE) n.º 402/2013 de la Comisión, de 30 de abril de 2013, relativo a la adopción de un método común de seguridad para la evaluación y valoración del riesgo*. Diario Oficial de la Unión Europea, L 121/8. https://europa.eu
* Comisión Europea. (2018). *Reglamento de Ejecución (UE) 2018/545 de la Comisión, de 4 de abril de 2018, por el que se establecen las disposiciones prácticas relativas a la autorización de vehículos ferroviarios y al proceso de autorización de tipo de vehículos ferroviarios*. Diario Oficial de la Unión Europea, L 90/66. https://europa.eu
* European Union Agency for Railways. (2022). *Railway cybersecurity strategy and cybersecurity guidance for the railway sector*. Publications Office of the European Union. https://europa.eu
* European Union Agency for Railways. (2023a). *Technical Specifications for Interoperability (TSI) relating to the control-command and signalling subsystems (CCS TSI / ERTMS)*. Publications Office of the European Union. https://europa.eu
* European Union Agency for Railways. (2023b). *ERA System Safety Framework: Guide for safety management and human factors integration*. Publications Office of the European Union. https://europa.eu
* Parlamento Europeo y Consejo de la Unión Europea. (2016a). *Directiva (UE) 2016/797 del Parlamento Europeo y del Consejo, de 11 de mayo de 2016, sobre la interoperabilidad del sistema ferroviario dentro de la Unión Europea*. Diario Oficial de la Unión Europea, L 138/44. https://europa.eu
* Parlamento Europeo y Consejo de la Unión Europea. (2016b). *Reglamento (UE) 2016/798 del Parlamento Europeo y del Consejo, de 11 de mayo de 2016, sobre la seguridad ferroviaria*. Diario Oficial de la Unión Europea, L 138/102. https://europa.eu
* Parlamento Europeo y Consejo de la Unión Europea. (2022). *Directiva (UE) 2022/2555 del Parlamento Europeo y del Consejo, de 14 de diciembre de 2022, relativa a las medidas destinadas a garantizar un elevado nivel común de ciberseguridad en toda la Unión (Directiva NIS 2)*. Diario Oficial de la Unión Europea, L 333/80. https://europa.eu

#### Estándares Técnicos, Ciberseguridad Industrial y Verificación Formal
* Behrmann, G., David, A., & Larsen, K. G. (2004). A tutorial on UPPAAL. En M. Bernardo & F. Corradini (Eds.), *Formal methods for the design of real-time systems* (pp. 200–236). Springer. https://doi.org
* Comité Europeo de Normalización Electrotécnica. (2021). *Aplicaciones ferroviarias. Ciberseguridad* (Especificación Técnica CLC/TS 50701:2021). AENOR.
* Comité Europeo de Normalización Electrotécnica. (2023). *Aplicaciones ferroviarias. Requisitos para el desarrollo de software* (Norma EN 50716:2023). AENOR.
* European Union Agency for Cybersecurity. (2023). *ENISA railway cybersecurity: Good practices in cyber risk management*. ENISA. https://europa.eu
* Europe's Rail Joint Undertaking. (2023). *Cybersecurity deliverables and system architecture specifications for future rail systems (Shift2Rail / FP2-R2DATO)*. Unión Europea. https://europa.eu
* International Electrotechnical Commission. (2010). *Functional safety of electrical/electronic/programmable electronic safety-related systems* (Norma IEC 61508). IEC.
* International Electrotechnical Commission. (2015). *Electronic railway equipment – Train communication network (TCN) – Part 2-3: TCN communication profile (TRDP)* (Norma IEC 61375-2-3:2015). IEC.
* International Electrotechnical Commission. (2019). *Security for industrial automation and control systems – Part 4-2: Technical security requirements for IACS components* (Norma IEC 62443-4-2:2019). IEC.
* MITRE Corporation. (2024a). *CWE-835: Loop with Unreachable Exit Condition ('Infinite Loop')* [Estándar de debilidades de software]. Common Weakness Enumeration. https://cwe.mitre.org/data/definitions/835
* MITRE Corporation. (2024b). *CWE-617: Reachable Assertion* [Estándar de debilidades de software]. Common Weakness Enumeration. https://cwe.mitre.org/data/definitions/617
* MITRE Corporation. (2024c). *CWE-833: Deadlock* [Estándar de debilidades de software]. Common Weakness Enumeration. https://cwe.mitre.org/data/definitions/833
* National Institute of Standards and Technology. (2023). *Guide to operational technology (OT) security* (NIST Special Publication 800-82 Rev. 3). U.S. Department of Commerce. https://doi.org/10.6028/NIST.SP.800-82r3
* National Institute of Standards and Technology. (2024). *The NIST Cybersecurity Framework (CSF) 2.0* (NIST CSWP 29). U.S. Department of Commerce. https://doi.org/10.6028/NIST.CSWP.29

#### Fuentes Parlamentarias, Hemerográficas y de Acreditación
* Diario de Sevilla. (2025). *Incidencias de comunicación en la red de alta velocidad: Los trenes de nueva generación pierden la señal de tierra y tardan en reconectarse*. Grupo Joly.
* García Manzano, J. A. (2026). *Ciberseguridad-ferroviaria-Urda: La pérdida de soberanía humana en sistemas SIL 4* [Repositorio de investigación y verificación]. GitHub. https://github.com/917543/Ciberseguridad-ferroviaria-Urda
* Google Career Certificates. (2025). *Certificado de Ciberseguridad de Google (Analista de nivel inicial)* [Programa de 8 cursos: fundamentos de ciberseguridad, gestión de riesgos, seguridad de redes, Linux y SQL, gestión de activos y amenazas, detección y respuesta a incidentes, automatización con Python y preparación profesional]. Coursera / Google.
* Senado de España. (2025). *Diario de Sesiones de la Comisión de Transportes y Movilidad Sostenible: Comparecencia de los operadores ferroviarios sobre incidencias y tiempos de reconexión en la red de alta velocidad*. Cortes Generales.

---

### VALIDACIÓN DE AUTORÍA E INTEGRIDAD CRIPTOGRÁFICA
La autoría intelectual, fecha de consolidación e inalterabilidad del presente documento quedan certificadas digitalmente mediante el historial de confirmaciones (*commits*) y su correspondiente firma criptográfica **hash SHA** registrada en el repositorio público de control de versiones:  
`https://github.com/917543/Ciberseguridad-ferroviaria-Urda`

**Autor:** Jose A. García Manzano  
**Perfil:** Ciudadano Colaborador (Art. 259 LECrim) | Analista de Ciberseguridad (Nivel inicial) — Certificado por Google 
