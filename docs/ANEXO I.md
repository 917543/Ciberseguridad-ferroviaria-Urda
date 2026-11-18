# ANEXO I: RESUMEN EJECUTIVO DE CIBERSEGURIDAD INDUSTRIAL Y MAPEO MITRE CWE

**PROYECTO:** Ciberseguridad-ferroviaria-Urda — Análisis de la Presunta Pérdida de Soberanía Humana en Sistemas SIL 4.  
**AUTOR:** Jose A. García Manzano  
**PERFIL:** Ciudadano Colaborador con la Justicia (Art. 259 LECrim) | Analista de Ciberseguridad de nivel inicial (Certificado por Google - Programa de 8 cursos).  
**NATURALEZA:** Resumen técnico ejecutivo e hipótesis lógica sujeta a verificación pericial oficial (cajas negras ferroviarias).  
**FECHA DE ACTUALIZACIÓN:** 18 de noviembre de 2026  

---

### I. SÍNTESIS DE LA HIPÓTESIS DE FALLO LÓGICO Y NEUMÁTICO
El presente resumen sintetiza la hipótesis técnico-funcional planteada sobre la inmovilización prolongada del material rodante ETR 1000 durante 13 minutos críticos en Urda (Toledo). Se propone verificar ante los registradores jurídicos oficiales si una rigidez en la arquitectura de software embarcada (*Train Communication Network* - TCN / protocolo TRDP) impidió la transición hacia un modo de degradación segura tras la caída de la portadora LZB de tierra.

Bajo esta hipótesis, el bloqueo lógico de la Unidad de Control de Freno (*Brake Control Unit* - BCU) habría mantenido las electroválvulas neumáticas retenidas en posición de escape abierta, purgando la Tubería de Freno Automático (TFA) e impidiendo alcanzar los $5.0\text{ bares}$ necesarios para liberar los frenos y emprender la marcha a la vista reglamentaria a $40\text{ km/h}$ (lo que habría permitido evacuar $8.66\text{ km}$ fuera del cantón ocupado).

---

### II. MAPEO TÉCNICO DE DEBILIDADES DE SOFTWARE (MITRE CWE)
El comportamiento observado en el bus de datos integrado sugiere la posible concurrencia de tres debilidades específicas de nivel *Base* tipificadas por MITRE Corporation:

1. **CWE-833 (*Deadlock* / Interbloqueo):** Dependencia circular mutua entre los hilos de ejecución del Sistema Operativo en Tiempo Real (*RTOS*) encargados de gestionar la comunicación externa con la infraestructura y la liberación neumática de los frenos, congelando el estado de las electroválvulas.
2. **CWE-835 (*Loop with Unreachable Exit Condition - 'Infinite Loop'* / Bucle Infinito):** Rutina de reconexión automática sin condición de salida alcanzable tras la pérdida de señal, monopolizando los ciclos de cómputo de la CPU, eludiendo los temporizadores de vigilancia (*watchdogs*) e induciendo inanición de comandos (*starvation*) sobre los mandos físicos de cabina.
3. **CWE-617 (*Reachable Assertion* / Aserción Alcanzable):** Condición algorítmica extrema que ejecuta una parada irrevocable vaciando la TFA al detectar portadora externa igual a cero, bloqueando cualquier mitigación manual posterior.

---

### III. VECTORES DE RIESGO Y MITIGACIÓN PROPUESTA
* **Co-ingeniería Safety-Security (Directiva NIS 2 / CLC/TS 50701):** La dependencia de enlaces inalámbricos en entornos ERTMS Nivel 2 (GSM-R / FRMCS) expone esta rigidez lógica a ataques de Denegación de Servicio Físico (*Physical DoS*) mediante inhibición de radiofrecuencia (*jamming* o *spoofing*).
* **Aislamiento MILS y Verificación Formal:** Se plantea la necesidad de aplicar arquitecturas de seguridad multinivel (*MILS*) y verificación formal mediante autómatas temporizados (**UPPAAL**) para garantizar la ausencia de *deadlocks*.
* **Salvaguarda Analógica:** Instalación física en cabina de una llave analógica de corte neumático directo independiente de la BCU para preservar la soberanía humana en emergencias.

---
**Validación de Integridad:** Autoría y fecha certificadas mediante firma criptográfica **hash SHA** en el repositorio `https://github.com`.
