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

## Pre-requisites

If you are running in local, install minikube or similar tools

## Scenario 1

Step 1: Create PV

<img width="315" alt="image" src="https://github.com/user-attachments/assets/c5b1d2f5-ea2b-44f0-9001-855bc686f72d" />

Step 2: Create PVC

<img width="272" alt="image" src="https://github.com/user-attachments/assets/3a1d4690-983e-43de-abc1-6a84168ee7ba" />

Step 3: Create write pod using the above PVC

<img width="543" alt="image" src="https://github.com/user-attachments/assets/4148d9b3-c243-4363-8ac1-d23cb0542272" />

Step 4: Create reader pods using the same PVC

<img width="521" alt="image" src="https://github.com/user-attachments/assets/4e2edb89-bdcd-4013-bac3-683e104fcf25" />

Step 5: Able to read the txt file written on the mount path

<img width="451" alt="image" src="https://github.com/user-attachments/assets/2b4dd94a-dd03-4a98-adf2-8e8b101b368f" />

Step 6: Dete the writer pod. Reader pod is still able to read the file

<img width="451" alt="image" src="https://github.com/user-attachments/assets/870accbb-0073-4eab-9ecc-c23683140029" />

Step 7: When writer pod recreated, reader pod is still able to see the file

<img width="446" alt="image" src="https://github.com/user-attachments/assets/e380e628-6e3a-4805-9269-bb1234e32d62" />






