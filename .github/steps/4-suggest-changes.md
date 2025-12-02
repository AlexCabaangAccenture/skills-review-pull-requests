Summary:

DIA Integration – ELZ File Retrieval (Contract-Dependent)

Description:
This story captures the integration work that depends on the DIA–Westpac contract and ELZ access. The work involves establishing secure connectivity from DIA Azure to Westpac ELZ, fetching the DIA file directly from their repository, and dropping it into Blob storage.

Acceptance Criteria:

ELZ connectivity details documented.

Architecture validated with Westpac security team.

Service A design documented (fetch file → drop into blob).

Contract dependency explicitly marked.

This story must not begin until legal agreement is signed.

Sub-Tasks:

Review contract requirements

Design ELZ inbound file retrieval

Define security headers & authentication

Document API call sequence for Service A

Update Confluence “DIA Integration – Service A”
