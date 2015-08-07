AWS Basics Using CloudFormation (Reference Demo)
=================================================

This project covers the basics of AWS's VPC, EC2 and ELB through the use of a
CloudFormation template.

This project does the following, all within a the template:

 * Sets up a new VPC, a NAT instance, one public, and one private subnet.
 * Creates 2 Apache instances running Amazon Linux behind an ELB.
 * Using user data, all 3 instances (including the NAT instance) are updated,
   and rebooted.
 * Also through user data, the 2 Apache instances have Apache installed on them,
   and their server ID is written to an index file.

The end result of this is that one can simply run `curl` on the ELB IP and get
a round-robin output of the server names.

Required Tools
---------------

`awscli` needs to be installed and properly configured with an IAM key and
secret. For more info, see https://github.com/aws/aws-cli.

The CloudFormation template has all the AMIs and `RegionMap` entries necessary
to run this template in either of the 3 US regions (`us-east-1`, `us-west-1`,
and `us-west-2`).

Running This Project
---------------------

To run this project yourself, just download the repo and run:

```
aws cloudformation create-stack --stack-name vcts-lab-stack \
  --template-body file:///full/path/to/project/cfn-stack.json
  --parameters ParameterKey=KeyPair,ParameterValue=KEYPAIRNAME \
  ParameterKey=SSHAllowIPAddress,ParameterValue=IPADDR/32
```

`aws cloudformation` expects the template `file://` URL to be a absolute path.
Also, `SSHAllowIPAddress` expects `IPADDR/32`. The explicit nature of the
constraint both serves to explain security group ACL syntax, and to reinforce
that this is a single-host entry.

The template can also be downloaded and uploaded through the CloudFormation UI.
Parameters will be prompted during the upload process.

Author
-------

Chris Marchesi <chrism@vancluevertech.com>

License
--------

This work is licensed under the Creative Commons Attribution 4.0 International
License, which can be found at:

http://creativecommons.org/licenses/by/4.0/legalcode

A full copy can also be found in the LICENSE file.
