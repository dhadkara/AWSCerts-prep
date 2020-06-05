## CloudWatch

- AWS CloudWatch monitors AWS resources and applications in real-time
- Can be used __on-prem__ too by installing SSM and cloudwatch agent on servers

#### CloudWatch and EC2

Host Level metrics consists of 
- CPU
- Network
- Disk I/O
- Status Check

__Exam Tip__ RAM Utilization is custom metric. By default EC2 monitoring is __5mins called standard monitoring__ and can be reduced __upto 1min called detailed monitoring__ . Min for custom metrics is 1 min

#### CloudWatch Logs

Logs Groups will keep the logs data __indefinately__ unless you change it. You can also retrieve data from terminated EC2 or ELB instance.

#### CloudWatch Alarms

- Alarm can be created to monitor any cloudwatch metrics in your account e.g. CPU utilizaton, ELB Latency etc.
- Can set threshold on these alarms to set actions if alarm status reach
- Alarm history is kept for __14 days__
- An alarm has three possible states:

  __OK__—The metric is within the defined threshold
  __ALARM__—The metric is outside of the defined threshold
  __INSUFFICIENT_DATA__—Alarm has just started, the metric is not available, or not enough data is available for the metric to determine the alarm state

- We are excited to announce that CloudWatch now supports __High-Resolution Custom Metrics and Alarms__, enabling you to monitor custom applications and infrastructure in near real-time, down to per-second resolution. Using the existing __PutMetricData API__, you can now publish Custom Metrics down to 1-second resolution. 

-----------------------
## CloudTrail
- CloudTrail provides visibility into user activity by recording actions taken on your account. API history enables security analysis, resource change tracking, and compliance auditing.
- CloudTrail records account activity and service events from most AWS services and logs the following records:
  - The identity of the API caller.
  - The time of the API call.
  - The source IP address of the API caller.
  - The request parameters.
  - The response elements returned by the AWS service.
- CloudTrail is enabled on your AWS account when you create it.

------------------------
