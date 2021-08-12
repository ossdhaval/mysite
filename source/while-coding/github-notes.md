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
- code owners are specific to branch and hence you have have different code owners per branch
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
