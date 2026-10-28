# Findings and cleanup

## Case outcomes

The repeated-account case produced 17 failed target logons and no success. Its rolling-window search detected the planned threshold groups, and a scheduled alert was validated against those records. The account-spread case produced five rejected submissions across five accounts from one source; its distinct-account search detected the planned group.

The failure/success comparison used separate, deliberate submissions. Its 103-second same-account pair matched the correlation condition; the different-account and late-success comparisons did not. Normal sign-in, password correction, lockout, disablement and task credentials supplied the other known contexts. Each case was checked against source records rather than classified from counts alone.

These are controlled investigation and detection tests. The recorded scheduled alert is distinguished from the case searches in the [alert documentation](dashboard-and-alert.md).

## Interpretation and response

Bad-password, disabled-account, locked-account and batch-logon-right failures needed different explanations. Source 4648, target 4624/4625 and DC 4776/4771 records helped connect the credential submissions without treating every supporting event as another attempt. Share events and task/process evidence supplied the next layer of context.

The lockout recovery also separated authentication from authorization: DC 4624 confirmed the recovered credential, while Explorer still denied access to NETLOGON. In the task case, successful process/file events and an unchanged marker after the failed launch distinguished execution from failure before the action started.

For triage, check the account, source, target, time gap, logon type and failure reason together. A repeated pattern with an unexplained successful logon deserves follow-up; a known task or password correction explains some otherwise similar patterns.

After testing, all ten lab accounts were enabled and unlocked. The task and its temporary grant were removed, the marker and evidence were retained, the network test mapping was disconnected, and the alert validation schedule was stopped. The isolated lab's share and dedicated lockout policy remain available for the next investigation.
