FINAL Subtasks to move under Substory A

These are the ones you will paste inside the JIRA Subtasks, buddy:

1. File Retrieval

Read daily DIA file from Azure Blob Storage

Validate filename pattern + timestamp

2. File Schema Validation

Validate JSON schema

Validate required fields

Validate row count ≥ 1

3. Deserialize Into POCO

Deserialize JSON into strongly typed POCO classes

Handle null/invalid data safely

4. Insert Into Dataverse Staging Table

Map POCO → Staging table DTO

Upsert records into Dataverse staging table

Capture insert/update result

5. Basic Matching Logic (Template Only)

Load matching rules from Excel / config

Apply simple row-level matching checks

Produce “Match”, “No Match”, “Needs Review” tags
(Not the final matching engine — only structure.)

6. Monitoring & Logging Bootstrap

Log file receipt

Log validation result

Log number of inserted rows

Provide error hooks for future monitoring board

--------------

1. ELZ Connectivity Setup

Validate connectivity requirements between Westpac ELZ → Azure

Confirm network path, firewall, and routing prerequisites

Identify required endpoints and whitelisting

2. Access & Permissions Validation

Validate required access for SFTP / Blob handoff

Confirm identity mechanism (Service Principal / Managed Identity)

Document permission gaps

3. Encryption & PGP Handling

Validate encryption standards required by DIA

Confirm PGP key pairs, storage strategy, and rotation requirements

Identify where private keys will be stored (KeyVault)

4. Credential Dependency Checks

Identify all secrets required from DIA (SFTP host, username, pubkey, etc.)

Mark the story as Blocked until DIA provides credentials

Document the credential flow end-to-end

5. Interface Handover Planning

Define how ELZ will push or expose files

Define how Azure will poll or retrieve from ELZ

Document differences from developer simulation mode


-------------------

DIA Matching Logic & Execution Outcome Updates (Service C)

Covers full matching logic using staging table inputs, rule evaluation, determining “pending / matched / unmatched”, writing results back to Dataverse, and preparing the output for D365 consumption. Includes logging, error handling, and mapping decisions.

Purpose:

Transform deserialized POCO into structured rows

Apply matching rules

Mark status (Matched / NotMatched / Invalid)

Prepare data for Dataverse outcome table

Logging + monitoring
