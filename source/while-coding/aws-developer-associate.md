# AWS Developer associate (DVA-C02)

downloaded material at: /home/dhaval/docs/learning/tech/learning material/aws/developer associate certification/

# Understanding AWS account

When you open a new aws account, the user using which you create aws account becomes your `root` user. And each was account has an ID. Like, `805640060484`. Every other user(called IAM user) you create will be recognised in reference to this id. So for example, AWS recommends creating another user with `admin` privileges instead of root user for all further logins. So, when you want to use this admin user, you need to add the account ID along with user-name and password. While the root user doesn't need account id.

## IAM:
- IAM is a global service so there is no region to be selected
- first, you create a root account and set up aws account with it. After this, using that user or sharing creds with anyone is not recommended.
### users and groups
- a single user can be part of multiple groups
- there can be users who are not part of any group
- groups can't contain other groups

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
      }
    ]
  ```
- initially, in any new AWS account, there are no users, no groups. But there are predefined policies. Like `AdministratorAccess`.
- policies have permissions within them. Permissions are simply a list of actions/resources that are allowed or denied under that policy.
- password policy is under account settings for admin/root user. So, this will not be available for normal users. But MFA, is available under User profile -> security credetials, so it should be available to all the users not just admin/root.

### AWS CLI

#### configuration
- cli needs an access key to be able to authenticate
- Root/admin user can create an access key for any user from the management console > IAM > users > select the user > security credentials > access key. From here the root/admin user can generate access key (every access key has a access key ID as well).
- provide access key ID and key to the user
- user can install CLI on its machine and run `aws configure` on command line to configure the access key ID and access key

#### commands

- if a user doesn't have permissions to perform an action, the cli will simply returns a blank response.
- 
