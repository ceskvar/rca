# ROOT CAUSE ANALISIS
how to drive a root cause analisis (PostMortem)

RCA most contain:
- Problem Description
- The Root Cause
- Remediation & Prevention
- Impact Description

---

## Problem Description

`Exaple`

### RCA: INCIDENT 20213010A

10/30/2021, The search service was interrupted for 35 minutes. Other important services were not affected and are working normally

---

## The Root Cause

`Exaple`

the search service depends on a database which is hosted in an external service. During the implementation of new feature that included log creation for this one, the logrotate was not configured, so it grew until creating bottleneck that prevented conection to database. it happen 5 days after deploy of that feature.

You can use the `root cause (5 whys)` to detect the cause

>Why search service doesn´t work?
>>- because it couldn´t connect to database

>why it couldn´t connect to DB?
>>- because the server was overloaded

>why server was overloaded?
>>- because logrotate occupies the entire disk

>why log rotate occupied entire disk?
>>- bad configuration

>why it was configured wrongly?
>>- due to human error

---

## Remediation & Prevention

`Exaple`

- Engineering teams were alerted about the problem in search service. 
They got to work and realized that when trying to replicate searches, the microservice did not respond correctly. Also when the team began to review the logs they found a singular error, "No space left on device", in this way the problem was detected and it was decided to stop the service to drain the disk. After 5 minutes the service was working normally.

- Once the service was recovered, the logrotate configuration was reviewed, where it was found that there was no entry for the application folder, so the team replicated the scenario in a test environment. After making the change and testing that it does not affect the service, the same change was made in production. the service in production behaved as expected and the searches work correctly.

- Pipeline was updated with logrotate configuration for that feature to avoid problem again.

---

## Impact Description

`Exaple`

- 10/30/2021 between 9:46 AM (UTC-6) and 10:21 AM (UTC-6) The search service was not working

- Search service: it was not possible to carry out product searches.

- Other services was not affected