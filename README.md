Student Information
Student Names: Saptarsi Roy & Girish Amrutesh Joshi
Course Code: SS ZG681 / SE ZG681 Advanced Cyber Security
Evaluation Component: EC-1 Expanded Situated Learning Project
System Selected: DMZ-to-LAN APM Bridge
System Type: Anonymized / Simulated Enterprise Architecture


Confidentiality Statement
This repository and its accompanying reports do not contain proprietary, sensitive, or confidential organizational information. All internal network topographies, hostnames, IP addresses, vendor specifics, and security findings have been safely abstracted and generalized using safe placeholders in accordance with BITS Pilani confidentiality guidelines.
Project Overview

This repository contains the complete security architecture evaluation, C4 model diagrams, threat modeling, CVSS v3.1 risk quantification, and defense-in-depth engineering design for a DMZ-to-LAN Application Performance Monitoring (APM) Data Bridge. The project evaluates security boundaries, data classification, and mitigation strategies against lateral movement and malicious telemetry injection attacks.

Repository Structure

cyber-security-assignment_GS/
├── README.md                              # Main repository overview and setup instructions
├── report/
│   ├── final-report.md                    # Comprehensive Markdown engineering report
│   └── final-report.pdf                   # Exported publication-ready PDF report
├── diagrams/
│   ├── c4-context.puml                    # C4 Level 1: System Context Diagram
│   ├── c4-container.puml                  # C4 Level 2: System Container Diagram
│   ├── c4-component.puml                  # C4 Level 3: Ingestion Service Component Diagram
│   ├── c4-code-optional.puml              # C4 Level 4: Optional Code/Class Diagram
│   ├── attack-graph-scenario-1.puml       # Threat Scenario 1: Lateral Pivot Attack Graph
│   ├── attack-graph-scenario-2.puml       # Threat Scenario 2: Telemetry Injection Attack Graph
│   └── did-architecture.puml              # Defense-in-Depth Layered Architecture Diagram
├── risk/
│   ├── cvss-table.md                      # CVSS v3.1 base, temporal, & environmental scores
│   └── risk-register.csv                  # Itemized enterprise risk register
├── templates/
│   ├── data-classification-matrix.md      # Data asset classification mapping
│   ├── cia-analysis.md                    # CIA triad valuation and failure scenarios
│   └── defense-in-depth-template.md       # Multi-layer control mapping matrix
├── scripts/
│   ├── check_structure.py                 # Structure validation helper script
│   ├── grade_report.py                    # Automated completeness & keyword review script
│   └── check_plantuml_files.py            # PlantUML syntax validator script
└── presentation/
    └── viva-presentation-outline.md       # 10-slide executive viva presentation outline


