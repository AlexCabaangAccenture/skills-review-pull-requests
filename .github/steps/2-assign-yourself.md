Please provision the following resources in the target subscription:

A. Storage & Keys

Azure Storage Account

For temporary file landing

For decrypted file staging

Blob Container(s)

/incoming (raw DIA files)

/processed

Azure Key Vault

AES private key (Westpac)

DIA public key (optional)

SFTP credential secret (username/password OR key pair)

B. Compute

Azure Function App

Runtime: .NET 8

Managed Identity enabled

Access to Key Vault

Access to Storage

App settings placeholder for:

SFTP_HOST

SFTP_PORT

SFTP_USERNAME

KEYVAULT_URL

C. sFTP Connectivity

DIA sFTP Endpoint Whitelist

Outbound IPs for the Function App

Credentials

Test environment username/password, or

Keypair for authentication

D. Monitoring

Application Insights

Log Analytics workspace (linked)

E. DevOps

Deployment Pipeline Access

Permission to create/edit YAML pipeline

Repository access

To push code + configuration

F. SharePoint (Final Output)

EG SharePoint Library access

Target folder where decrypted file should be uploaded

Service account that the Function App will use to upload
