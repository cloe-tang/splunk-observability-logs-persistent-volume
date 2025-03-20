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

## Scenario 2

Step 1: Create PV

<img width="263" alt="image" src="https://github.com/user-attachments/assets/468f2aec-85fc-40a2-8b59-bfbec3f54091" />

Step 2: Create PVC

<img width="288" alt="image" src="https://github.com/user-attachments/assets/bd03ea6c-95ea-4ea4-84d9-bbbf487e1999" />

Step 3: Create writer pod using the above PVC

<img width="748" alt="image" src="https://github.com/user-attachments/assets/1c311f19-dd99-4044-af6b-1e8f818ef797" />

Step 4: Create Splunk Otel collector pod

<img width="677" alt="image" src="https://github.com/user-attachments/assets/ef7f19d6-acf5-429c-9626-ef52c5a7994a" />

![image](https://github.com/user-attachments/assets/cbecd46b-bdd4-4f07-a3bd-363ec833e940)

Step 5: In Splunk Enterprise, logs are indexed

<img width="631" alt="image" src="https://github.com/user-attachments/assets/0471354e-3a8d-46e8-a5f6-861d498549c4" />

Step 6: Delete the writer pod

<img width="530" alt="image" src="https://github.com/user-attachments/assets/a7169c09-1648-4cab-9535-56363465d61b" />

Step 7: Recreate the writer pod with different log to differentiate

<img width="796" alt="image" src="https://github.com/user-attachments/assets/3963f0b5-2d24-4040-b692-c7b4d9a1425b" />

Step 8: Read the logs in the mount path. Reflecting the new logs

<img width="806" alt="image" src="https://github.com/user-attachments/assets/98388cc1-57dd-498a-91de-06f3c0663333" />

Step 9: Also seeing the new logs in the Splunk enterprise security

<img width="813" alt="image" src="https://github.com/user-attachments/assets/c1eb6ffb-8c29-4b54-afd7-95c1798553d5" />






