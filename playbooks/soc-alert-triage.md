SOC Alert Triage Playbook

Purpose

This playbook documents a repeatable process for reviewing security alerts, validating evidence, assessing risk, and determining appropriate next steps.

1. Alert Intake

* Identify the alert source, timestamp, affected endpoint, user, and detection rule.
* Review the alert description and severity.
* Record the initial evidence before making changes.

2. Validate the Alert

* Open the associated event in the SIEM.
* Review the relevant event fields and confirm the detection logic.
* Determine whether the activity is expected, suspicious, or inconclusive.
* Do not treat an alert by itself as proof of compromise.

3. Collect Context

For Windows process alerts:

* Review the executable name and full path.
* Examine the process ID and parent-child relationship.
* Review command-line arguments and user context when available.
* Correlate related Sysmon and Windows events.

For network connection alerts:

* Identify the local and remote addresses and ports.
* Determine which process owns the connection.
* Compare the activity with expected lab or business operations.
* Investigate additional context before labeling an external connection malicious.

4. Assess Risk

Consider:

* Whether the activity is expected for the user and endpoint
* The reputation and location of the executable
* The parent process and command-line details
* Related network or file activity
* Whether other alerts or events support the same concern

Use evidence to distinguish a likely benign event from a suspicious or unresolved one.

5. Decide on Next Steps

* Likely benign: Document the evidence and close according to the applicable process.
* Suspicious: Collect additional evidence and escalate according to organizational procedures.
* Inconclusive: Record what is known, identify evidence gaps, and recommend further investigation.

Do not isolate systems, delete files, or terminate processes without appropriate authorization and an approved response procedure.

6. Document the Investigation

Record:

* Alert name and timestamp
* Affected endpoint and user
* Relevant process and network details
* Evidence reviewed
* Assessment and rationale
* Actions taken
* Recommended follow-up

7. Home Lab Example

In this lab, Wazuh custom rule 100002 detected a Sysmon process-creation event. The event was reviewed in Wazuh Discover and documented as evidence that the detection worked.

A separate network investigation identified expected Wazuh agent communication to the lab manager on TCP port 1514. Another transient external connection could not be verified, so it remained inconclusive rather than being classified as malicious.

Skills Demonstrated

* SIEM alert triage
* Event validation and correlation
* Windows process investigation
* Network connection analysis
* Risk-based assessment
* Evidence documentation
* Responsible escalation decisions

This playbook is an educational reference for a home lab. Real incidents should follow the employer’s policies, escalation paths, and approved response procedures.
