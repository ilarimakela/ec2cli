# ec2cli
Command Line Interface for AWS EC2 instances

The ec2cli package works on Bash. It's developed and tested with Mac OS X.
It requires working aws-cli https://github.com/aws/aws-cli/

## Installation
The easiest way to install ec2cli is to use `curl`:

    $ curl https://raw.githubusercontent.com/ilarimakela/ec2cli/master/ec2cli > /usr/local/bin/ec2cli
    $ chmod +x /usr/local/bin/ec2cli

## Getting started

Before using ec2cli, you need to install and configure aws-cli. It could be done in several ways. More detailed install instructions could be found from https://github.com/aws/aws-cli/ but here is quick quide:

    $ pip install aws-cli
    $ aws configure

You also need at least following IAM policy:

    {
        "Version": "2012-10-17",
        "Statement": [
            {
                "Sid": "Stmt1443794791000",
                "Effect": "Allow",
                "Action": "ec2:DescribeInstances",
                "Resource": "*"
            }
        ]
    }

ec2cli usage:

    $ ec2cli [OPTIONS] [pattern]
    AWS options:
      --profile       Use a specific profile from your credential file
      --region        Region to use
    Other options:
      --columns       Columns to show as comma separated list.
                      Default is "name,instanceid,instancetype" and "all" means all columns

If you have multiple aws configurations in ~/.aws/credentials, you could use --profile option. --region option is mandatory because aws-cli needs it but you could write it to ~/.aws/config so you don't need to specify it all the time.

    $ cat ~/.aws/config
    [profile default]
    region = eu-central-1

Pattern is a keyword to search instances. Without keyword ec2cli will return all instances. You could give multiple keywords to narrow down the results.

## Examples

To find all instances and default columns to shown

    $ /usr/local/bin/ec2cli

To find all instances which has name tag and are running in eu-central-1

    $ /usr/local/bin/ec2cli name running eu-central-1

To find running t2.micro instances which are part of opsworks stack

    $ /usr/local/bin/ec2cli --columns name,ami,status running t2.micro opsworks:stack

To find all running instances

    $ /usr/local/bin/ec2cli running

