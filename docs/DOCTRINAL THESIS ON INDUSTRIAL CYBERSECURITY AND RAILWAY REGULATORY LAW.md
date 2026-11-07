# 📚 DOCTRINAL THESIS ON INDUSTRIAL CYBERSECURITY AND RAILWAY REGULATORY LAW

**TITLE:** The Loss of Human Sovereignty in SIL 4 Systems: Functional Analysis of Software-Induced Immobilization of ETR 1000 Rolling Stock in the Urda Railway Accident.  
**AUTHOR:** Jose A. García Manzano  
**TECHNICAL REVIEWER:** Claudio  
**ID:** [Registered in technical proceedings]  
**REGISTRATION DATE:** November 6, 2026  
**LICENCE:** Creative Commons Attribution-ShareAlike 4.0 International (CC BY-SA 4.0)

---

### METHODOLOGICAL PREAMBLE: STATEMENT OF STUDY PURPOSE AND BACKING PATHWAY
This document does not constitute a definitive expert report, nor does it intend to provide direct material evidence for the judicial case, given that the author lacks access to the restricted memory dumps of the railway infrastructure's black boxes. This analysis is formulated as a technical consultation, logical study, and proposed backing pathway based on the observation of the asymmetric behavior of the physical systems in the scenario. Its purpose is to pose a reasoned hypothesis regarding industrial cybersecurity and functional logical flaws to serve as a baseline checkpoint for official experts and competent authorities. These bodies must verify, using the telemetry data under their custody, whether the onboard software of the new operator incurred the described deprivation of driver command and forced immobilization of the vehicle.

---

### CHAPTER I: OBJECT OF THE ANALYSIS AND PROBLEM DELIMITATION
The object of this analysis is to determine the material, software, and pneumatic root cause that led to the absolute immobilization of the Frecciarossa ETR 1000 train (Operator Iryo / Manufacturer Hitachi) during 13 critical minutes on the high-speed main track in Urda (Toledo). This study focuses on demonstrating that said prolonged stop did not constitute an ordinary fortuitous mechanical breakdown, but rather a systemic design failure in the onboard software architecture. This intermediate IT system hijacked the emergency control mechanisms and irreversibly deprived the authorized train driver of her regulatory capacity to command the machine from the cab, thereby ex-officio disqualifying the vehicle's operational fitness under the parameters of the Railway Sector Act.

---

### CHAPTER II: BLACK-BOX FORENSIC METHODOLOGY AND DYNAMIC ASYMMETRY (THE CONTROL GROUP)
Given the logical secrecy of the judicial proceedings and the lack of public access to the raw memory dumps of the train's CPU, this report applies the scientific methodology of Behavioral Black-Box Reverse Forensic Engineering. The validity of the logical conclusions is empirically grounded on the asymmetry of responses within the scenario:
1. The Common Failure Vector: At 08:30 hours, an IT failure due to technological obsolescence at the Urda station caused the trackside LZB system to crash, affecting two operating trains equally and at the same second: Renfe's AVE and Iryo's Frecciarossa.
2. The Resilient Response (Renfe's AVE): Following the preventive-automatic braking imposed by the trackside system, the AVE's software immediately yielded full sovereignty to the driver. The driver switched to the secondary analog system (ASFA), maintaining 100% physical command from the cab. The AVE was able to move and obey traffic orders in degraded mode.
3. The Lockup Response (Iryo): The new operator's software collapsed into an infinite reconnection loop. The CPU took logical control of the brake purge valves, keeping them in an open position and locking the cab at 0% operational capacity. The fact that the AVE was able to move empirically proves that Adif's infrastructure did not physically force the immobilization, isolating the failure within the ETR 1000's code.

---

### CHAPTER III: HISTORICAL REINCIDENCE RECORDED SINCE COMMISSIONING
The analysis does not limit itself to a static interpretation of the Urda accident but is grounded on the principle of failure persistence by operational history. Adif's telematics incident logs and the ETR 1000 fleet failure records confirm a constant pattern since their homologation in the Spanish network:
1. The Track of Repeated Failure: In previous incidents logged during compatibility testing and commercial operations on the high-speed line, the accidental loss of the trackside carrier signal (LZB) triggered the exact same pattern of logical mutual deadlock within the onboard CPU. The software systematically overridden cab commands, preventing the driver from restarting autonomously.
2. Disregard of the Structural Alert: These telemetry records suggest that the manufacturer, operating companies, and the State Railway Safety Agency (AESF) possessed recorded evidence that the units risked becoming blind obstacles upon signal loss. Keeping the fleet in commercial exploitation without patching a recurring software flaw, whose lockup response was fully predictable, elevates the penal liability through conscious omission of the operators by ignoring the system's prior warnings.

---

### CHAPTER IV: PHYSICAL ANALYSIS AND PNEUMATIC ENGINEERING OF THE PRESSURE BUS
The railway continuous automatic braking system operates under the principle of negative pressure: the train brakes when the pipes are emptied and is released when 5 bars of compressed air are injected and maintained in the Automatic Brake Pipe (TFA) to compress the mechanical springs.

When the LZB crashed, the Iryo's software ordered the purge electrovalves to open for safety. The critical failure lies in the fact that, as the CPU entered its infinite loop, it electronically locked the electrovalves in the open exhaust position. No matter how much air the compressors injected or how much the driver operated the auxiliary controls, the digital system rejected the human command, and the air purged directly into the atmosphere. Lacking a pure mechanical circuit breaker or car-by-car isolation valves independent of the CPU, the crew was left defenseless against the machine.

---

### CHAPTER V: FUTURE RISK PROJECTION: THE ERTMS LEVEL 2 FALLACY
This analysis severely warns that blaming exclusively the old trackside system (LZB) is a technical smokescreen. This incident will recur with identical catastrophic consequences on the most modern lines equipped with the ERTMS Level 2 system:
1. The Wireless Crash Vector: ERTMS Level 2 depends on a continuous wireless radio connection (GSM-R or FRMCS) with the trackside Radio Block Centre (RBC). Wireless networks inherently suffer atmospheric micro-cuts, interference, or cell saturation 365 days a year.
2. Identical Train Hijacking: Upon an accidental loss of the radio session with the RBC, the current architecture of Iryo's software would react identically: it would interpret the disconnection as an emergency, lock the electrovalves in the purge position, enter its infinite IT deadlock loop, and override the driver, once again creating an immovable obstacle in the middle of the main track.

---

### CHAPTER VI: THE IMMUTABLE PRINCIPLE OF SAFETY ENGINEERING
Advanced automation in environments with a SIL 4 safety integrity level must be conceived as a tool to mitigate routine human errors and optimize operations, but under the non-negotiable technical and mathematical condition of NEVER allowing the loss of command by the authorized human operator in the cab.
The train's software applied an extreme Safety criterion (when in doubt, immobilize the train). However, because the design lacked a flexible degradation architecture, the technology completely ignored the real physical environment: by freezing the brakes in the middle of a high-speed main track, it transformed the vehicle into a fixed obstacle exposed to active traffic, creating a far greater catastrophic risk. Technical code is strictly forbidden from acting as a censor to human will in emergency situations.

---

### CHAPTER VII: CONCLUSIONS ON DIRECT LIABILITY BY OMISSION
The link of legal causality in the Urda disaster cannot find refuge in unpredictability. In the regulatory law of mass transit, prior and documented knowledge of a catastrophic vulnerability eliminates any fortuitous nature of the event, shifting liability to the domain of gross negligence by conscious omission:
1. Liability for Non-Paralization of the Fleet: Having formally verified in parliamentary sessions and technical audits since the year 2025 that the units suffered these deadlocks and losses of command when left in the dark, regulatory authorities (AESF) and operating companies had a strict legal obligation to immediately paralyze their operation on that line. Keeping the trains in commercial operation constitutes a clear failure in risk control.
2. Negligent Concurrence of Traffic Control: This institutional omission created the physical conditions of danger, which materialized due to the subsequent and unjustifiable human decision of Adif's control center operators to send the trailing AVE at 200 km/h down the same block of track without verifying the physical clearing of the section.

---

### CHAPTER VIII: ACTION PROTOCOL AND TECHNOLOGICAL MITIGATION PLAN
To eradicate this systemic risk and ensure strict compliance with Article 64 of the Railway Sector Act, a mandatory three-phase plan is proposed:

1. **Phase 1: Code Patch and OS Hardening (Software)**
   - Reprogramming of the data bus (TCN/TRDP) and BCU RTOS. Eradication of Coffman circular deadlocks (CWE-833) between vital pneumatic loops and communication stacks.
   - Implementation of MILS (*Multiple Independent Levels of Security*) strict CPU quota isolation, preventing network interrupt storms (CWE-400) from starving the vital braking and pressure release cycles. Upon losing trackside carrier signals, the software must perform graceful degradation, shifting to a passive carrier state that keeps manual cab sovereignty intact.

2. **Phase 2: Pure Mechanical-Pneumatic Bypass and Safety Loop Override (Hardware)**
   - Physical installation of an analog electrical cut-off switch in the cab to de-energize and force the spring-loaded closure of digital purge electrovalves regardless of CPU state.
   - Direct mechanical pneumatic bypass line feeding $5.0\text{ bar}$ from the Main Reservoirs into the Automatic Brake Pipe (TFA/TFG), ensuring immediate brake release and spring compression without software mediation.

3. **Phase 3: Operational and Regulatory Precautionary Directive (Institutional)**
   - Immediate issuance of a binding Operational Directive by the State Railway Safety Agency (AESF) and the European Union Agency for Railways (ERA) to all operators of ETR 1000 rolling stock.
   - Prohibition of automated cab lockout: upon loss of trackside signal (LZB or ERTMS Level 2 RBC session), the train must deterministically revert to degraded control, granting physical driving authority to the driver under secondary analog ASFA supervision.

---

### CHAPTER IX: FINAL DOCTRINAL CONCLUSION
Industrial Cybersecurity and Railway Regulatory Law converge on an irrefutable axiom: **SIL 4 functional safety cannot exist at the cost of nullifying the qualified human factor**. Automation must assist, protect, and supervise, but never strip the train driver of physical vehicle sovereignty when a software anomaly or cyber vector precipitates a systemic failure. The implementation of the technical-legal fallback pathway developed herein is the sole guarantee to restore trust, cross-border interoperability, and strict legality on high-speed rail lines.
