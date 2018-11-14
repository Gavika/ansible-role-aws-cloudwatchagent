Warning
==========
This is a work-in-progress alpha stage role.

Role Name
=========

This Ansible role installs and configures AWS CloudWatch Agent on AWS EC2 instances.

Requirements
------------

* AWS EC2 instance must have an IAM role that has policies to run AWS CloudWatch Agent.

Role Variables
--------------


| Variable | Default Value | Description | Required? |
|----------|---------------|---------|-----------|
| cloudwatch_agent_username |  | The administrative user that should be the owner of the downloaded files. Typically same as remote_user. On Ubuntu it maybe ubuntu and CentOS it may be centos and Amazon Linux it may be ec2-user. | Yes |
| cloudwatch_agent_download_directory | | The location where the AWS CloudWatch Agent software has to be downloaded to.| Yes |

Dependencies
------------

None

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: cloudwatch-servers
      roles:
         - role: bngsudheer.aws-cloudwatch-agent


License
-------

BSD

Author Information
------------------

Sudheer Satyanarayana
* Blog: https://www.techchorus.net
* Twitter: https://www.twitter.com/bngsudheer
* Work: https://www.gavika.com
