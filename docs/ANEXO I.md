# ANEXO I: INFORME RESUMEN EJECUTIVO DE CIBERSEGURIDAD INDUSTRIAL

  
**DOCUMENTO:** Identificación de Debilidades de Software Aplicadas a la Pérdida de Comandancia y Presión Neumática (Mapeo CWE Oficial)
**AUTOR:** Jose A. García Manzano  
**REVISOR TÉCNICO:** Claudio  
**LICENCIA:** Creative Commons Atribución-CompartirIgual 4.0 Internacional (CC BY-SA 4.0)

---

### I. OBJETO DEL INFORME RESUMEN
Este informe condensa la argumentación técnica de la tesis aportada, traduciendo el comportamiento físico y neumático del tren Frecciarossa ETR 1000 a la taxonomía internacional de vulnerabilidades de ciberseguridad industrial (CWE) de MITRE. Se demuestra que la inmovilización del convoy no fue una avería fortuita, sino la consecuencia de un fallo de diseño lógico que suprimió por completo la capacidad de control del operador humano sobre el bus de presión de los frenos.

### II. MAPEO DE VULNERABILIDADES DEL BUS DE PRESIÓN Y MANDOS DE CABINA
El análisis del bloqueo del bus de datos (TCN/MVB) y el vaciado físico de la Tubería de Freno Automático (TFA) tras perder la señal de tierra revela la presencia de tres debilidades de software críticas de impacto físico directo:

* **CWE-833 (Deadlock / Interbloqueo):** Al caer el sistema LZB de la vía, el hilo de ejecución informático encargado de gestionar la comunicación externa con Adif y el hilo encargado de la liberación neumática de los frenos entraron en una condición de interbloqueo circular (*deadlock*). Al quedarse el "cerebro" electrónico atrapado de forma cíclica esperando datos de red que no existían, congeló las instrucciones del bus y bloqueó las electroválvulas neumáticas en posición de escape abierta.
* **CWE-400 (Uncontrolled Resource Consumption / Consumo no Controlado de Recursos):** Como consecuencia directa del bucle infinito de reconexión, la CPU del tren experimentó una saturación por consumo descontrolado de recursos de computación (*resource exhaustion*). Esto provocó un fenómeno de inanición de comandos (*starvation*) en la cabina: las órdenes físicas de inyección de aire enviadas por la maquinista a través de las palancas auxiliares fueron completamente descartadas y desatendidas por el sistema lógico, al estar la capacidad de procesamiento monopolizada por el software bloqueado.
* **CWE-617 (Reachable Assertion / Aserción Alcanzable):** El código contiene una condición de parada extrema invulnerable: ante un valor de conectividad externa igual a cero, se ejecuta una rutina de parada irrevocable que purga los 5 bares de la tubería de freno. Al alcanzarse de forma automática esta aserción lógica por el corte de red de Adif, el software bloqueó físicamente las electroválvulas neumáticas imposibilitando que ninguna instrucción posterior o acción de los tripulantes mitigara el vaciado de aire, consolidando el obstáculo inamovible en la vía general.

### III. HECHOS PROBADOS Y ASIMETRÍA (EL GRUPO DE CONTROL)
El comportamiento del tren AVE (Renfe) actúa como el grupo de control pericial. El software del AVE carecía de estas debilidades de interbloqueo y saturación de recursos: aisló la pérdida de señal y restauró el 100% de la comandancia física del maquinista. El tren de los nuevos operadores, al verse afectado por los fallos de lógica descritos (CWE-833 y CWE-400), redujo la operatividad de la cabina al 0%, impidiendo materialmente volver a meter los 5 bares de presión para liberar las ruedas.

### IV. EL PRINCIPIO DE INGENIERÍA VIOLADO
Los sistemas industriales con nivel de integridad SIL 4 tienen prohibido por diseño permitir que la automatización anule los mandos de socorro analógicos del operador habilitado. La presencia de estos errores de software (CWE) vulnera el principio de resiliencia y el artículo 64 de la Ley del Sector Ferroviario, al comercializar un vehículo que carece de la capacidad de supervivencia operativa básica ante indisponibilidades comunes de la red de tierra cuya estabilidad de datos no se puede asegurar los 365 días del año.

### V. CONCLUSIONES DE RESPONSABILIDAD DIRECTA POR OMISIÓN
1. **Causa Material (Software):** El fallo de diseño del software del fabricante, que anteponía el veto informático y el bloqueo por *deadlock* a la soberanía del piloto.
2. **Causa Penal por Omisión:** Al constatar documentalmente desde 2025 que la flota sufría estas debilidades específicas de interbloqueo (CWE-833) y bloqueo del bus de presión por saturación (CWE-400), los operadores y las autoridades reguladoras (AESF) tenían la obligación legal de paralizar de inmediato su circulación hasta la implantación de un parche de código o una llave de corte mecánico puro en cabina. Mantener los trenes en explotación comercial a sabiendas de este fallo estructural constituye el núcleo de la responsabilidad por omisión en la catástrofe.