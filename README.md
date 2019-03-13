Warning
==========
This is a work-in-progress beta stage role. Currently, tested on Ubuntu 18.04 and CentOS 7 on AWS EC2.

Ansible Role CloudWatch Agent
=========
This Ansible role installs and configures AWS CloudWatch Agent on AWS EC2 instances.

Requirements
------------

* AWS EC2 instance must have an IAM role that has policies to run AWS CloudWatch Agent.
* Create the file aws-cw-config.json in a path where Ansible can find it. Within this file, save your AWS CloudWatchAgent configuration in JSON format.

Role Variables
--------------


| Variable | Default Value | Description | Required? |
|----------|---------------|---------|-----------|
| cloudwatch_agent_username |  | The administrative user that should be the owner of the downloaded files. Typically same as remote_user. On Ubuntu it maybe ubuntu and CentOS it may be centos and Amazon Linux it may be ec2-user. | Yes |
| cloudwatch_agent_download_directory | | The location where the AWS CloudWatch Agent software has to be downloaded to.| Yes |
| cloudwatch_agent_download_url | | The URL from which Amazon CloudWatchAgent must be downloaded. This is automatically set by the role. But you can override it | No |

Example JSON file: aws-cw-config.json
-------------
```json

{
	"metrics": {
		"append_dimensions": {
			"AutoScalingGroupName": "${aws:AutoScalingGroupName}",
			"ImageId": "${aws:ImageId}",
			"InstanceId": "${aws:InstanceId}",
			"InstanceType": "${aws:InstanceType}"
		},
		"metrics_collected": {
			"cpu": {
				"measurement": [
					"cpu_usage_idle",
					"cpu_usage_iowait",
					"cpu_usage_user",
					"cpu_usage_system"
				],
				"metrics_collection_interval": 60,
				"resources": [
					"*"
				],
				"totalcpu": false
			},
			"disk": {
				"measurement": [
					"used_percent",
					"inodes_free"
				],
				"metrics_collection_interval": 60,
				"resources": [
					"*"
				]
			},
			"diskio": {
				"measurement": [
					"io_time"
				],
				"metrics_collection_interval": 60,
				"resources": [
					"*"
				]
			},
			"mem": {
				"measurement": [
					"mem_used_percent"
				],
				"metrics_collection_interval": 60
			},
			"swap": {
				"measurement": [
					"swap_used_percent"
				],
				"metrics_collection_interval": 60
			}
		}
	}
}

```

Example JSON for onPremise server:
```json
{
        "metrics": {
                "namespace": "my_custom_namespace",
                "metrics_collected": {
                        "cpu": {
                                "measurement": [
                                        "cpu_usage_idle",
                                        "cpu_usage_iowait",
                                        "cpu_usage_user",
                                        "cpu_usage_system"
                                ],
                                "metrics_collection_interval": 360,
                                "resources": [
                                        "*"
                                ],
                                "totalcpu": false
                        },
                        "disk": {
                                "measurement": [
                                        "used_percent",
                                        "inodes_free"
                                ],
                                "metrics_collection_interval": 360,
                                "resources": [
                                        "*"
                                ]
                        },
                        "diskio": {
                                "measurement": [
                                        "io_time"
                                ],
                                "metrics_collection_interval": 360,
                                "resources": [
                                        "*"
                                ]
                        },
                        "mem": {
                                "measurement": [
                                        "mem_used_percent"
                                ],
                                "metrics_collection_interval": 360
                        },
                        "swap": {
                                "measurement": [
                                        "swap_used_percent"
                                ],
                                "metrics_collection_interval": 360
                        }
                }
        }
}
```

For the list of metrics, see [AWS CloudWatchAgent Documentation](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/metrics-collected-by-CloudWatch-agent.html)

Example Playbook
----------------

```yml
    - hosts: cloudwatch-servers
      roles:
         - role: bngsudheer.aws-cloudwatch-agent
```


License
-------

BSD

Author Information
------------------

Sudheer Satyanarayana
* Blog: https://www.techchorus.net
* Twitter: https://www.twitter.com/bngsudheer
* Work: https://www.gavika.com
