Acceptance Criteria (Updated)

1. System can retrieve DIA encrypted files from the designated blob container.
2. System can decrypt the file using the provided PGP private key (once provisioned).
3. Decrypted data is stored in a staging table in Dataverse for further processing.
4. System triggers the matching logic (once implemented) and logs the decision outcome.
5. System handles invalid files, missing metadata, or unexpected formats with appropriate logging.
6. System produces monitoring and audit logs for each execution cycle.
7. Story is split into: 
   – Story A: Blob → Staging (can be built now)  
   – Story B: DIA SFTP → Blob (blocked until DIA contract and credentials)
