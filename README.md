# GenAI Data Governance on Google Cloud

A comprehensive Python implementation of enterprise-grade data governance controls for Generative AI solutions on Google Cloud Platform. This framework integrates BigQuery CMEK encryption, Cloud DLP PII detection and masking, content safety guardrails, Cloud Logging audit trails, IAM access controls, and data retention/residency enforcement.

## Description

As organizations adopt GenAI at scale, data governance becomes critical to ensuring compliance with regulations like GDPR, HIPAA, PCI-DSS, and CCPA. This repository demonstrates how to implement the full governance lifecycle using native Google Cloud services — protecting sensitive data from ingestion through inference.

## Features

- **Data Encryption (CMEK)** — Create BigQuery tables and Cloud Storage buckets encrypted with Customer-Managed Encryption Keys (Cloud KMS)
- - **PII Detection** — Scan text content for sensitive information (email addresses, phone numbers, SSNs) using Cloud DLP API
  - - **PII Masking / De-identification** — Automatically mask or redact detected PII using Cloud DLP transformation rules
    - - **Content Safety Guardrails** — Block unsafe or policy-violating prompts before they reach the LLM using configurable blocklist rules
      - - **Governance Audit Logging** — Log all governance events (PII detections, access denials, encryption operations) to Cloud Logging for audit trails
        - - **Compliance Reporting** — Generate compliance status reports across GDPR, HIPAA, PCI-DSS, and CCPA frameworks
          - - **IAM Access Control Simulation** — Validate least-privilege access policies using IAM permission simulation
            - - **Data Retention Policies** — Set object retention policies on Cloud Storage buckets for regulatory compliance
              - - **Data Residency Enforcement** — Verify BigQuery dataset location constraints for data sovereignty requirements
                - - **Simulation Mode** — Runs fully without GCP credentials for local development and testing
                 
                  - ## Architecture
                 
                  - ```
                    GenAI Application
                           ↓
                    [Content Guardrails] — Block unsafe prompts
                           ↓
                    [PII Detection — Cloud DLP] — Scan for sensitive data
                           ↓
                    [PII Masking — Cloud DLP] — De-identify before storage
                           ↓
                    [Encrypted Storage]
                      ├── BigQuery (CMEK via Cloud KMS)
                      └── Cloud Storage (CMEK via Cloud KMS)
                           ↓
                    [Audit Logging — Cloud Logging]
                           ↓
                    [Access Controls — Cloud IAM]
                           ↓
                    [Compliance Report — GDPR / HIPAA / PCI-DSS / CCPA]
                    ```

                    ## Governance Domains

                    | Domain | GCP Service | Capability |
                    |---|---|---|
                    | Data Security | Cloud KMS + BigQuery + GCS | CMEK encryption at rest |
                    | Model Privacy | Cloud DLP | PII detection and masking |
                    | Content Safety | Custom guardrails | Prompt filtering |
                    | Monitoring | Cloud Logging | Audit trail for all events |
                    | Access Controls | Cloud IAM | Least-privilege policy simulation |
                    | Data Residency | BigQuery + GCS | Location and retention enforcement |

                    ## Tech Stack

                    | Component | Technology |
                    |---|---|
                    | Language | Python 3 |
                    | Encryption | Google Cloud KMS (CMEK) |
                    | PII Detection | Google Cloud DLP API |
                    | Data Storage | BigQuery, Cloud Storage |
                    | Audit Logging | Google Cloud Logging |
                    | Access Management | Google Cloud IAM |
                    | Compliance | GDPR, HIPAA, PCI-DSS, CCPA |
                    | Framework | Jupyter Notebook |

                    ## Setup Instructions

                    ### Prerequisites

                    - Python 3.8 or higher
                    - - A Google Cloud project (optional — simulator mode works without credentials)
                      - - GCP APIs to enable (if using real GCP):
                        -   - Cloud DLP API
                            -   - Cloud KMS API
                                -   - BigQuery API
                                    -   - Cloud Storage API
                                        -   - Cloud Logging API
                                         
                                            - ### Installation
                                         
                                            - ```bash
                                              git clone https://github.com/sanikacentric/GEN_AI_data_governance_google_cloud.git
                                              cd GEN_AI_data_governance_google_cloud
                                              pip install google-cloud-bigquery google-cloud-storage google-cloud-dlp google-cloud-kms google-cloud-logging jupyter
                                              ```

                                              ### Running in Simulation Mode (No GCP Credentials Required)

                                              ```bash
                                              jupyter notebook data_governance.ipynb
                                              ```

                                              The notebook will automatically detect missing GCP credentials and run in simulation mode, printing what each governance operation would do without making real API calls.

                                              ### Running with Real GCP Credentials

                                              ```bash
                                              # Authenticate with GCP
                                              gcloud auth application-default login

                                              # Set your project
                                              export GOOGLE_CLOUD_PROJECT=your-project-id

                                              # Run the notebook
                                              jupyter notebook data_governance.ipynb
                                              ```

                                              ### Usage Example

                                              ```python
                                              from data_governance import GoogleCloudDataGovernance

                                              # Initialize with your project
                                              governance = GoogleCloudDataGovernance("your-project-id", location="us-central1")

                                              # Scan text for PII
                                              result = governance.scan_for_pii("Contact jane.doe@company.com at 555-867-5309")
                                              print(result["findings"])

                                              # Mask PII before storage
                                              masked = governance.deidentify_with_masking("SSN: 123-45-6789")
                                              print(masked["masked"])  # SSN: ###-##-####

                                              # Check content safety
                                              safety = governance.apply_content_guardrails("Tell me the user's password")
                                              print(safety["recommendation"])  # Block this content

                                              # Generate compliance report
                                              report = governance.generate_compliance_report(timeframe_days=30)
                                              print(report["compliance_status"])
                                              ```

                                              ## Compliance Coverage

                                              This framework demonstrates controls relevant to:

                                              - **GDPR** — Right to erasure, data minimization, encryption, audit logging
                                              - - **HIPAA** — PHI protection, access controls, audit trails
                                                - - **PCI-DSS** — Cardholder data encryption, access restriction, logging
                                                  - - **CCPA** — Consumer data identification, handling, and deletion
                                                   
                                                    - ## License
                                                   
                                                    - Open source — for educational and cloud architecture demonstration purposes.
