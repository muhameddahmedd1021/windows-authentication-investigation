# Search guide

Each search answers one question. The files use the actual lab index and hosts; time filters select the recorded UTC window. Set those filters to your own run when reusing a search.

| Question | Search |
|---|---|
| Which hosts and channels supplied events? | [Source inventory](source-inventory.spl) |
| What happened, in time order? | [Authentication timeline](authentication-timeline.spl) |
| Which accounts and sources had failures or successes? | [Source and account](source-and-account.spl), [account summary](account-summary.spl) |
| Why did network logons fail? | [Failure reasons](failure-reasons.spl) |
| Did one account reach three failures in five minutes? | [Repeated failures](repeated-failure-candidates.spl) |
| Did one source try five accounts in ten minutes? | [Distinct accounts](multiple-account-candidates.spl), [per-account counts](multiple-account-detail.spl) |
| Was success preceded by a failure for the same account and source? | [Success comparison](success-comparison.spl) |
| Was the account locked, unlocked and able to authenticate again? | [Lockout recovery](lockout-recovery.spl) |
| Was the account disabled? | [Disabled account](disabled-account.spl) |
| Did the scheduled task fail at authentication or during its action? | [Authentication](task-authentication.spl), [task results](task-run-results.spl) |
| Can fixed time buckets miss the repeated-failure threshold? | [Rolling window](rolling-window-boundary.spl), [fixed buckets](fixed-window-comparison.spl) |
| How does the validator's address compare with the source? | [Validator address](validator-address.spl) |
| Did the internal alert run and suppress repeat notifications? | [Scheduler results](alert-scheduler.spl) |

`dedup Computer Channel EventRecordID` removes repeat forwarding of the same Windows record. Different records from one Explorer submission stay visible. `sort` orders events, `stats` counts or groups them, and `streamstats time_window=5m` keeps a moving five-minute count.

The network summaries explicitly select the SOC domain and the target machines. Supporting credential-validation events are investigated in their own searches. For the Kerberos example, `replace` removes the IPv4-mapped prefix for comparison while keeping the original `IpAddress` column. Missing addresses are not assigned a shared attacker address.

The success search carries forward the latest failure for each account and source, then measures the gap at successful events. Its displayed yes/no result makes the different-account and late-success controls visible. The known case labels in the case summary come from the lab timeline; they are separate from the event fields.
