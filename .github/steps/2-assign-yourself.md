Integration notes and current plan (aligned with SPESTG-64)
– SPESTG-64 (“Create a staging table in D365”) owns the staging table design + Power Automate matching script on the D365 side.
– SPESTG-38 focuses on the Azure integration:

Read decrypted DIA CSV file from Azure Blob (or manually uploaded file during POC).

Create one staging record per file in the Deceased Estate Staging table, attach the CSV, and populate metadata fields (File Name, File Type, Received On, Processing Started On, Processing Status, Retry Count, Error Message / Error Details when applicable).

Set Processing Status to Pending / In progress / Failed from the integration side.
– The Power Automate matching script (owned by the D365 team under SPESTG-64) will later read the attached CSV from this staging record and update D365 cases/customers. That implementation is out of scope for SPESTG-38 but depends on the fields produced by this story.
