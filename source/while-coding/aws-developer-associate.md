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
