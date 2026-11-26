# 06-Active-Response

## Objective

The objective of this phase was to implement an automated response capability within Wazuh.
The goal was to detect multiple failed SSH login attempts originating from the same source IP address and automatically block that source using Wazuh Active Response.

## Technologies Used

- Wazuh SIEM
- Wazuh Active Response
- Ubuntu Server 24.04
- OpenSSH
- Firewall-Drop Script
- Custom Wazuh Rules
- IPTables

## Threat Scenario

Repeated SSH authentication failures are commonly associated with password guessing and brute-force attacks.
To improve the defensive capabilities of the SOC lab, a custom detection rule was developed to identify multiple failed SSH login attempts from the same IP address within a short time frame.

## Custom Detection Rule

A custom Wazuh rule was created to detect:

- Three failed SSH login attempts
- From the same source IP
- Within 120 seconds

Rule ID: 100101

MITRE ATT&CK Technique: T1110 - Brute Force

## Validation

Three failed SSH authentication attempts were generated against the Ubuntu endpoint.

### Result:

✅ Custom rule triggered successfully

✅ Alert generated in Wazuh

✅ Source IP identified

✅ Potential brute-force activity detected

## Active Response Configuration

The active response script was configured to automatically block source IP addresses responsible for generating the SSH brute-force detection rule.

Configuration:
- Response Script: firewall-drop
- Location: local
- Trigger Rule: 100101

## Active Response Validation

After enabling Active Response, another sequence of failed SSH login attempts was generated.

When the custom rule fired:
- The firewall-drop script executed automatically.
- The attacker source IP was added to IPTables.
- Network connectivity between the Windows endpoint and Ubuntu endpoint was interrupted.

This confirmed that automated response was functioning correctly.

## Investigation Evidence

The following observations confirmed successful operation:
- Multiple SSH login failures detected.
- Active Response triggered.
- Host blocked by firewall-drop.
- ICMP connectivity lost.
- Source IP present within IPTables DROP rules.

## Recovery Procedure

After validation testing, the blocked IP address was removed from IPTables.
This restored communication between the Windows and Ubuntu endpoints and returned the environment to its normal state.

## Outcome

Successfully implemented automated incident response within the Wazuh SOC lab.

## Achievements:

✅ Developed custom SSH brute-force detection logic

✅ Generated a custom Wazuh alert

✅ Configured firewall-drop Active Response

✅ Automatically blocked malicious source IPs

✅ Validated IPTables integration

✅ Restored connectivity after testing

✅ Demonstrated automated threat containment

## Lessons Learned

- Learned how Wazuh Active Response operates.
- Developed a custom detection rule for SSH brute-force activity.
- Gained experience mapping detections to MITRE ATT&CK techniques.
- Automated incident containment using firewall-drop.
- Validated response actions through network testing.
- Improved understanding of detection and response workflows.


