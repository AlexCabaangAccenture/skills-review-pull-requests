Title:
DIA SFTP/ELZ File Retrieval Service (Blocked Pending Contract)

Story Description:
This story captures the work required for DIA → Westpac Azure integration.
The service will connect to DIA’s Azure-hosted file repository, fetch the encrypted DIA file daily, and drop it into the project Blob Storage.

Status:
BLOCKED — pending DIA contract signing and credential provisioning.

Acceptance Criteria (AC):

Connectivity to DIA Azure SFTP / repository is established.

Credentials (service principal / keys) are provisioned by enterprise security.

Daily schedule fetches the file and writes it to Blob.

Logs are available in App Insights.

Error notifications are raised on failed fetch.

Security and networking config approved (VNet, firewall, IP allowlist).

Unblocked when the DIA contract is signed and access is provided.
