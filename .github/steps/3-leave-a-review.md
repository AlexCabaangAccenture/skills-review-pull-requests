Hi Swapna, Kaustav

As discussed, I’ve completed the detailed HLD draft and consolidated requirements in SP-ESTG-5 (Story Description).

Please review when convenient.

To proceed with the environment setup and begin implementation work, kindly help confirm/provision the following Azure resources:

Resource Group under the correct subscription

Storage Account (Blob) for temporary encrypted/decrypted file handling

Key Vault for storing private keys and SFTP credentials

Function App for File Ingestion + AES256 Decryption + Validation

SFTP Endpoint Credentials (DIA → Westpac secure transfer)

Application Insights for monitoring, logging and alerting

Service Bus Namespace (if required, based on the final design and whether we decouple steps asynchronously)

Let me know if you need the export of the HLD text or if we should upload a copy into Confluence after access is enabled.

Thanks!

Alex
