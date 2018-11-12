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

TBD

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
