Summary:

DIA Integration – Azure Blob to Dataverse Staging Table (Service B)

Description:
This sub-story covers all DIA integration steps that can be completed without waiting for DIA–Westpac contract activation. The scope includes consumption of files already present in Azure Blob, data deserialization, building the Dataverse staging table, and outlining the matching logic without touching the live D365 functionality.

Acceptance Criteria:

Azure Function can read the file from Blob Storage.

File schema is validated (row count, column names, date formats).

File is deserialized and inserted into a Dataverse staging table.

Basic matching logic outline is documented (Excel-based version OK).

No DIA dependency required (manual file placement into blob allowed).

Monitoring and error logs are added.

Story is independent and unblocked.

Story B is created for blocked contract work.

Sub-Tasks for Story A:

Define staging table structure in Dataverse

Build Blob file-reading Function

Build deserialization module

Insert rows into Dataverse

Document matching logic outline

Implement logging/monitoring

Update Confluence section “DIA Integration – Service B”
