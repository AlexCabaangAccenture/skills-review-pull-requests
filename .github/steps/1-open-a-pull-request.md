Integration usage (from SPESTG-38)
– Azure Function (SPESTG-38) will create one Deceased Estate Staging record per DIA file and attach the CSV.
– Fields updated by integration: File Name, File Type, File, Received On, Processing Started On, Processing Status (Pending / In progress / Failed), Retry Count, Error Message, Error Details.
– Fields updated by the D365 matching process / Power Automate: Processing Status (Completed / Partial Success / Partial Fail), Processed On.
– Matching script will read the attached CSV and update customer / case records accordingly.
