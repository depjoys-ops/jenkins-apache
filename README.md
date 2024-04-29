# Jenkins Pipeline for Apache HTTP Server

This Jenkinsfile defines a pipeline that installs, starts, checks, stops, and verifies the status of the Apache HTTP Server. 

## Description

The Jenkins pipeline consists of the following stages:

1. **Install Apache**: Updates package lists and installs Apache HTTP Server.
2. **Check Started Apache**: Checks the status of the Apache service to verify it is started.
3. **Check Apache Logs**: Searches the Apache error log for 4xx and 5xx errors and displays a message if any errors are found.
4. **Stop Apache**: Stops the Apache service.
5. **Check Stopped Apache**: Checks the status of the Apache service again to verify it is stopped.

## Explanation

The pipeline provides more detailed output and handles errors more effectively, making it easier to troubleshoot any issues that may arise during the process.
