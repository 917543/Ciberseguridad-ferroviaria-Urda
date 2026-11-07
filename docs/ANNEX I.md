# ANNEX I: EXECUTIVE SUMMARY REPORT ON INDUSTRIAL CYBERSECURITY

**DOCUMENT:** Identification of Software Weaknesses Applied to the Loss of Command and Pneumatic Pressure (Official CWE Mapping)  
**AUTHOR:** Jose A. García Manzano  
**TECHNICAL REVIEWER:** Claudio  
**LICENCE:** Creative Commons Attribution-ShareAlike 4.0 International (CC BY-SA 4.0)  

---

### I. OBJECT OF THE SUMMARY REPORT
This report condenses the technical argumentation of the thesis, translating the physical and pneumatic behavior of the Frecciarossa ETR 1000 train into the international taxonomy of industrial cybersecurity vulnerabilities (Common Weakness Enumeration - CWE) by MITRE. It demonstrates that the immobilization of the convoy was not a fortuitous mechanical breakdown, but the direct consequence of a logical design failure that entirely suppressed the human operator's control capacity over the brake pressure bus.

### II. VULNERABILITY MAPPING OF THE PRESSURE BUS AND CAB COMMANDS
The forensic analysis of the data bus freeze (TCN/MVB) and the physical bleeding of the Automatic Brake Pipe (TFA/TFG) following the loss of trackside carrier signals reveals the presence of three critical software weaknesses with direct physical impact:

* **CWE-833 (Deadlock / Interbloqueo):** When the trackside LZB system collapsed, the software execution thread managing external communications with Adif and the thread managing pneumatic brake release entered a circular deadlock condition (*Coffman lockup*). As the electronic "brain" became cyclically trapped waiting for non-existent network packets, it froze bus instructions and locked the pneumatic electrovalves in an open exhaust/purge position.
* **CWE-400 (Uncontrolled Resource Consumption / Consumo no Controlado de Recursos):** As a direct consequence of the infinite reconnection loop, the train's CPU experienced computation resource exhaustion (*starvation*). This triggered command starvation in the cab: physical air injection commands sent by the driver via the auxiliary levers were completely rejected and unattended by the logical system, as processing capacity was monopolized by the locked software.
* **CWE-617 (Reachable Assertion / Aserción Alcanzable):** The software contains an unhandled extreme shutdown condition: upon encountering an external connectivity value equal to zero, it executes an irrevocable panic/stop routine that purges the 5 bars from the brake pipe. When this logical assertion was automatically triggered by Adif's trackside network cut, the software physically locked the pneumatic electrovalves open, preventing any subsequent instruction or crew action from halting the exhaust of air, thereby consolidating an immovable obstacle on the main track.

### III. PROVEN FACTS AND DYNAMIC ASYMMETRY (THE CONTROL GROUP)
The operational behavior of the AVE train (Renfe) acts as the expert control group. The AVE's software lacked these deadlock, resource exhaustion, and reachable assertion flaws: it isolated the lost trackside signal, performed graceful degradation, and restored 100% of physical command to the driver. Conversely, the new operator's train (Iryo / ETR 1000), afflicted by the described flaws (CWE-833, CWE-400, and CWE-617), collapsed cab operability to 0%, materially preventing the re-injection of the 5 bars of nominal pressure required to release the wheels.

### IV. THE VIOLATED SAFETY ENGINEERING PRINCIPLE
Industrial systems with a SIL 4 safety integrity level are strictly forbidden by design from allowing automation to override the analog relief controls of an authorized operator. The existence of these software flaws (CWE) violates the principle of resilience and Article 64 of the Spanish Railway Sector Act (Ley del Sector Ferroviario), by commercializing a rolling stock vehicle that lacks basic operational survivability against standard trackside network dropouts whose data stability cannot be guaranteed 365 days a year.

### V. CONCLUSIONS ON DIRECT LIABILITY BY OMISSION
1. **Material Cause (Software):** Systemic software design flaw by the manufacturer, which prioritized software veto and deadlock over pilot sovereignty.
2. **Penal Liability by Conscious Omission:** Having recorded evidence in technical audits and parliamentary records since 2025 that the fleet suffered from these specific weaknesses (CWE-833, CWE-400, and CWE-617) resulting in pressure bus lockups, operating companies and regulatory authorities (AESF) had a strict legal obligation to halt commercial service on that line until a software patch or a pure mechanical cut-off switch was installed in the cab. Maintaining commercial operation with full knowledge of this recurring structural flaw constitutes the core of liability by conscious omission in the disaster.

