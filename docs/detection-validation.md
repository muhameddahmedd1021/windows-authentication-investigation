# Detection checks

The repeated-failure rule reached its threshold at three events in a moving five-minute window. Two events stayed below it; a separate four-entry group exceeded it. In another group, three failures occurred between 20:48:01 and 20:52:57. A rolling count reached three, while fixed five-minute buckets split them into one and two. Fixed buckets would miss that threshold.

The account-spread comparison returned four and then five distinct accounts. Later live searches fell from five to four as an older account left the ten-minute window. One genuine lab.user1 failure from the following case overlapped those later windows; it is included in their explanation.

For success correlation, lab.ops had no preceding failure for that account. Lab.user1's success after 103 seconds matched, while the success after 918 seconds did not. A password-correction case can also match this pattern, so a match needs context.

Lockout, disabled accounts and a stale task credential produced different status codes and supporting events. The [validation table](../evidence/detection-validation.csv) links each check to its evidence.
