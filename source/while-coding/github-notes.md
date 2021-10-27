# Github notes

### setting up github commit signature verification:
- First check that your email id is verified:
  - go to github->user settings->emails->see if it mentions 'unverified' below your email id
  - ref [here](https://docs.github.com/en/github/getting-started-with-github/signing-up-for-github/verifying-your-email-address)
- Check if you have a GPG key (private-public key pair) already generated for this email id on your machine
  - `gpg --list-secret-keys --keyid-format LONG`
- if you don't have a key generate it
  - while generating the key, it'll ask for inputs, most of it is ok to keep default and email is your github (preferrably private, or public) email id.
  - `gpg --full-generate-key`
  - ref [here](https://docs.github.com/en/github/authenticating-to-github/managing-commit-signature-verification/generating-a-new-gpg-key)
- Now check the key that got generated
  - `gpg --list-secret-keys --keyid-format LONG`
  - output have a line similar to `sec   rsa4096/<your key> 2021-06-02 [SC]`
- Now, set GPG key in your local git client
  - `git config --global user.signingkey <your key>`
- Now we need to add same key to your github account
  - get public key block
    - `gpg --armor --export <your key>`
    - copy the entire text that got printed on your screen, starting from first '-' to last '-'
  - now go to github->profile->settings->SSH and GPG keys->New GPG key. Paste public key block that you copied in step above.
- after this whenever you want to sign a commit add `-S` flag
  - `git commit -S -m your commit message` 

- Troubleshooting:
  - Many times people face this error while trying to push to github.
  `commits must have valid signatures` 
  this error is saying that you are trying push commits that are unsigned. Many times people confuse it with commits that are already there in github. To solve this you have to find the unsinged commit and sign it. To see all commits with its signing information run `git log --show-signature`.
  - when you run `git log --show-signature`, you'll see that there are lot of red warnings which are like this.
      ```
      gpg: Signature made Monday 25 October 2021 10:10:36 PM IST
      gpg:                using RSA key 4AEE18F83AFDEB23
      gpg: Can't check signature: No public key
      Merge: 2880250f3 f5ec22d37
      Author: YuriyZ <yzabrovarniy@gmail.com>
      Date:   Mon Oct 25 19:40:36 2021 +0300

      ```
      it says `signature made` but no public key available. This is will be the case with commits signed by other members of your team. Because you don't have their public key stored with you. To do so, run `curl https://github.com/ossdhaval.gpg | gpg -import` to download key for user `ossdhaval`.
      
      

Above steps were derived from links given [here](https://docs.github.com/en/github/authenticating-to-github/managing-commit-signature-verification)

### issues vs PRs
  
  ##### Issues
  - Used for raising bug or feature requests or tracking large development work
  - Focus is around requesting, planning and tracking tasks and work

  ##### PRs
  - Used for tracking, discussing code changes 
  - Focus is on code and not planning or tracking work

### Linking issues and PRs

##### linking issues with issues
- do it with `issue mentions` or creating issues from `task lists`
##### issues with PRS
- in issue : do it with `linked PR` section on the right
- in PR : you can link issue by using key words like `closes`
- In both you can refer to an issue using number afte #
##### PRs with PRs

### Creating Issue and PR templates that apply to all the repos in org

If you want certain files to be set as default for all the repos under your org, you can create a `.github` repo. Github uses files under this repo as default. Reference [here](https://docs.github.com/en/communities/setting-up-your-project-for-healthy-contributions/creating-a-default-community-health-file)

##### Issue template

- creat a new repo `.github` in org github account
- To create a new template called `development-item`, create a new file as `.github/ISSUE_TEMPLATE/development-item.md`. This will create two new folders and one file. 
- Put below header in the file and then start writting your contents for template.
  ```
  ---
  name: Contribution item
  about: Developers should use this when contributing a feature or bug fix
  title: ''
  labels: ''
  assignees: ''

  ---
  
  ```
- create another template in `ISSUE_TEMPLATE` directory in similar way. For example `feature-request.md`
- You may have to enable templates from `settings` of `.github` repo as well. But not sure if this step is required. Ideally, after the first step, whenever you create a new issue, git hub should first show you a screen to select the issue template.

##### PR template
- Create a PR template file named `pull_request_template.md` under `.github` repository root folder. 
- Not tried: if you have more than one pull request templates, you should put it under `PULL_REQUEST_TEMPLATES` folder



reference [here](https://docs.github.com/en/communities/using-templates-to-encourage-useful-issues-and-pull-requests/about-issue-and-pull-request-templates).


### code owners
- you can define code owners by creating `CODEOWNERS` file in target branch.
- code owners are specific to branch and hence you can have different code owners per branch
- There are two things that code owners file can help with 
  1) when you raise a pull request, the code owners as defined in base branch will get review requests
  2) when you have turned on branch protection for that branch from `settings` of repo, you can require approval from code owner of that branch for all PRs before merging.


### Repository defaults
- you can define following as default for every new repository in your org
  - Labels
  - default branch name
- this can be done from organization settings -> repository defaults


### Security

- have SECURITY.md in .github repository at org level, like [this](https://github.com/falcosecurity/.github/blob/master/SECURITY.md)
- enable security advisory in github, like [this](https://github.com/falcosecurity/.github/security)
- Enable Dependabot scanning
- read process around [security vulnerability reporting](https://docs.github.com/en/code-security/security-advisories/about-github-security-advisories)
- [Best practices](https://docs.github.com/en/code-security/security-advisories/about-coordinated-disclosure-of-security-vulnerabilities)


### Labelling :

- [good artice](https://seantrane.com/posts/logical-colorful-github-labels-18230/#:~:text=Issue%2FPR%20labels%20should%20only,intuitive%20at%2Da%2Dglance.)
- [good discussion about maintaining labels](https://github.com/kubernetes/community/issues/2032)
- check this [labeler](https://github.com/actions/labeler)


### github api:

you can get programatic access to github data using rest api. For example, to get all repositories in JanssenProject org:

```
curl  https://api.github.com/orgs/JanssenProject/repos
```


### using github rest api

Till version 3, github had rest apis but from version 4 they have moved to GraphQL. 

#### using version 4 (graphQL api)
Reference : https://docs.github.com/en/graphql
public schema: https://docs.github.com/en/graphql/overview/public-schema
how to use without explorer: https://docs.github.com/en/graphql/guides/forming-calls-with-graphql
how to use : https://docs.github.com/en/graphql/guides/using-the-explorer
explorer url: https://docs.github.com/en/graphql/overview/explorer


#### using rest API

all APIs are listed https://docs.github.com/en/rest/reference

you can access public data without authenticating. For example:

```
curl https://api.github.com/users/ossdhaval
```

but to access some information plus to make changes to github data you have to authenticate.


##### authentication

Your regular ssh key will not work. You have to get an OAuth key or [generate a personal token](https://docs.github.com/en/github/authenticating-to-github/keeping-your-account-and-data-secure/creating-a-personal-access-token).

Then you can fire command using curl

```
curl -u ossdhaval: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 -H "Accept: application/vnd.github.zzzax-preview+json" https://api.github.com/repos/ossdhaval/gitcheck/branches/main/protection/required_signatures
```

### Useful Tools 
- for analysing github data of your org and multiple repos: https://livablesoftware.com/tools-mine-analyze-github-git-software-data/
- Agile project management on github: https://www.zenhub.com/

### github repository permission levels
https://docs.github.com/en/organizations/managing-access-to-your-organizations-repositories/repository-permission-levels-for-an-organization

### github change log (audit log)
you can see all the changes that happend to all the entites in your organisation in github using audit logs. You need to be organization `owner` to
be able to see this.
https://docs.github.com/en/organizations/keeping-your-organization-secure/reviewing-the-audit-log-for-your-organization#accessing-the-audit-log


### branch protections

- `Require status checks to pass before merging`
  - at this time, when you turn on this protection, only statuses that were run in last week will be available for selection in the search box. so if there is an active status check but corresponding workflow did not run during last week then that status check will not be available for selection
  - name of the status check is the name of the job within workflow or externally injected status
- only jobs from those workflow will be appear in search selection box which get triggered on [pull-request] event

a good link for troubleshooting: 
https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/defining-the-mergeability-of-pull-requests/troubleshooting-required-status-checks

### useful shortcuts

- `e`	Open source code file in the Edit file tab
- `ctrl+s` write commit message

[full list](https://docs.github.com/en/get-started/using-github/keyboard-shortcuts#about-keyboard-shortcuts)
