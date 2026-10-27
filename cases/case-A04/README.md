# Failures across several accounts

Submitted one incorrect password for each of five lab accounts through File Explorer's credential dialog, all from SOC-WS01 to SOC-SRV01. The query groups by source address and counts distinct account names over ten minutes.

The first comparison returned four accounts; the next returned five. Later live searches returned five and then four as older attempts expired. Those later windows also include a real lab.user1 failure from the following comparison, which kept that account present after its initial attempt expired.

The distinct-account results matched the original target 4625 records. This pattern is useful for finding a source trying several accounts; the count alone does not establish malicious intent.

[Four-account search](four-account-search.spl) - [Five-account search](five-account-search.spl)

![Five distinct accounts](screenshots/A04-five-accounts-search.jpg)

[Timeline](timeline.csv) - [Original Windows events](selected-events/)
