Ansible Role: AWS CloudWatch Agent
=========
This Ansible role installs and configures AWS CloudWatch Agent on AWS EC2 instances
and on-premise servers.

Requirements
------------
* An AWS EC2 instance or an on-premise Linux server
* If using AWS EC2 instance, the instance must have an IAM role attached that has policies to run AWS CloudWatch Agent. Consider using the AWS provided policy - CloudWatchAgentServerPolicy.
* If using on-premise server, configure /root/.aws/credentials and /root/.aws/config.
* Provide the YAML variable `aws_cloudwatch_agent_config`. This will be converted into JSON. See defaults/main.yml for a basic configuration.

Role Variables
--------------

| Variable | Default Value | Description | Required? |
|----------|---------------|---------|-----------|
| aws_cloudwatch_agent_username |  | The administrative user that should be the owner of the downloaded files. Typically same as remote_user. On Ubuntu it maybe `ubuntu` and CentOS it may be `centos` and on Amazon Linux it may be `ec2-user`. The role guesses the username based on OS if not set explicitly. | No |
| aws_cloudwatch_agent_download_directory | | The location where the AWS CloudWatch Agent software has to be downloaded to. The role guesses the location based on OS if not set explicitly. | No |
| aws_cloudwatch_agent_download_url | | The URL from which Amazon CloudWatchAgent must be downloaded. This is automatically set by the role. But you can override it. | No |
| aws_cloudwatch_agent_mode | ec2 | The AWS CloudWatch Agent mode. Can be one of `ec2`, `onPremise` and `auto` | No |

Example JSON file: aws-cw-config.json
-------------
```yaml

agent:
    metrics_collection_interval: 60
    run_as_user: "cwagent"
metrics:
    namespace: "Gavika"
    append_dimensions:
      InstanceId: "${aws:InstanceId}"
    metrics_collected:
      disk:
        measurement:
          - used_percent
        metrics_collection_interval: 60
        resources:
          - "*"
      mem:
        measurement:
          - mem_used_percent
        metrics_collection_interval: 60
```


Example /root/.aws/credentials for on-premise server:
```
[AmazonCloudWatchAgent]
aws_access_key_id = youaccesskeyid
aws_secret_access_key = yoursecretkey

```
Example /root/.aws/config for on-premise server:
```
[AmazonCloudWatchAgent]
region = us-east-1
```

For the list of metrics, see [AWS CloudWatchAgent Documentation](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/metrics-collected-by-CloudWatch-agent.html)

Example Playbook
----------------

```yml
    - hosts: cloudwatch-servers
      roles:
         - role: Gavika.aws-cloudwatch-agent
```


Continuous Integration
-----------------------
You can execute molecule tests locally.

License
-------

Apache2

Author Information
------------------

Sudheer Satyanarayana
* Blog: https://www.techchorus.net
* Twitter: https://www.twitter.com/bngsudheer


Gavika
* https://www.gavika.com
