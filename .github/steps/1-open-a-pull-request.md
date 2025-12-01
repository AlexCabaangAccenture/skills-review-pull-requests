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


