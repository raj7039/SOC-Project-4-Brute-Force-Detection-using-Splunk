# SOC Project 4 – Brute Force Detection using Splunk

## Objective

Detect brute force login attempts using SSH logs in Splunk.

## Tools Used

* Splunk Enterprise
* Kali Linux

## SPL Query

password
| rex "for (invalid user )?(?<user>\w+)"
| stats count by user
| where count > 2

## Output

* fakeuser → 12 attempts
* rajvarma → 4 attempts

## Alert Logic

* Condition: Results > 0
* Time range: Last 15 minutes
* Schedule: Every 1 minute

## Note

Logs were static due to lab limitation, but detection logic is correct.

## Conclusion

Successfully detected brute force attack using Splunk.
# SOC-Project-4-Brute-Force-Detection-using-Splunk