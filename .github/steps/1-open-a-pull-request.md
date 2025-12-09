Hi team,

I reviewed the staging table design and aligned it with the integration requirements for SPESTG-38.
Below is the confirmed understanding and how the integration will use the staging table:

* Integration Alignment (SPESTG-38 -> Staging Table)

One staging record corresponds to one uploaded CSV file (not per row).
The row-by-row processing will be handled within Power Automate / D365, not on the Azure side.

Azure Function will populate:

File Name

File Type

Received On (date/time when file is received)

Processing Status = Pending

File (attachment) — if enabled on the table (else SharePoint link)

Power Automate will be responsible for:

Updating Processing Started On

Updating Processing Status (In Progress, Completed, Partial, Failed)

Updating Processed On

Populating Retry Count

Writing to Error Message and Error Details

The staging table fields fully support the expected end-to-end flow for:

File receipt

Processing orchestration

Status update and troubleshooting

No additional schema requirements from the integration side at this time.

Thanks, let me know if further alignment is needed.

That's your final comment for SPESTG-64.
