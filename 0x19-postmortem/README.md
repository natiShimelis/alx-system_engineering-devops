
stmortem: June 13, 2024, Website Outage
Issue Summary
Duration: June 13, 2024, 10:15 AM - 12:45 PM (PST)
Impact: The main website experienced significant slowdowns and intermittent downtime. Approximately 75% of users were affected, encountering long load times and sporadic 500 Internal Server Errors.
Root Cause: A misconfiguration in the database connection pool, leading to resource exhaustion and cascading failures across the web servers.
Timeline
10:15 AM: Issue detected via automated monitoring alerts indicating increased error rates and response times.
10:20 AM: Initial investigation by on-call engineer focused on web server logs, identifying 500 errors.
10:35 AM: Database logs examined, revealing numerous connection timeout errors.
10:50 AM: Assumption made that database performance was degraded due to a sudden spike in traffic.
11:10 AM: Database performance metrics checked, showing no unusual spikes or resource limits reached.
11:30 AM: Incident escalated to the database administration team.
11:45 AM: Deeper investigation into database configuration and application logs.
12:15 PM: Root cause identified as a misconfigured database connection pool size in the application server settings.
12:30 PM: Configuration corrected and application servers restarted.
12:45 PM: Service restored, monitoring confirmed normal operation.
Root Cause and Resolution
Root Cause
The issue stemmed from a misconfiguration in the database connection pool settings in the application server. The connection pool was set to a maximum of 10 connections, which was insufficient to handle the typical load. As a result, all available connections were quickly exhausted, causing requests to time out and leading to cascading failures across the web servers. This configuration error was inadvertently introduced during a recent update aimed at optimizing database performance.

Resolution
To resolve the issue, the following steps were taken:

Identification of Misconfiguration: Through a detailed examination of the application server settings, the connection pool size was identified as the bottleneck.
Adjustment of Settings: The maximum connection pool size was increased from 10 to 100, aligning with the expected load and current hardware capabilities.
Server Restarts: All application servers were restarted to apply the new settings.
Monitoring Confirmation: Post-change monitoring ensured that the error rates and response times returned to normal levels, confirming the resolution of the issue.
Corrective and Preventative Measures
Improvements
Enhanced Monitoring: Implement more granular monitoring on database connection pool usage and thresholds to catch such misconfigurations early.
Configuration Management: Introduce stricter review processes for configuration changes, including automated validation against best practices.
Load Testing: Regularly perform load testing in staging environments to ensure configuration settings can handle peak traffic loads.
Tasks
Monitor Database Connections: Implement alerts for when database connection usage exceeds 80% of the configured pool size.
Automate Configuration Checks: Develop scripts to automatically validate configuration changes against a set of predefined rules before deployment.
Review and Update Documentation: Update internal documentation to reflect the importance of appropriate connection pool sizing and the potential impacts of misconfiguration.
Training: Conduct training sessions for the engineering team on best practices for database connection management and troubleshooting.
Post-incident Review: Schedule a post-incident review meeting to discuss the findings and preventative measures, ensuring all stakeholders are informed and aligned.
