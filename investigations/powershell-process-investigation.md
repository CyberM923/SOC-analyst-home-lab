SOC Investigation: PowerShell Process Activity

1. Objective

Examine Windows process-creation telemetry to understand PowerShell activity, identify parent-child process relationships, and assess whether the available evidence indicates suspicious behavior.

2. Lab Environment

* SIEM: Wazuh
* Endpoint: Windows 11 ARM64
* Telemetry: Sysmon
* Analysis platform: Wazuh Dashboard
* Investigation tools: PowerShell and Windows process information

3. Investigation Procedure

Reviewed Sysmon process-creation events in Wazuh, focusing on powershell.exe.

Examined available event fields, including:

* Process image and executable path
* Process ID
* Parent process ID and parent image
* User context
* Available command-line details

Used Windows process information to check whether the reported parent process was a PowerShell process.

4. Findings

The observed process-creation event identified:

* Child process: powershell.exe
* Child process ID: 9304
* Parent process ID: 6880
* Parent image: powershell.exe
* User context: vboxuser

The parent process ID was checked using Windows process information and was associated with a PowerShell process during the investigation.

The available command-line details showed powershell.exe without clearly suspicious arguments.

5. Assessment

The evidence was consistent with one PowerShell process launching another PowerShell process. However, the available information was not sufficient to determine the user’s intent or establish malicious activity.

A PowerShell-to-PowerShell parent-child relationship can occur during legitimate administration and automation, as well as during some attacks. Context is necessary to distinguish between them.

Conclusion: Inconclusive. No confirmed malicious behavior was established from the evidence collected.

6. Recommended Follow-up

If investigating this activity in a production environment, I would:

* Review the full command line and process ancestry.
* Correlate the event timestamp with related Sysmon and Windows security events.
* Check the user session and expected administrative activity.
* Review nearby network connections and file activity.
* Escalate only if additional evidence supports a suspicious conclusion.

7. Skills Demonstrated

* Sysmon process-creation event analysis
* Parent-child process investigation
* Windows process identification
* PowerShell activity review
* Evidence-based assessment
* Documentation of uncertainty and follow-up actions

This investigation was performed in an educational home lab. The conclusion is limited to the evidence available during the exercise.
