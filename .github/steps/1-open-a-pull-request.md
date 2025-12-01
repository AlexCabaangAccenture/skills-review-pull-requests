1. Introduction

The Department of Internal Affairs (DIA) currently sends daily death notifications manually via email attachments. Files are manually downloaded, verified, and uploaded to Estate Guardians. This process is time-consuming, prone to delay, and lacks monitoring capability.

2. Purpose

Define and implement a secure, automated SFTP-based integration with DIA so Westpac systems can reliably receive, decrypt, validate, and process death notification files under the Estate Guardians (EG) workflow.

3. Scope

This story covers:

Secure reception of DIA files via sFTP

AES256 decryption of incoming files

Validation of file presence before end-of-day processing

Basic monitoring & alerting for missing or invalid files

Preparing outputs for onward consumption by Estate Guardians workflow

Storing decrypted files in the EG State Management SharePoint location

Not in scope:

DIA-side changes

D365 update logic

Business validation workflow

Full monitoring dashboard (covered in SP-ESTG-21)

4. High-Level Summary of Target Design

At a high level, the automated solution will:

Receive encrypted death notification files from DIA via sFTP.

Automatically detect new file arrival.

Begin decryption using AES256 and Westpac-secured private keys.

Extract and prepare clean daily death notification data for Estate Guardians.

Save processed output into the State Management SharePoint library.

Raise alerts if:

File is missing by cut-off

File integrity is invalid

Decryption fails

File does not meet encryption requirement

5. Interfaces & Integration Points

sFTP Endpoint (DIA → Westpac)
For secure file transfer.

Azure Function App – File Ingestion
Detect, pull, decrypt, validate files.

Azure Storage (Blob / KeyVault)
For temporary storage & key retrieval.

SharePoint EG State Management Library
Final resting place of processed outputs.

Alerting (App Insights / Email / Logs)
Based on monitoring definitions.

6. Non-Functional Requirements

All file transfers must use secure encryption (SFTP channel + AES256 file-level encryption).

Azure Function processing must complete within SLA agreed with EG / DIA.

Monitoring must surface any errors or missing files within the defined cut-off window.

Logging must capture traceability for: file name, time pulled, time decrypted, validation results.

Solution must be scalable to handle future changes in DIA file size or schedule.

7. Assumptions

DIA will continue to provide daily files in the existing encrypted format.

Westpac procurement team will supply updated credentials for SFTP connection.

The EG SharePoint library is the correct target location for decrypted files.

No D365 updates are required as part of this initial integration.

Westpac internal firewall rules will support outbound SFTP connection.

8. Constraints

No direct write-back to DIA systems.

Encryption/decryption logic must follow DIA rules (cannot be modified).

Access to DIA SFTP may take time due to external approval flows.

SharePoint upload limits apply (file size, API constraints).

Only the EG workflow consumes the decrypted data.

9. Risks

Delay in obtaining SFTP access credentials may block development timelines.

Failure in decryption due to wrong key version would halt file processing.

Missing files may cause operational delays in EG workflow.

Misalignment between business cut-off expectations vs. technical processing window.

Incorrect SharePoint configuration may cause upload failures.

10. Open Points

Confirm DIA SFTP folder path and test endpoint.

Confirm expected filename pattern and retention period.

Confirm maximum file size and number of records per daily file.

Confirm SharePoint library folder structure under EG State Management.

Confirm alerting routing (EG support inbox, wider team, or shared DL).

