Hi Vishal,

I completed the initial comparison of the current Deceased Estates Terraform/file/function structure against the SQYC reference pattern.

Summary of findings:

1. Infra/Terraform repo

Current Deceased Estates infra repo:
WNZL.ICOW.DE.ELZIntInfra

Reference infra repo:
WNZL.WF.AzureELZ.Infrastructure

Both repos follow the same high-level Terraform structure:

* base_environment
* global_variables
* elz_local
* root-level Terraform pipeline YAML files

The root pipeline also follows the same pattern of using elz_local templates and passing base_environment as the Terraform configuration directory.

Based on this initial check, I do not see a major Terraform folder structure gap against the reference infra repo.

2. Function services repo

Current Deceased Estates function repo:
WNZL.ICOW.DE.ELZIntServices

Current structure:
repo root
src
WNZL.ICOW.DeceasedEstates.IntServices
Pipeline
WNZL.ICOW.DeceasedEstates.AzureFunctions
WNZL.ICOW.DeceasedEstates.Services
WNZL.ICOW.DeceasedEstates.Services.Tests

Reference SQYC services repo:
WNZL.WF.AzureELZ.Services

Reference structure:
repo root
Pipelines
WNZL.SKYC.Dataverse.Func

This is the main structure difference found. SQYC keeps the pipeline folder and function project directly under the repo root, while Deceased Estates has an additional src/WNZL.ICOW.DeceasedEstates.IntServices nesting layer.

3. Impact if we align the function repo structure

The Deceased Estates function build/deploy/Sonar pipeline files currently have path references tied to the existing nested structure, including:

* solution path
* function project csproj path
* publish project path
* package/artifact path
* SonarQube source/project path

Because of this, restructuring the function repo would not be only a folder move. It would require coordinated updates to pipeline YAML paths and validation of build, deploy, and SonarQube execution.

4. Risk

The current Dev/Test/UAT deployment baseline has already been validated from the merged branch. Changing the structure now could affect:

* build solution discovery
* function app publish output
* deployment package generation
* deployment stages
* SonarQube analysis path
* documentation references

5. Recommendation

My recommendation is to treat this as a separate cleanup/alignment item rather than a quick change under the already validated deployment work.

Suggested approach:

* Confirm the target structure to align with the SQYC services repo pattern.
* Create a separate branch/PR for the structure alignment.
* Move the function pipeline and project folders in a controlled way.
* Update the build, deploy, and SonarQube YAML path references.
* Validate build and SonarQube first.
* Then validate deployment in Dev before considering Test/UAT promotion.

This keeps the completed Dev/Test/UAT deployment baseline protected while still allowing the structure alignment to be planned properly.

I can walk through the comparison and proposed alignment if needed.
