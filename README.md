# AWS-CloudWatch-Synthetics-Monitoring

## HumanGov: Implementing AWS Cloud Watch Synthetics for Real-Time Application URL Monitoring Integrated with CloudWatch Alarms, SNS, and AWS Chatbot to Send Real-Time Alerts on Slack.
<p align="center">
<img src="https://i.imgur.com/6tBcdmy.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

## Project Description:
This project focuses on implementing monitoring and observability for the HumanGov application, which is deployed in two Kubernetes clusters, one in Florida and another in California. As part of the SRE (Site Reliability Engineering) team, the goal is to ensure that the application is monitored 24/7 and that the team receives real-time notifications whenever there is an issue. AWS services such as CloudWatch, SNS, and Chatbot are utilized to automate alerts that are sent to a Slack channel for immediate action. Additionally, AWS CloudWatch Synthetics Canaries are used to simulate user interactions with the application, ensuring its availability and performance.

## Project Objectives
1. Enable proactive monitoring of the HumanGov application across multiple regions (Florida and California).
2. Set up CloudWatch Synthetics Canaries to monitor the application URLs and alert the team of any downtime or performance degradation.
3. Configure CloudWatch alarms to detect issues and trigger alerts.
4. Use SNS and AWS Chatbot to notify the SRE team via Slack when problems are detected.
5. Ensure 24/7 observability and create a clear, actionable response plan for potential failures.

## Tools and Technologies
- **AWS Elastic Kubernetes Service (EKS)**: Hosts the HumanGov application.
- **AWS CloudWatch**: Monitors the application's health and performance.
- **AWS CloudWatch Synthetics**: Simulates user interactions with the application to check availability.
- **AWS SNS (Simple Notification Service)**: Routes CloudWatch alarms to notifications.
- **AWS Chatbot**: Delivers notifications to the SRE team's Slack channel.
- **Slack**: Receives real-time alerts for monitoring failures.
- **AWS Certificate Manager**: Manages SSL certificates for secure communication.
- **Cloud 9**: Development environment for implementing AWS solutions.

## Project Solution
The project solution involved setting up a comprehensive monitoring and alerting system for the HumanGov application, which is deployed across Kubernetes clusters in multiple regions. The solution integrates AWS services such as CloudWatch, SNS, and Chatbot to ensure that the SRE team is notified of any potential issues in real time. Here's how the solution was implemented:

### 1. EKS Cluster and Application Setup:
- The HumanGov application is deployed in two distinct Kubernetes clusters hosted in AWS, one in the California region and the other in Florida. These clusters are managed by AWS Elastic Kubernetes Service (EKS).
- The application is served through domain names associated with each region (e.g., california.human.gov.click for California and florida.human.gov.click for Florida).
- SSL certificates are managed through AWS Certificate Manager to ensure secure connections.

### 2. CloudWatch Synthetics for Monitoring:
- AWS CloudWatch Synthetics Canaries were set up to simulate user interactions with the application by regularly pinging the URLs for the California and Florida deployments.
- Canaries were created for both environments (humangov-canary-CA and humangov-canary-FL), set to run every minute to check if the application URLs are accessible and performing as expected.
- Each canary captures a screenshot on every run, providing visual confirmation of the application's availability and functionality.
- If the canary fails (e.g., the application is unavailable), a CloudWatch alarm is triggered.

### 3. CloudWatch Alarms for Alerting:
- CloudWatch alarms were configured to monitor the health of the Synthetics canaries.
- The alarm triggers if a canary fails for a specific time period (set to 1 minute) and sends an alert to the SRE team.
- Alarms were also configured to notify when the application fails a certain number of times consecutively, ensuring that both short-term and persistent issues are detected.

### 4. AWS SNS for Notification Routing:
- An SNS topic (humangov-chatbot.notification) was created to handle notification routing.
- This topic receives notifications from CloudWatch alarms and forwards them to AWS Chatbot, which is integrated with the SRE team's Slack channel.

### 5. AWS Chatbot Integration with Slack:
- AWS Chatbot was set up and linked to the SRE team's Slack channel. The Slack integration allows real-time alerts from CloudWatch to be delivered directly to the team.
- Notifications contain detailed information about the failure, including links to the affected resources and canary results, enabling the SRE team to quickly investigate and respond.

### 6. Testing and Verification:
- After configuring the monitoring and alerting system, various test scenarios were conducted, such as deliberately causing downtime for the application.
- The tests verified that canaries detected the issues, alarms were triggered, and Slack notifications were delivered to the SRE team promptly.
- Screenshots of the canary runs provided visual evidence of the failure, helping the team identify the root cause of the issue quickly.

The project solution ensures that the HumanGov application is monitored continuously, and any issues are automatically flagged and communicated to the SRE team through an efficient notification pipeline. This approach minimizes downtime, improves application reliability, and provides actionable insights for the team to resolve issues before they impact end-users.

## Step-by-Step Directions
### 1. Verify EKS Cluster and Application Deployment: 
Ensure that the EKS cluster named humangov-cluster is up and running with the HumanGov application deployed in both California and Florida regions.
<p align="center">
<img src="https://i.imgur.com/ZGmbJAJ.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

### 2. Create SNS Topic for Synthetics:
- Navigate to the AWS Console.
- Access the SNS service.
- Create a new SNS topic named humangov-chatbot-notifications.
<p align="center">
<img src="https://i.imgur.com/WgY9cph.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

### 3. Create Heartbeat Canary for URL Monitoring:
- Access the CloudWatch service in the AWS Console.
- Navigate to Synthetics Canaries.
- Create a new canary for California and repeat process for Florida applications:
<p align="center">
<img src="https://i.imgur.com/RSRApSY.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

- Name the canary (e.g., humangov-canary).
<p align="center">
<img src="https://i.imgur.com/s2PlOeK.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

- Choose "Use heartbeat monitoring".
<p align="center">
<img src="https://i.imgur.com/u12lVRy.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

- Input the monitoring URLs (e.g., https://california.cloudspecialist.click/).
<p align="center">
<img src="https://i.imgur.com/1YfkGr7.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

- Set the execution frequency (e.g., every minute).
<p align="center">
<img src="https://i.imgur.com/Qbt0oeU.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

### 4. Integrate with AWS Chatbot for Slack Notifications:
- Navigate to the AWS Chatbot service in the AWS Console.
<p align="center">
<img src="https://i.imgur.com/Vp75Yhj.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

- Configure AWS Chatbot to connect to Slack workspace.
<p align="center">
<img src="https://i.imgur.com/MIZ1OoH.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

- Attach the SNS topic humangov-chatbot-notifications to the Slack channel.
<p align="center">
<img src="https://i.imgur.com/sAIUxj9.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

- Verify the integration by sending a test notification to Slack.
<p align="center">
<img src="https://i.imgur.com/GR1oHBS.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

### 5. Test the Setup:
- Run the CloudWatch Synthetics canaries.
<p align="center">
<img src="https://i.imgur.com/IZnnHeL.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

- Confirm that the alarms activate as expected.
<p align="center">
<img src="https://i.imgur.com/7MmQg2F.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

### 6. Simulate Application Down Scenario:
- Use kubectl to scale down the nginx deployment for the California application to 0 replicas.
<p align="center">
<img src="https://i.imgur.com/R1RKmLE.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

- Observe the canary reporting the failure and triggering alarms.
<p align="center">
<img src="https://i.imgur.com/X9T9cbW.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

<p align="center">
<img src="https://i.imgur.com/QrxU5uS.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

- Verify that Slack receives the alert from AWS Chatbot.
<p align="center">
<img src="https://i.imgur.com/SBzfBXU.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

### 7. Simulate Application Up & Running Scenario:
- Use kubectl to scale down the nginx deployment for the California application to 1 replicas.
<p align="center">
<img src="https://i.imgur.com/f0GEprQ.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

<p align="center">
<img src="https://i.imgur.com/a5amglt.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

<p align="center">
<img src="https://i.imgur.com/cGtBcZQ.png" height="80%" width="80%" alt="Pic"/>
<br />
<br />

## Project Conclusion

By implementing AWS CloudWatch Synthetics Canaries and configuring AWS Chatbot to notify the SRE team via Slack, this project enables 24/7 observability for the HumanGov application. The solution ensures that downtime or performance issues are detected and addressed before users notice, enhancing the reliability of the service. The automated alerts allow the SRE team to act quickly on issues, minimizing the impact on the application's availability.

## Challenges Encountered

1. **Integrating Slack with AWS Chatbot**: Setting up a new Slack workspace and configuring the proper permissions took some time.
2. **Monitoring Frequency**: Deciding on the correct frequency for the canary tests required balancing between getting timely alerts and avoiding too many unnecessary notifications.

## Lessons Learned

1. **Proactive Monitoring is Critical**: The use of CloudWatch Synthetics allowed us to proactively identify and fix issues before they affected users, showcasing the importance of monitoring in a production environment.
2. **Automating Alerts Saves Time**: By automating alerts and sending them directly to Slack, the team can respond faster and more effectively to problems.
3. **Granularity of Monitoring**: It's essential to find the right granularity in monitoring, especially with alarms and alerts, to avoid alert fatigue while ensuring timely notifications.

## Future Improvements

1. **Advanced Monitoring Blueprints**: In the future, more advanced canary blueprints (e.g., GUI workflow builders) can be explored for testing user interactions beyond simple URL checks.
2. **Integration with Incident Management Tools**: Integrating AWS notifications with incident management tools (e.g., PagerDuty) could further streamline the response process.
3. **Multi-region Monitoring Enhancements**: Additional regions could be added to enhance redundancy and monitoring for larger-scale deployments across more than two states.

This wraps up the hands-on project for monitoring the HumanGov application using AWS monitoring and notification services.
