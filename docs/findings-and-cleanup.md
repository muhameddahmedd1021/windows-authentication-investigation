# Findings and cleanup

Bad-password, disabled-account, locked-account and batch-logon-right failures needed different explanations. Source 4648, target 4624/4625 and DC 4776/4771 records helped connect the credential submissions without treating every supporting event as another attempt. Share events and task/process evidence supplied the next layer of context.

The lockout recovery also separated authentication from authorization: DC 4624 confirmed the recovered credential, while Explorer still denied access to NETLOGON. In the task case, successful process/file events and an unchanged marker after the failed launch distinguished execution from failure before the action started.

For triage, check the account, source, target, time gap, logon type and failure reason together. A repeated pattern with an unexplained successful logon deserves follow-up; a known task or password correction explains some otherwise similar patterns.

After testing, all ten lab accounts were enabled and unlocked. The task and its temporary grant were removed, the marker and evidence were retained, the network test mapping was disconnected, and the alert validation schedule was stopped. The isolated lab's share and dedicated lockout policy remain available for the next investigation.
