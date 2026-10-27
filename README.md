# Windows Authentication Investigation

A Windows domain lab investigation of failed logons, password correction, repeated attempts, account lockout and stale scheduled-task credentials. The aim was to explain each pattern using its account, source, target, timing and failure reason.

Used File Explorer and Active Directory interfaces for the network authentication comparisons, Task Scheduler for the batch-logon case, and Splunk Search for investigation. Windows events and interface pictures are linked in each case.

![Authentication dashboard](dashboard/dashboard-overview.jpg)

## Lab

| System | Role |
|---|---|
| SOC-DC01 | Windows Server 2022, Active Directory and DNS |
| SOC-WS01 | Windows Server 2022, source domain member |
| SOC-SRV01 | Windows Server 2022, target file server |
| SOC-SIEM | Splunk Enterprise 9.4.1 |

Domain: `soc.test` (`SOC`). All event times are UTC. [Lab setup](docs/lab-setup.md) - [Collection configuration](config/README.md)

## Investigations

| Case | Finding |
|---|---|
| [Normal sign-in](cases/case-A01/README.md) | One credential submission opened SOC-Share; source, validator and target records agreed |
| [Password correction](cases/case-A02/README.md) | A wrong password was rejected, then the corrected entry succeeded |
| [Repeated failures](cases/case-A03/README.md) | Two, three and four failures tested the five-minute threshold; spaced entries showed expiry |
| [Several accounts](cases/case-A04/README.md) | Four and five distinct accounts tested the ten-minute rule |
| [Failure then success](cases/case-A05/README.md) | The same-account success at 103 seconds matched; another account and a 918-second gap did not |
| [Lockout](cases/case-A06/README.md) | Lockout blocked a correct credential; administrative unlock restored authentication |
| [Disabled account](cases/case-A06-D/README.md) | Windows reported account disablement; the original enabled state was restored |
| [Scheduled task](cases/case-A07/README.md) | A saved credential became stale after a password change; task history separated this from a missing batch-logon right |

The network comparison contains 41 target logon records: 35 failures and 6 successes. These are event counts; Explorer sometimes retried a single credential submission. Supporting DC and source records are kept separately rather than added as extra attempts. The scheduled-task case has its own batch-logon timeline.

Repeated failures and a following success are useful investigation leads. The lab's known password-correction and task examples show why counts alone are not a verdict.

## Searches and evidence

[Query guide](queries/README.md) - [Detection tests](docs/detection-validation.md) - [Dashboard and alert](docs/dashboard-and-alert.md) - [Master timeline](evidence/master-timeline.csv) - [Case summary](evidence/case-summary.csv) - [File hashes](SHA256SUMS.txt)
