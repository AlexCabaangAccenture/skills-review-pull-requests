# SPESTG-1054 Evidence Summary

Story: SPESTG-1054
Title: Deploy Integration infra and Resource to UAT

## Summary

The deployment and documentation work for SPESTG-1054 has been completed from my side.

The evidence below maps to the story acceptance criteria:

1. Terraform pipeline is able to deploy infra and resources to UAT environment
2. Terraform code is configured to deploy infra and resources to Prod environment as well
3. Library variables cleaned and no duplicate
4. Library group created/configured for all environments
5. Pipelines, infra, and function app documented

## Evidence links to update

Replace the placeholders below with the actual Westpac links before attaching/updating the Jira story.

* [LINK-1] WNZL.DE.AzureELZ.TerraformBaseInfra pipeline run 20260526.2
* [LINK-2] WNZL.DE.ELZIntInfra pipeline run 20260602.1
* [LINK-3] WNZL.DE.ELZIntServices pipeline run 20260529.9
* [LINK-4] Azure deployment documentation Confluence page
* [LINK-5] 2.4 Pipelines Confluence page
* [LINK-6] Related PR/reference links, if added separately
* [LINK-7] Azure resource validation screenshot/evidence, if added separately
* [LINK-8] Library variable group/backend setting evidence, if added separately

## Evidence by acceptance criteria

### 1. Terraform pipeline is able to deploy infra and resources to UAT environment

Evidence:

* UAT deployment pipeline was executed successfully.
* Latest infra deployment run from the merged branch completed successfully through Build, Dev, Test, and UAT.
* UAT resource deployment/configuration was validated after pipeline execution.

Attach/link:

* [LINK-2] WNZL.DE.ELZIntInfra pipeline run: 20260602.1

  * Evidence: Build, Dev, Test, and UAT stages completed successfully.
  * Prod stage was skipped.
  * PR reference: Merged PR 28638: SPESTG-1054 Add Key Vault secret access for Function App identity.

* [LINK-1] WNZL.DE.AzureELZ.TerraformBaseInfra pipeline run: 20260526.2

  * Evidence: Dev, Test, and UAT stages completed successfully.
  * Prod stage was skipped.
  * PR reference: Merged PR 28435: Fix Test bootstrap environment value.

* [LINK-7] UAT Azure resource validation evidence, if available.

Status: Completed

### 2. Terraform code is configured to deploy infra and resources to Prod environment as well

Evidence:

* Terraform pipeline includes Prod deployment stage/configuration.
* Prod stage is visible in the Terraform deployment pipeline runs.
* Prod deployment was skipped and remains subject to the normal approval/release process.

Attach/link:

* [LINK-1] WNZL.DE.AzureELZ.TerraformBaseInfra pipeline run: 20260526.2

  * Evidence: Prod stage exists in the pipeline and was skipped.

* [LINK-2] WNZL.DE.ELZIntInfra pipeline run: 20260602.1

  * Evidence: Prod stage exists in the pipeline and was skipped.

* [LINK-5] Pipeline documentation page covering environment execution order.

Status: Completed from configuration/documentation perspective

### 3. Library variables cleaned and no duplicate

Evidence:

* Library variable usage was reviewed and cleaned as part of deployment readiness.
* Environment-specific variable groups/backend settings were aligned for the deployment flow.
* Pipeline execution completed successfully using the configured environment/backend variable groups.

Attach/link:

* [LINK-8] Pipeline/library variable configuration evidence, if available.
* [LINK-4] Azure deployment documentation page.
* [LINK-5] Pipeline documentation page showing environment/backend variable group usage.

Status: Completed

### 4. Library group created/configured for all environments

Evidence:

* Backend/environment variable groups were configured for the deployment flow.
* Deployment pipeline references the required backend variable groups per environment.
* Pipeline completed successfully through Dev, Test, and UAT using the configured deployment flow.

Attach/link:

* [LINK-2] WNZL.DE.ELZIntInfra pipeline run: 20260602.1

  * Evidence: Build, Dev, Test, and UAT stages completed successfully.

* [LINK-5] Pipeline documentation page showing environment execution order and backend variable group usage.

* [LINK-8] Library variable group/backend setting evidence, if available.

Status: Completed

### 5. Document the pipelines, infra, and function app

Evidence:

* Azure deployment documentation was updated.
* Pipeline links and execution order were documented.
* Validation notes, known constraints, and PR/reference details were added.
* The 2.4 Pipelines Confluence page was updated with Azure pipeline links and execution order.
* Function app deployment pipeline evidence is available.

Attach/link:

* [LINK-4] Azure deployment documentation page.

* [LINK-5] 2.4 Pipelines Confluence page.

* [LINK-3] WNZL.DE.ELZIntServices pipeline run: 20260529.9

  * Evidence: Function app deployment pipeline completed successfully.
  * PR reference: Merged PR 28631: SPESTG-480 Deploy DIA Function App exception handling updates.

* [LINK-6] Related PR/reference links, if added separately.

Status: Completed

## Pipeline run summary

| Pipeline                            |        Run | Evidence                                                 | Related PR                                                                         |
| ----------------------------------- | ---------: | -------------------------------------------------------- | ---------------------------------------------------------------------------------- |
| WNZL.DE.AzureELZ.TerraformBaseInfra | 20260526.2 | Dev, Test, and UAT completed. Prod skipped.              | Merged PR 28435: Fix Test bootstrap environment value                              |
| WNZL.DE.ELZIntInfra                 | 20260602.1 | Build, Dev, Test, and UAT completed. Prod skipped.       | Merged PR 28638: SPESTG-1054 Add Key Vault secret access for Function App identity |
| WNZL.DE.ELZIntServices              | 20260529.9 | Function app deployment pipeline completed successfully. | Merged PR 28631: SPESTG-480 Deploy DIA Function App exception handling updates     |

## Additional notes

The latest deployment baseline has been validated across Dev, Test, and UAT.

A separate structure comparison summary was also prepared and sent for review. That structure review is a follow-up analysis item and is not considered a blocker for SPESTG-1054 closure.

## Closure statement

The deployment and documentation items under SPESTG-1054 have been completed from my side. Evidence has been attached/linked to support story closure.
