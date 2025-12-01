1. Introduction
1.1 Background
- DIA currently sends daily death notification files to the bank.
- The existing process is largely manual: files are decrypted and the matching script is executed manually; outputs are handled by the business team.
- Estate Management workflows and CRM (Dynamics 365) cases are updated manually based on these outputs.

1.2 Purpose
- Describe the high-level technical design for automating the DIA death notification process.
- Provide enough detail for:
  - Azure environment provisioning.
  - Development of ingestion, decryption, and matching automation.
  - Integration with Dynamics 365 and SharePoint.
- Act as a single reference for developers, testers, and business stakeholders.

1.3 Scope
In scope:
- Ingestion of DIA files via secure SFTP into Azure.
- Storage of raw and decrypted files in Azure Storage (Blob/File).
- Automation of the existing DIA matching script.
- Generation and storage of:
  - Full match results.
  - Partial match results.
  - In-scope records (full match + partial match failed on address).
- Creation or update of cases in Dynamics 365 based on in-scope records.
- Outputs to the Estate Management SharePoint location (for audit/monitoring).
- Monitoring, alerting, and error handling for the automated process.

Out of scope (for this HLD):
- Detailed field-level mapping to Dynamics 365 entities.
- Detailed UI changes in Dynamics 365 screens.
- Checklist / downstream estate-management epics (handled in separate HLDs).
- Non-DIA integrations.

1.4 References
- DIA BRD and refined requirements sessions (Transcripts 1–7 & latest refinement call).
- Existing manual DIA matching script documentation [REFERENCE IF AVAILABLE].
- Current Estate Management workflow documentation and process maps.
- Dynamics 365 configuration documentation (routing rules, case entities, etc.).

2. Solution Overview
2.1 Target Solution Summary
At a high level, the solution will:
1) Receive a daily encrypted DIA file via SFTP into Azure Storage.
2) Automatically decrypt the file into a secure decrypted container.
3) Execute the existing DIA matching logic (script) automatically.
4) Produce result files:
   - Full-match file.
   - Partial-match file.
   - “In-scope” file containing:
     - All full matches; and
     - Partial matches that failed on address (treated as full match for automation).
5) Store result files in the Estate Management SharePoint location, aligned with the current business filing practice.
6) For each in-scope record, either:
   - Create a new case in Dynamics 365; or
   - Link to an existing case (if already present) and update required fields (e.g., Date of Death) and indicators.
7) Provide monitoring and alerting for:
   - Missing daily file.
   - Decryption failures.
   - Matching script failures.
   - Case creation/update errors.

2.2 High-Level Objectives
- Reduce manual handling of DIA files and matching logic.
- Ensure consistent and auditable processing of death notifications.
- Improve timeliness and accuracy of Dynamics 365 case updates.
- Maintain or improve the existing audit trail (file outputs and logs).

3. Logical Architecture
3.1 Components (Logical)
- DIA SFTP Endpoint
  - External system sending encrypted death notification files daily.
- Azure Storage Account (DIA Integration)
  - Container: /dia/raw (encrypted files from SFTP).
  - Container: /dia/decrypted (post-decryption files).
  - Container: /dia/results (full-match, partial-match, in-scope files).
- Azure Function App – DIA Integration
  - Timer-trigger function for daily orchestration.
  - Decryption function / activity.
  - Matching-script executor.
  - Case integration function (Dynamics 365).
  - Logging and error handler.
- Key Vault
  - SFTP credentials, encryption keys, connection strings.
- Dynamics 365 (Estate Management)
  - Case entity and related configuration.
  - Status / tag / indicator for “DIA notification received”.
  - Date of Death field and related audit.
- Estate Management SharePoint
  - Final storage location for:
    - Full matches.
    - Partial matches.
    - In-scope records for audit.
- Monitoring & Alerting
  - Application Insights for telemetry.
  - Alert rules for missing file, decryption errors, script failures, etc.

3.2 Integration Pattern
- File-based integration with DIA using secure SFTP.
- Azure timer-triggered batch process for once-per-day execution.
- Script-driven matching logic (reusing existing business script where possible).
- API-based or SDK-based integration with Dynamics 365 for case operations.
- SharePoint integration for final file publishing (via Graph API / SharePoint APIs or configured connectors).

3.3 Environments
- DEV: used for initial development and integration testing (using sample DIA files).
- TEST / UAT: used for business validation with masked or test data.
- PROD: live processing of DIA notifications.

4. End-to-End File Flow
4.1 Daily Ingestion
1) DIA sends encrypted file via SFTP to bank endpoint.
2) Azure SFTP receiver / integration writes the file into Azure Storage: /dia/raw/YYYY/MM/DD/.
3) Timer-triggered Azure Function (e.g., 07:00 NZ time) checks for the expected file.
4) If file is not present by a defined threshold (e.g., within 6 hours of expected time), raise an alert to business/support.

4.2 Decryption
1) Decryption function reads encrypted file from /dia/raw.
2) Uses configured keys/utility to decrypt the file.
3) Writes decrypted file into /dia/decrypted.
4) Performs basic checksum / sanity checks (e.g., record count, file ID/number).
5) If decryption fails, logs detailed error & raises technical alert (to IT/support).
6) Optional: notify business that the DIA file is present but could not be decrypted.

4.3 Matching Script Execution
1) Matching executor function takes the decrypted file as input.
2) Invokes existing DIA matching script logic (or equivalent implementation) to classify records:
   - Full match.
   - Partial match.
   - Partial match with failure on address.
3) Script produces:
   - Full match file (aligned to current business format).
   - Partial match file (aligned to current business format).
4) Automation additionally produces or extracts an “in-scope” file:
   - All full-match records.
   - Partial matches that failed on address (per new requirement to treat as full match).
5) All result files are stored in /dia/results and then published to the configured SharePoint location.
6) Error handling:
   - Script failure => log + technical alert, no Dynamics 365 updates performed.
   - Output validation errors (e.g., missing columns) => log + alert.

4.4 Case Creation & Update – Dynamics 365
For each record in the in-scope file (full match + partial match failed on address):
1) Check whether a case already exists in Dynamics 365 for the deceased person.
   - Matching criteria to be confirmed (e.g., Name, Date of Birth, Address, etc.).
2) If no existing case:
   - Automatically create a new case in Dynamics 365.
   - Link the case to the relevant customer profile.
   - Set Date of Death from the DIA record.
   - Add an indicator/tag/status note that this case came from a DIA notification.
3) If existing case found:
   - Link the DIA notification to the existing case.
   - Check the existing Date of Death on the case:
     - If empty: populate from DIA record.
     - If present but different: update if required, and add a case note describing the change.
   - Add/ensure the DIA notification indicator/tag/status is present.
4) For all updates:
   - Add case notes summarising the action (new case vs existing, fields updated).
   - Ensure case owner/case manager is alerted where Date of Death was added or updated.

Error Handling:
- If Dynamics API fails or validation errors occur:
  - Log detailed context.
  - Flag record for manual follow-up.
  - (Option) write failed records to a separate file in SharePoint for business review.

4.5 Outputs to SharePoint
- Full match file – stored as per current business convention.
- Partial match file – stored as per current business convention.
- In-scope file (full matches + partial matches failed on address) – stored with clear naming, e.g.:
  - DIA_InScope_YYYYMMDD.csv
- Optional: Failed/cannot-process records file.
- Folder structure to follow existing business patterns (to be confirmed with business).

5. Non-Functional & Operational Requirements
5.1 Security
- All file transfers from DIA via secure SFTP.
- Encrypted at rest in Azure Storage.
- Secrets and keys stored in Azure Key Vault.
- Access to storage, functions, and SharePoint restricted via RBAC and least-privilege principles.

5.2 Monitoring & Alerting
- Application Insights used for logs, metrics, and traces.
- Alerts configured for:
  - Daily file not received by cutoff time.
  - Decryption failures.
  - Matching script failures.
  - High error rates for Dynamics 365 operations.
- Logs should contain correlation IDs per file and per record where feasible.

5.3 Performance & Scalability
- Initial volumes expected to be modest (daily batch files).
- Design should support growth in file size without major rework.
- Functions should be able to process the daily file within agreed SLA.

5.4 Audit & Traceability
- Preserve files at each stage:
  - Raw encrypted file.
  - Decrypted file.
  - Result files (full, partial, in-scope, failed).
- Maintain an audit trail in Dynamics 365 via case notes and indicators.
- Retention policies for stored files to align with bank policies.

6. Open Points & Assumptions
6.1 Open Points
- Exact SFTP landing endpoint and folder convention (to be confirmed with DIA and infrastructure).
- Final Azure storage container and folder structure naming conventions.
- Exact technology for running the “existing” matching script (e.g., PowerShell, Python, SSIS, etc.).
- Dynamics 365:
  - Final matching criteria for “existing case” detection.
  - Final design for “DIA notification” indicator (tag, status, label, etc.).
- SharePoint:
  - Final folder structure and permissions for DIA result files.
- Notification channels for alerts (e.g., email, Teams, ITSM).

6.2 Assumptions
- DIA will continue to send one file per day in a consistent format.
- The file format (layout, columns) is stable or changes will be communicated ahead of time.
- Existing manual matching script can be reused or reimplemented with equivalent logic.
- Necessary Azure resources and subscriptions will be provisioned by the infrastructure team.
- Teams (onshore/offshore) will have appropriate access to Dev/UAT environments, SharePoint, and DevOps.

7. Azure Resources (High-Level)
- Subscription: [TO BE CONFIRMED].
- Resource Group: [RG-DIA-EstateMgmt-<ENV>].
- Storage Account:
  - Containers: dia-raw, dia-decrypted, dia-results.
- Function App:
  - Timer trigger function (“DIA_DailyOrchestrator”).
  - Decryption function.
  - Matching executor function.
  - Case integration function.
- Key Vault:
  - SFTP credentials, storage keys, encryption keys, Dynamics connection configuration.
- Application Insights instance linked to Function App.
- (Optional) Service Bus / Queue (if future decoupling is required).

8. Jira / Work Breakdown (High-Level Mapping)
(Note: IDs are illustrative; use actual Jira IDs in your project.)

