# Release Please : Github Release automation tool from Google

## Configuring release-please on a spring-boot project

1. Create a `.github/workflows/release-please.yml`
2. Add these contents to that file
   ```
   on:
    push:
      branches:
        - main
  
   permissions:
     contents: write
     pull-requests: write
  
   name: release-please
  
   jobs:
     release-please:
       runs-on: ubuntu-latest
       steps:
         - uses: googleapis/release-please-action@v4
           with:
             # this assumes that you have created a personal access token
             # (PAT) and configured it as a GitHub action secret named
             # `MY_RELEASE_PLEASE_TOKEN` (this secret name is not important).
             token: ${{ secrets.MY_RELEASE_PLEASE_TOKEN }}
             # this is a built-in strategy in release-please, see "Action Inputs"
             # for more options
             release-type: simple
    ``` 
3. Push these changes to github repo
3. Create a token and configure as a secret:
   - Go to your account settings > developer settings > create a new classic token with name `for release please`. Copy the token value.
   - Go to the repository settings > secrets and variables > add a new secret `MY_RELEASE_PLEASE_TOKEN` with the token value
   - Under the same repository settings, Move to the `Actions` > `general` > check the `Allow GitHub Actions to create and approve pull requests`
4. Now all is set. Push any commit to the `main` branch in repo and the action above will create a new PR for next release. Example: [here](https://github.com/ossdhaval/empmgmt/pull/3). This is just a release PR, release is not yet created.
5. merge this PR and a new release will be created. Example [here](https://github.com/ossdhaval/empmgmt/releases/tag/v1.0.0)
