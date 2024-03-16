# AWS Developer associate (DVA-C02)

downloaded material at: /home/dhaval/docs/learning/tech/learning material/aws/developer associate certification/


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
- initially, in any new AWS account, there are no users, no groups. But there are predefined policies. Like `AdministratorAccess`.
- policies have permissions within them. Permissions are simply a list of actions/resources that are allowed or denied under that policy.
- 
