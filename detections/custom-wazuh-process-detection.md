Custom Wazuh Detection: Sysmon Process Creation

1. Objective

Create and validate a custom Wazuh rule that identifies Windows Sysmon process-creation events, demonstrating basic detection engineering in a SOC home lab.

2. Lab Environment

* SIEM: Wazuh
* Manager: Ubuntu 24.04
* Monitored endpoint: Windows 11 ARM64
* Endpoint telemetry: Sysmon
* Event source: Microsoft-Windows-Sysmon/Operational

3. Detection Logic

Created a custom rule in Wazuh’s local rules configuration file:

/var/ossec/etc/rules/local_rules.xml

<group name="local,sysmon,">
  <rule id="100002" level="7">
    <if_sid>61634</if_sid>
    <description>SOC LAB - Sysmon Process Creation Detected</description>
  </rule>
</group>

Rule components:

* Rule ID: 100002
* Severity level: 7
* Parent rule: 61634
* Purpose: Generate a custom alert when an event matching the parent process-creation rule is received.

The rule relies on the built-in parent rule to identify the relevant event. It is a lab detection for process creation, not a determination that the process is malicious.

4. Validation Procedure

1. Added the custom rule to local_rules.xml.
2. Tested the Wazuh analysis configuration with:

sudo /var/ossec/bin/wazuh-analysisd -t

3. Confirmed the configuration test passed.
4. Restarted the Wazuh manager.
5. Launched Notepad on the Windows endpoint to generate a new process-creation event.
6. Searched the resulting events in the Wazuh Dashboard.

5. Result

A fresh Notepad process-creation event triggered custom rule 100002 and appeared in Wazuh Discover.

Outcome: Successful. The custom rule was validated against controlled lab activity.

6. Security Analyst Notes

Process creation telemetry can help analysts investigate:

* Unexpected executables
* Unusual parent-child process relationships
* Command-line arguments that may warrant review
* Processes launched from unusual locations

A process-creation alert alone does not prove malicious activity. Analysts should correlate it with command-line details, user context, timestamps, network events, and other available evidence.

7. Skills Demonstrated

* Wazuh rule configuration
* Sysmon telemetry analysis
* Detection logic and rule inheritance
* Configuration validation and service restart
* Controlled alert testing
* SIEM event review
* Evidence-based reporting

8. Future Improvements

* Add more specific conditions to reduce unnecessary alerts.
* Build and safely test detections for suspicious command-line patterns.
* Correlate process creation with network connections and other endpoint telemetry.
* Capture a screenshot of rule 100002 triggering in Wazuh Discover.

This detection was created and tested in an educational home lab using controlled activity.
