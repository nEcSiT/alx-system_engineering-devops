The NexShop web application was entirely down during this period. Users attempting to accePostmortem: Outage on NexShop Web Application
Issue Summary
Duration: The outage lasted for 2 hours and 15 minutes, starting from 14:00 GMT to 16:15 GMT.
Impacss the service were met with a "502 Bad Gateway" error. Approximately 80% of our user base, primarily in the Accra region, were affected, unable to search for nearby shops or retrieve directions.
Root Cause: The root cause was a misconfiguration in the Nginx server that handled traffic between the front-end and the back-end services.


Timeline
14:00 GMT: Issue detected by automated monitoring alert indicating a significant spike in 502 errors.
14:05 GMT: Initial investigation began, focusing on the database performance as it seemed to coincide with a recent update.
14:25 GMT: Misleading path—database performance was ruled out after thorough checks.
14:40 GMT: The investigation shifted to the API gateway. Logs showed multiple failed attempts to connect to the backend service.
15:00 GMT: Escalated to the DevOps team after identifying potential issues in the API gateway.
15:30 GMT: The DevOps team discovered a misconfiguration in the Nginx server’s upstream settings.
15:50 GMT: Configuration was corrected, and services were gradually restored.
16:15 GMT: Full recovery confirmed, and the application was fully operational.


Root Cause and Resolution
The issue stemmed from a misconfiguration in the Nginx server, specifically in the upstream directive, which caused improper routing of traffic between the front-end and back-end services. This misconfiguration was introduced during a recent update to the server configurations, where a typo in the IP address led to failed connections.
To resolve the issue, the DevOps team corrected the Nginx configuration file by updating the IP address to the correct one and reloaded the Nginx server. The service was tested rigorously post-fix to ensure no further issues remained.
Corrective and Preventative Measures


Improvements:
Configuration Management: We need to improve our configuration management processes to avoid such errors in the future.
Automated Testing: Implement automated testing for server configuration changes before they go live.
Enhanced Monitoring: Increase the granularity of our monitoring to detect and alert on similar configuration issues more quickly.
Tasks:
Implement a review process for any changes to server configurations.
Add unit tests for critical server configuration files.
Deploy additional monitoring to check the health of the Nginx server post-deployment.
Schedule training sessions for the team on best practices for server configuration and management.
