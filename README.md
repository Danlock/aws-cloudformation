# aws-cloudformation
Cloudformation templates made for creating a robust and secure system on aws. Using private subnets, NAT gateways, different VPCs through cloudformation parameters, and made with a base from http://templates.cloudonaut.io/en/stable/. Thanks to Cloudonaut and Widdix.

### Order stacks should be brought up in:
1. Alarms
2. VPC
3. Elastic Beanstalk Application
4. SSH-Bastion
5. Databases
6. Route53 DNS
7. S3
8. Elastic Beanstalk Environment
9. Web App Firewall

### Tips
Stick to just using AWS cloudformation for certain services, because changing things using AWS GUI(console) and letting the cloudformation stacks get out of sync will lead to hard to diagnose problems.

The AWS CLI must be installed, and set with the right region and your API credentials before performing these cli commands.

Everytime the Elastic Beanstalk environment is changed in anyway that involves destroying the Application Load Balancers, for example a blue/green deployment, the web app firewall must be re updated to attach to the new Application Load Balancers!
Elastic Beanstalk cloudformation template doesn't seem to expose the arn of the load balancer it creates.

Notes on switching regions:
dns.yaml parameters rely on the sphinx environment and the ssh bastion stacks being created and their results manually passed in through parameters.
s3.yaml parameters need to create new buckets with the region inside the name of the bucket
waf.yaml parameters need to point to the new elastic beanstalk environment ALB
