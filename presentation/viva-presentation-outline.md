Viva Presentation Outline: DMZ-to-LAN APM Bridge
Slide 1: Title
Title: Security Architecture Evaluation: DMZ-to-LAN APM Bridge
Course: Advanced Cyber Security (SS ZG681 / SE ZG681)[cite: 2]
Presenters: Saptarsi Roy & Girish Amrutesh Joshi
System Declaration: Anonymized / Simulated Enterprise Architecture[cite: 2]
Slide 2: System Overview & Business Context
Business Purpose: Centralizing real-time application health, latency, and SLA compliance metrics from DMZ hosts to core LAN databases.
Core Components: DMZ Probe Agents, Firewall Conduit (Port 443), APM Ingestion Service, Processing Engine, Telemetry Storage.
Primary Risk: Monitoring conduits acting as a lateral movement pathway from exposed DMZ hosts into internal networks.
Slide 3: C4 Architecture Model (Context & Containers)
C4 Context: Shows SRE/NOC teams, web application endpoints, and the central APM Bridge.
C4 Container: Highlights trust boundaries (Internet-to-DMZ and DMZ-to-LAN) and HTTPS/TLS 1.3 push mechanics.
Trust Isolation: Unidirectional data push boundary preventing internal LAN probing from DMZ nodes.
Slide 4: Data Classification & CIA Impact
Metrics & Metadata: Classified as Internal/Restricted; stored in encrypted time-series DBs.
Trace Headers: Classified as Confidential due to GDPR risks if user PII is captured.
CIA Impact: High Integrity (preventing alert manipulation), Medium Availability, Low-Med Confidentiality.
Slide 5: Threat Scenario 1 — Lateral Pivot Attack
Attack Vector: Web vulnerability exploit on DMZ host -> Agent Hijack -> Tunnel through permissive firewall.
Root Cause: Misconfigured bi-directional firewall rules across monitoring ports.
Impact: Full compromise of internal APM servers and lateral movement across core LAN stores.
Slide 6: Threat Scenario 2 — Malicious Telemetry Injection
Attack Vector: Payload injection (Log4j/RCE) embedded inside transaction trace headers.
Root Cause: Absence of schema validation and input sanitization at the ingestion layer.
Impact: Arbitrary Remote Code Execution (RCE) on ingestion nodes and telemetry database corruption.
Slide 7: Defense-in-Depth Architecture Design
Layer 1 (Network): Unidirectional Data Diode / NGFW PUSH policy on Port 443.
Layer 2 (Application): Mutual TLS (mTLS) 1.3 + Schema Validation + Regex PII Scrubbing Module.
Layer 3 (Admin): Least privilege agent execution, RBAC, and File Integrity Monitoring (FIM).
Slide 8: CVSS v3.1 Risk Quantification & Gap Analysis
Scenario 1 Rating: CVSS:3.1/AV:N/AC:L/PR:N/UI:N/S:C/C:H/I:H/A:H (10.0 Critical).
Scenario 2 Rating: CVSS:3.1/AV:N/AC:L/PR:L/UI:N/S:U/C:H/I:H/A:H (8.8 High).
Gap Summary: Transitioning from single-ended TLS and plain parsing to mTLS and schema-enforced ingestion.
Slide 9: Remediation Roadmap
Immediate (Days 1–7): Hardening firewall rules for DMZ-to-LAN PUSH only.
Medium-Term (Days 8–20): Deploying mTLS certificates and JSON schema validation modules.
Long-Term (Days 21–30+): Integrating automated PII scrubbing and Zero-Trust data governance.
Slide 10: Architectural Reflection & Trade-offs
Key Lesson: Observability pipelines are high-value targets that require zero-trust perimeter controls.
Trade-off: Unidirectional network policies maximize boundary security but prevent direct remote agent management from the LAN.
Final Takeaway: Layered input validation and strict mTLS turn a vulnerable monitoring bridge into a resilient asset.

