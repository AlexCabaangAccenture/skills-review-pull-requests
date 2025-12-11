Design – DIA File to D365 Staging Integration Flow

Purpose
Design a high-level integration flow for the DIA file into the Deceased Estate staging table in D365.

This is preparatory design work while access to the Dev/Azure environment is being resolved.

Scope
– File arrival in DIA location (e.g., SFTP / DIA drop / Storage)
– Ingestion by DIA/Deceased Estate Function/App or equivalent integration component
– Validation and basic logging (success / error)
– Creation/update of records in the Deceased Estate staging table in D365
– Linking or storing the file in the appropriate SharePoint / document location
– Initial status handling for records (e.g., Pending, Success, Failed, Partial Success)
– Handover points where D365 or subsequent flows take over

Outputs
– A sequence diagram showing the end-to-end DIA → Staging → D365 flow
– Open questions and assumptions clearly listed (for Kostubh / Swapna / D365 team)

Notes
– This task does not require working environment access; it can be done based on current understanding, previous discussions, and existing documents.
– The diagram will help the team align on responsibilities between DIA integration, D365, and environments once access is fully granted.


Acceptance criteria

Sequence diagram created for the DIA → Deceased Estate staging → D365 flow.
Diagram is stored in a shared location (Confluence or shared folder).
Link to the diagram is added in this subtask.
Any open questions/assumptions are written in a short list in this subtask’s comments.
Subtask status moved to Done once 1–4 are completed.

--------------------------
As discussed in this morning’s stand-up, I’ll use this subtask to track the DIA integration design work while my access is being reset via Fixit. First output will be a sequence diagram for the file-to-staging flow; I’ll attach/link it here once v1 is ready
