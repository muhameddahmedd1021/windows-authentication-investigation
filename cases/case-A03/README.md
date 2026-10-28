# Repeated password failures

This controlled case models concentrated password-guessing activity against one account and tests whether a moving-window search detects the repeated failures.

Used File Explorer's network credential dialog on SOC-WS01 to submit individual incorrect passwords for SOC\lab.repeat against SOC-SRV01. Each rejected submission was captured from the Windows interface.

The search counts failures in the preceding five minutes. Two failures stayed below the three-failure threshold. Three failures reached it, and a separate four-attempt group exceeded it. Spaced attempts dropped out of the window, so the counter decreased even though the overall number of attempts increased.

All 17 target failures were type 3 network logons from 192.168.144.30 with bad-password substatus 0xc000006a. The target record IDs and rolling counts matched the original Windows records.

**Result:** the detection found the intended repeated-failure pattern. Every submission in this case was rejected; there was no successful logon in this experiment. The [internal alert test](../../docs/dashboard-and-alert.md) used these recorded events.

[Five-minute search](rolling-failures.spl) - [Search results](rolling-failures.csv)

![Windows rejection](screenshots/A03-H-03-failure.jpg)

![Four failures inside five minutes](screenshots/A03-I-search.jpg)

[Timeline](timeline.csv) - [Original Windows events](selected-events/)
