# Assumptions

This document records the assumptions used to construct the **DMZ-to-LAN APM Bridge** security assessment. The system is explicitly treated as an **anonymized / simulated enterprise architecture**; no proprietary organizational details, real IP addresses, hostnames, credentials, customer data, or confidential implementation details are assumed.

## 1. Network and Trust-Boundary Assumptions

1. **Unidirectional DMZ-to-LAN telemetry flow**  
   The NGFW / data-diode boundary is assumed to support a strict DMZ-to-LAN PUSH model. Internal LAN systems do not need to initiate a reverse TCP connection to receive telemetry.

2. **Strict firewall enforcement**  
   The security boundary is assumed to permit only the intended telemetry path over HTTPS / TLS 1.3 on Port 443. Any bidirectional rule or unintended management path is treated as a configuration weakness for the lateral-pivot threat scenario.

3. **Trust zones are meaningful security boundaries**  
   The DMZ is treated as semi-trusted / exposed, the firewall conduit as the enforcement boundary, and the internal core LAN as a trusted zone. The analysis does not assume that crossing into the LAN automatically grants unrestricted access.

4. **IP allow-listing is available**  
   The ingestion path can enforce source IP restrictions for authorized DMZ APM probes.

## 2. Agent and Endpoint Assumptions

5. **DMZ APM probes run with least privilege**  
   Probe agents are assumed to operate as lightweight, non-privileged services without local administrator/root privileges.

6. **DMZ applications may be compromised**  
   The threat model intentionally allows a public-facing DMZ application or host to become compromised. This is the starting condition for the lateral-pivot scenario.

7. **The APM probe connection is an attack-relevant asset**  
   A compromised DMZ host is assumed to be able to discover or interact with its local APM probe process and associated network connectivity, subject to the controls described in the report.

## 3. Telemetry and Application Assumptions

8. **Telemetry has a defined schema**  
   Metrics are exchanged as JSON/Protobuf-style telemetry objects and can therefore be validated against a strict schema before downstream processing.

9. **Telemetry may contain sensitive trace information**  
   Transaction trace headers may contain URL paths, correlation IDs, user-agent strings, and other information that could expose PII or internal topology. The design therefore assumes PII scanning and redaction before storage.

10. **Input validation occurs before business processing**  
    The ingestion service is assumed to validate payload structure before passing telemetry to the APM Processing Engine.

11. **Malformed telemetry is potentially hostile**  
    The threat model treats telemetry as untrusted input rather than inherently trustworthy monitoring data. Parser/input-validation weaknesses are therefore considered capable of producing injection or RCE impact.

## 4. Cryptography and Identity Assumptions

12. **TLS 1.3 / mTLS is technically deployable**  
    The architecture assumes that DMZ probes can authenticate to the internal ingestion service using client certificates and TLS 1.3.

13. **Certificate lifecycle management exists**  
    PKI/KMS/HSM capabilities are assumed to be available for certificate/key storage and rotation. The report specifies automated 90-day key rotation as the target policy.

14. **Strong cryptographic algorithms are available**  
    Weak TLS cipher suites are assumed to be disabled. The proposed design uses AES-256-GCM or ChaCha20-Poly1305 for TLS and HMAC-SHA256 for payload integrity verification.

15. **Encryption at rest is supported**  
    Telemetry storage is assumed to support AES-256-based encryption and RBAC.

## 5. Availability and Operations Assumptions

16. **Ingestion capacity can scale**  
    Internal ingestion nodes are assumed to have sufficient CPU/RAM overhead and the ability to scale to process real-time mTLS decryption, schema validation, and PII sanitization without unacceptable packet loss.

17. **Asynchronous buffering is available**  
    A queue/buffer can be placed between ingestion and processing to absorb telemetry bursts and reduce the impact of transient downstream failures.

18. **Security and operational logs are retained**  
    Ingestion logs, failed mTLS handshakes, and FIM events can be stored immutably and forwarded to a SIEM. The report assumes a minimum 90-day retention period for security audit logs.

19. **Operational users are authenticated and authorized**  
    SRE/NOC operators, security analysts, and application owners access dashboards through authenticated HTTPS sessions with role-based access controls.

## 6. Data and Compliance Assumptions

20. **Performance telemetry is operationally important**  
    Availability, latency, throughput, CPU/memory utilisation, and related metrics are considered important for monitoring customer-facing applications and SLA compliance.

21. **System metadata is restricted/confidential**  
    Hostnames, OS versions, agent IDs, and internal IP addresses are treated as restricted information even though they are represented using safe placeholders in the assignment.

22. **Trace headers may create privacy exposure**  
    Transaction trace headers are treated as confidential and potentially subject to GDPR/privacy requirements.

23. **GDPR / ISO 27001 are used as architectural compliance references**  
    These are treated as design/compliance considerations in the simulated architecture, not as evidence of an actual organization's certified compliance status.

## 7. Assessment and Evidence Assumptions

24. **The report is primarily an architecture/security design assessment**  
    The submitted PDF documents the proposed architecture, threat model, controls, risk analysis, and assumptions. It does not establish that the proposed controls have been deployed in a production environment.

25. **Evidence placeholders distinguish design from implementation**  
    Where screenshots would normally demonstrate execution, testing, repository state, rendered diagrams, or tool output, the evidence folder uses placeholders rather than claiming that those tests were performed.

26. **PlantUML is the authoritative diagram source**  
    Diagram evidence should be generated from the version-controlled `.puml` files in the repository rather than from manually redrawn diagrams.

27. **CVSS scores represent the modeled vulnerabilities**  
    The CVSS values in the report are treated as risk-quantification outputs for the simulated threat scenarios. They should not be interpreted as confirmed production vulnerability findings.

## 8. Confidentiality Boundary

All examples, hostnames, IP addresses, vendor details, and security findings are assumed to be abstracted or simulated. No evidence screenshot should reveal real internal infrastructure, credentials, tokens, customer information, or unpublished security findings.
