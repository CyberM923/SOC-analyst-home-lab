SOC Investigation: Windows Network Connections

1. Objective

Investigate established TCP connections on a Windows endpoint, identify the processes responsible, and distinguish expected lab traffic from connections that require further investigation.

2. Lab Environment

* SIEM: Wazuh
* Endpoint: Windows 11 ARM64
* Telemetry: Sysmon and Wazuh agent
* Investigation tools: PowerShell and netstat
* Wazuh manager: 10.10.10.10
* Windows endpoint: 10.10.10.20

3. Investigation Procedure

Used PowerShell to list established TCP connections:

Get-NetTCPConnection -State Established

Then reviewed connection details, including local and remote addresses, ports, and owning process IDs:

Get-NetTCPConnection -State Established |
Select-Object LocalAddress,LocalPort,RemoteAddress,RemotePort,OwningProcess

Correlated the relevant process ID with a process name using:

Get-Process -Id 3872

4. Findings

Finding A: Wazuh Agent Communication

* Remote address: 10.10.10.10
* Remote port: 1514/TCP
* Owning process ID: 3872
* Process: Wazuh-agent

Assessment: Expected lab traffic. The connection matched the Wazuh agent communicating with the Wazuh manager.

Finding B: Unverified External Connection

* Remote address observed: 52.110.2.144
* Status: The connection disappeared before its owning process could be confirmed.

Assessment: Inconclusive. There was not enough evidence to determine the process responsible or whether the connection was suspicious. The address alone is not proof of malicious activity.

5. Conclusion

The investigation successfully identified expected SIEM agent traffic and demonstrated how to correlate a TCP connection with its owning process. A separate transient connection could not be verified, so it was documented as inconclusive rather than classified as malicious.

6. Skills Demonstrated

* Windows endpoint investigation
* TCP connection analysis
* PowerShell command-line investigation
* Process identification and correlation
* Evidence-based security assessment
* Clear documentation of findings and limitations

7. Potential Next Steps

* Capture the process ID and executable path if the external connection reappears.
* Review related Sysmon network-connection events, if configured and available.
* Correlate timestamps with Wazuh events before reaching a conclusion.

This investigation was conducted in an educational home lab. Findings are limited to the evidence collected during the exercise.
