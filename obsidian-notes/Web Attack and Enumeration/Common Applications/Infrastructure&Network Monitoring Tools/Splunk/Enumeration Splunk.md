
We can discover Splunk with a quick Nmap service scan. `Splunkd httpd` service on port 8000 and port 8089, the Splunk management port for communication with the Splunk REST API.

Splunk has multiple ways of running code, such as server-side Django applications, REST endpoints, scripted inputs, and alerting scripts. A common method of gaining remote code execution on a Splunk server is through the use of a scripted input.

As Splunk can be installed on Windows or Linux hosts, scripted inputs can be created to run Bash, PowerShell, or Batch scripts.

Also, every Splunk installation comes with Python installed, so Python scripts can be run on any Splunk system.

