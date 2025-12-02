Title:
DIA File – Blob to Dataverse Ingestion & Staging Table Load

Story Description:
Implement the internal ingestion pipeline that reads the daily DIA file from Azure Blob Storage and loads its structured content into the Dataverse staging table.
This story contains all work that we can complete before the DIA contract is finalized.
The staging table must mirror the required fields defined in the Excel/CSV structure.

Acceptance Criteria (AC):

A Dataverse staging table is defined with fields matching the required schema.

An Azure Function/Service (Service B) reads the file from Blob daily.

The file is parsed and validated (format, encryption flag if applicable).

Records are inserted into the Dataverse staging table.

Logs and failures are captured in App Insights.

Manual file-drop simulation is supported until actual DIA connect is available.

No external DIA dependencies are required for this story.
