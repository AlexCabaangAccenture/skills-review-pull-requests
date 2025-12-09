Update – Integration Alignment & Next Steps

Azure subscription access issue is still pending
Evidence provided to Kostav; awaiting access activation to proceed with Function App deployment setup.

Staging Table Design Reviewed (Story 64)

Confirmed that one staging record = one CSV file

Integration will only insert the metadata; row-level processing is performed by D365/PowerAutomate

Azure Function – planned responsibilities

Trigger on new Blob file

Extract file metadata

Insert staging entry into D365 (via API)

Set initial fields (ReceivedOn, ProcessingStatus = Pending)

Out of scope for this story

Power Automate matching script

Updating processing timestamps and status after processing

Any D365-side retries or validation logic

Next Steps (pending access)

Prepare function skeleton for Blob Trigger

Confirm endpoint + authentication for D365 API insert

Prepare draft flow diagram for internal processing

Coordinate with D365 team once sample CSV file format is shared

Will proceed with design tasks while waiting for environment access.
