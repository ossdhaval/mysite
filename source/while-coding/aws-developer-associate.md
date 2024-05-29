# AWS Developer associate (DVA-C02)

downloaded material at: /home/dhaval/docs/learning/tech/learning material/aws/developer associate certification/

# Understanding AWS account

When you open a new aws account, the user using which you create aws account becomes your `root` user. And each was account has an ID. Like, `805640060484`. Every other user(called IAM user) you create will be recognised in reference to this id. So for example, AWS recommends creating another user with `admin` privileges instead of root user for all further logins. So, when you want to use this admin user, you need to add the account ID along with user-name and password. While the root user doesn't need account id.

## IAM:
- IAM is a global service so there is no region to be selected
- first, you create a root account and set up aws account with it. After this, using that user or sharing creds with anyone is not recommended.
- AWS works on shared responsibility model where AWS is responsible for protecting and keeping AWS services safe but you(root user) is responsible to keep all the account users safe by creating proper password policies, enabling MFA etc.
### users and groups
- a single user can be part of multiple groups
- there can be users who are not part of any group
- groups can't contain other groups
- group is a set of users who we want to apply same policies
- Policies are group of permissions.

### user credentials
-  when you create a user, AWS doesn't ask to set a password by default. User is created without any security credentials
-  How user will be authenticated depends on what mode of interaction will the user be using to connect with AWS. There are three ways you can interact with AWS
  - AWS management console (password and MFA protected)
  - AWS CLI (access key)
  - AWS SDK (access key)
Like for example, if you allow user the access to the admin management console, aws will ask to set the password. While if the user is just going to interact with aws using CLI then admin can create an access key for the user. If the user is going to just use `codecommit` service to commit the code, then admin should just create SSH public key for the user.

### IAM policies
- a policy can be applied to a group or an individual user.
- policy applied to individual user is called `inline` policies
- Policy structure:
  ```json
  {
    "Version": "2023-03-23",
    "Id": "allowRootToS3",
    "Statement":
    [
      {
        "Sid": "1",
        "Effect": "Deny",
        "Principal":
        {
          "AWS": ["arn:aws:iam::34523532453:root"]
        },
        "Action":
        [
          "s3:GetObject",
          "s3:PutObject"
        ],
        "Resource":
        [
          "arn:aws:s3:::mybucket/*"
        ]
        "Condition": {
                  "NumericLessThanEquals": {"aws:MultiFactorAuthAge": "3600"}
        }
      }
    ]
  ```
  - condition is optional in a statement
- initially, in any new AWS account, there are no users, no groups. But there are predefined policies. Like `AdministratorAccess`.
- policies have permissions within them. Permissions are simply a list of actions/resources that are allowed or denied under that policy.
- password policy is under account settings for admin/root user. So, this will not be available for normal users. But MFA, is available under User profile -> security credetials, so it should be available to all the users not just admin/root.

### Roles

- While groups are for IAM users, the roles are for amazon services or users that are not authenticated by amazon IAM (for example, SAML, web identity by external providers etc)
- One role is created for one service only (one role one service)
- for exam only the roles or `aws services` are important
- when you create a role, you have to choose which service it may apply to. 
- You need to attach one or more permissions to a role

### AWS CLI

#### configuration
- cli needs an access key to be able to authenticate
- Root/admin user can create an access key for any user from the management console > IAM > users > select the user > security credentials > access key. From here the root/admin user can generate access key (every access key has a access key ID as well).

#### Cloudshell
- cloud shell is not available in all regions
- when you click on cloudshell icon on management console it opens a shell with the same credentials as the management console.
- You can create new files on cloudshell. These files will persist. Also, you can upload and download files to cloudshell.
- provide access key ID and key to the user
- user can install CLI on its machine and run `aws configure` on command line to configure the access key ID and access key

#### commands

- if a user doesn't have permissions to perform an action, the cli will simply returns a blank response.
- 

## EC2

### billing info and setup of budget 
- There are three important sections under this
  - budget: allows you to set budget
  - bills: shos you breakdown of the monthly bills
  - free tier: shows usage under free tier and whether the usage will exceed free tier allowed usage
- At the start budget and cost management is only available to the root user and not to any IAM users. Not even IAM users with admin policy access.
- to allow the IAM admin user the access to budget and cost management, the root user has to go to its account home page, and enable the `iam user and the role access to the billing information`.
- billing info page can show following info
  - monthly bill
  - breakdown of monthly bill by service and even more granular
 
### EC2
  -  elastic compute cloud = ec2
  -  covers services of EBS, ELB, ASG
  -  each instance has private and public IPs and corresponding DNS names for both
  -  for each OS, amazon creates an initial user. For amazon linux AMI, the default user is `ec2-user`. You can use this user when you want to ssh into the instance. 
  -  An ec2 instance config involves choosing:
    -  cpu
    - ram
    - storage (either `instance store` on the same EC2 hardware, or the network attached (EBS or EFS))
    - network: network speed, do you need static IP or not,
    - firewall: using security groups
    - Bootstrap script called `user data` (only configurable at the first launch)
    - remember that even a stopped instance will continue to be charged for attached resources like EBS and elastic ip if any.

### Security groups
  -  SG is a firewall around an ec2 instance.
  -  it consists of rules for inbound and outbound network traffic
  -  by default all inbound traffic is blocked and all outbound traffic is enabled for an EC2 instance that doesn't have an SG attached
  -  SG to EC2 is an many to many relation. One SG can be attached to multiple EC2 and a single EC2 can be assigned multiple SGs
  -  SGs are regione and VPC specific
  -  Tip: if you are trying to access an ec2 instance from outside (like using htttp, ss etc) and your request is timing out, then it is a problem with SG. But if your request is returning with `connection refused ` then it may be your application issue
  -  each SG rules are made up of `type`, `protocol`, `port`, `SOURCE ip`. Type is like SSH, HTTP, https etc, while the protocol is TCP
  -  a security group can also allow connections from and to other security groups. That is all the EC2 instances that have that SG attached to them.
  -  

### EC2 buying options
- EC2 is billed per second
- 3 Different ways to book a EC2 instance that will affect the final price. With each category a different type of discount is applied to EC2 instance price.
  - **On demand EC2 instances**: [pricing](https://aws.amazon.com/ec2/pricing/on-demand/)
  - savings plan: Savings Plans is a flexible pricing model that can help you reduce your bill by up to 72% compared to On-Demand prices, in exchange for a one- or three-year hourly spend commitment. AWS offers three types of Savings Plans: Compute Savings Plans, EC2 Instance Savings Plans, and Amazon SageMaker Savings Plans.
  - **Reserved instances**: Amazon EC2 Reserved Instances (RI) provide discount in return of a capacity reservation. Reservation can be either 1 year or 3 years.
  - **Spot instances** : Amazon EC2 Spot Instances let you take advantage of unused EC2 capacity in the AWS cloud and are available at a discount of up to 90% compared to On-Demand prices. These instances can be taken away any time. These are good for fault-tolerant, stateless operations.
- 2 ways to get reserved capacity or instance
  - **On-demand capacity reservation**: On-Demand Capacity Reservations enable you to reserve compute capacity for your EC2 instances in a specific Availability Zone for any duration. Capacity reservations mitigate against the risk of being unable to get On-Demand capacity in case of capacity constraints and ensure that you always have access to EC2 capacity when you need it, for as long as you need it. On-Demand Capacity Reservations are recommended for:
    - Business-critical events or workloads that require capacity assurance
    - Workloads that need to meet regulatory requirements for high availability
    - Disaster recovery
  - **Dedicated Host**: A Dedicated Host is a physical EC2 server fully dedicated for your use. Dedicated Hosts can help you reduce costs by allowing you to use your existing server-bound software licenses, including Windows Server, SQL Server, and SUSE Linux Enterprise Server (subject to your license terms). Dedicated Hosts can be purchased On-Demand (hourly) or can be purchased as part of Savings Plans. Dedicated Hosts are recommended for:
    - Users looking to save money on licensing costs
    - Workloads that need to run on dedicated physical servers
    - Users looking to offload host maintenance onto AWS, while controlling their maintenance event schedules to suit their business’s operational needs

## Storage options

### EBS

