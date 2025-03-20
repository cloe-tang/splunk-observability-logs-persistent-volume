# splunk-observability-logs-persistent-volume
This is an experiment to test if Splunk collector deployed in kubernetes can retrieve logs from persistent volume. 

Scenario 1
 
Writer pod (simulate vault pod) writing logs to log file
Reader pod (simulate collector pod) reading the log file
 
Reprovisioned the writer pod while Reader pod is still running. When writer pod is up, reader pod read the new logs that is written to the file
 
Scenario 2
 
Writer pod (simulate vault pod) writing logs to log file
Collector pod reading and sending logs to Splunk enterprise
 
Reprovisioned the writer pod while collector pod is still running. When writer pod is up, reader pod read the new logs that is written to the file and send it to splunk enterprise
 
Scenario 3
 
Writer pod (simulate vault pod) writing logs to log file
Collector pod reading and sending logs to Splunk enterprise
 
Create the collector pod first then the writer pod. It is able to pick up the logs written by the writter pod      
