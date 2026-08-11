# Evidence / Screenshot Placeholders

This file defines the evidence that should be added to the `evidence/` folder when screenshots or rendered artifacts are available.

The assignment handbook requires the GitHub repository to contain reproducible diagram sources and expects traceability between the report and diagrams. It does **not** require fabricated screenshots. Therefore, placeholders below are intentionally marked as pending where actual execution evidence has not been captured.

## Evidence Status

| ID | Evidence | Status | Suggested File |
|---|---|---|---|
| E01 | Repository structure showing `report/`, `diagrams/`, `risk/`, `evidence/`, `scripts/` | Pending | `e01-repository-structure.png` |
| E02 | C4 Level 1 — System Context rendered from PlantUML | Pending | `e02-c4-context.png` |
| E03 | C4 Level 2 — Container Diagram rendered from PlantUML | Pending | `e03-c4-container.png` |
| E04 | C4 Level 3 — Component Diagram rendered from PlantUML | Pending | `e04-c4-component.png` |
| E05 | Threat Scenario 1 — Lateral Pivot Attack Graph rendered | Pending | `e05-attack-graph-lateral-pivot.png` |
| E06 | Threat Scenario 2 — Malicious Telemetry Payload Injection Attack Graph rendered | Pending | `e06-attack-graph-payload-injection.png` |
| E07 | Data-flow mapping / trust-boundary view | Pending | `e07-data-flow.png` |
| E08 | Data classification matrix | Pending | `e08-data-classification.png` |
| E09 | CVSS calculation / scoring evidence for Vulnerability 1 | Pending | `e09-cvss-vuln-1.png` |
| E10 | CVSS calculation / scoring evidence for Vulnerability 2 | Pending | `e10-cvss-vuln-2.png` |
| E11 | Evidence of PlantUML source validation/rendering | Pending | `e11-plantuml-validation.png` |
| E12 | Evidence of security-control/test validation, if implemented | Not performed / add only if available | `e12-security-test-results.png` |

## E01 — Repository Structure

**Purpose:** Demonstrate that the submitted repository follows the expected GitHub structure and contains the report, diagrams, risk material, scripts, and evidence.

**Capture:** Repository root showing the relevant folders and files.

**Do not capture:** Credentials, personal tokens, private repositories, internal URLs, or confidential corporate paths.

**Placeholder:**  
`[INSERT SCREENSHOT: repository root and required assignment folders]`

---

## E02 — C4 Level 1: System Context

**Purpose:** Demonstrate the system context, external DMZ application, operational/security users, and major interactions.

**Expected content:** SRE/NOC Operators, Security Analysts, Application Owners, DMZ Web Applications, and the DMZ-to-LAN APM Bridge.

**Placeholder:**  
`[INSERT SCREENSHOT: rendered c4-context.puml]`

---

## E03 — C4 Level 2: Container Diagram

**Purpose:** Demonstrate the major runtime containers and the DMZ / firewall / internal LAN security boundaries.

**Expected content:** DMZ APM Probe Agent, NGFW/Data Diode Conduit, APM Ingestion Service, APM Processing Engine, Telemetry Storage, and Operational UI.

**Placeholder:**  
`[INSERT SCREENSHOT: rendered c4-container.puml]`

---

## E04 — C4 Level 3: Component Diagram

**Purpose:** Demonstrate the security-sensitive ingestion pipeline.

**Expected content:** mTLS Endpoint Listener, Rate Limiter & IP Whitelisting, Schema & Input Validator, PII Redaction & Sanitizer, and Ingestion Buffer Forwarder.

**Placeholder:**  
`[INSERT SCREENSHOT: rendered c4-component.puml]`

---

## E05 — Threat Scenario 1: Lateral Pivot

**Purpose:** Demonstrate the attack progression from a compromised DMZ application toward the internal LAN.

**Expected content:** Initial DMZ compromise → discovery of APM connection → attempted tunnel/pivot → internal APM compromise → potential movement toward internal data stores. The graph should also show containment when the strict unidirectional rule/data diode is correctly enforced.

**Placeholder:**  
`[INSERT SCREENSHOT: rendered attack-graph-1.puml]`

---

## E06 — Threat Scenario 2: Malicious Telemetry Payload Injection

**Purpose:** Demonstrate the malicious telemetry / parser-injection threat path.

**Expected content:** Compromised/intercepted probe → malformed telemetry → ingestion parser → potential RCE → internal compromise, together with schema validation and least-privilege controls.

**Placeholder:**  
`[INSERT SCREENSHOT: rendered attack-graph-2.puml]`

---

## E07 — Data Flow and Trust Boundaries

**Purpose:** Provide visual evidence for the six documented data flows (DF-01 through DF-06) and their controls.

**Expected content:**

- DMZ Application Host → DMZ APM Probe Agent
- DMZ APM Probe Agent → Firewall Conduit
- Firewall Conduit → APM Ingestion Service
- APM Ingestion Service → APM Processing Engine
- APM Processing Engine → Telemetry Database
- Telemetry Database → Operational Dashboard

The screenshot should make the DMZ, firewall/security boundary, and trusted LAN boundary visible.

**Placeholder:**  
`[INSERT SCREENSHOT: rendered data-flow architecture / annotated diagram]`

---

## E08 — Data Classification Matrix

**Purpose:** Demonstrate classification and handling requirements for performance metrics, system metadata, transaction trace headers, and security audit logs.

**Placeholder:**  
`[INSERT SCREENSHOT: data classification matrix from report or Markdown source]`

---

## E09/E10 — CVSS Evidence

**Purpose:** Demonstrate how the top two modeled vulnerabilities were quantified.

**Capture:** If the official CVSS calculator or another approved scoring tool was actually used, capture the vector and resulting score. Otherwise, retain the report's documented vector/reasoning without claiming external calculator execution.

**Vulnerability 1:** Lateral pivot / firewall misconfiguration.

**Vulnerability 2:** Remote Code Execution via malicious payload.

**Placeholder:**  
`[INSERT SCREENSHOT: CVSS calculation for vulnerability 1]`

`[INSERT SCREENSHOT: CVSS calculation for vulnerability 2]`

---

## E11 — Diagram Source Validation

**Purpose:** Demonstrate reproducibility of the PlantUML diagrams.

**Capture:** A local render or repository/tool output showing that the `.puml` files render successfully.

**Placeholder:**  
`[INSERT SCREENSHOT: PlantUML render/validation output]`

---

## E12 — Security Test Results

This item is **optional and must only be populated if actual testing was performed**.

Possible evidence could include:

- blocked reverse/inbound DMZ-to-LAN connection;
- rejected telemetry with an invalid schema;
- failed mTLS authentication;
- rate limiting of excessive telemetry;
- PII redaction from trace headers;
- RBAC denial for an unauthorized dashboard action.

Do **not** create screenshots of simulated test results and present them as real execution evidence.

**Placeholder:**  
`[INSERT ONLY ACTUAL TEST EVIDENCE, IF AVAILABLE]`

---

## Evidence-to-Report Traceability

| Evidence | Report Area |
|---|---|
| E02–E04 | B.2 — C4 architecture |
| E05–E06 | B.3 Task 2 — Threat modeling and attack graphs |
| E07 | B.2 — Data flow mapping and trust boundaries |
| E08 | B.2 — Data classification |
| E09–E10 | B.4 — CVSS risk quantification |
| E11 | Diagram-as-code / reproducibility |
| E12 | B.3 — Defense-in-depth validation, only if actually tested |

## Important Submission Rule

The evidence folder should contain **real supporting evidence or clearly labeled placeholders**. It should not contain fabricated screenshots, fabricated tool output, or screenshots that expose confidential organizational information.
