Good resource that describes skills and attitude of DevOps engineer:
https://github.com/scott45/devops-learningmap

## CI-CD

### CI flow

Essential actions to take place when PR is created or merged into the mail line.

1. Automate the build
   - Build and project and create artifacts
2. Add automated tests in the code
   - Unit tests
   - integration tests
3. Linting
   - code style checks
   - security scans
   - static code analysis
   - document linting
4. Commit checks
   - commit message styles (conventional commit)
   - commit should have DCO

First, when the PR is created, these automation steps will run at every commit. `pull_request` event.

Then it should be possible to dispatch an action and create a cloud environment where the software build gets installed with new changes. This environment can be used to perform manual QA plus and manual UI tests.

then when PR is merged, the above steps should run on the merged code. `Push` event on main.



## GitOps

CNCF site: https://opengitops.dev/ and https://github.com/cncf/tag-app-delivery/tree/main/gitops-wg
CNCF tool for gitops: [flux](https://fluxcd.io/)
good repo for gitops: resources: https://github.com/weaveworks/awesome-gitops
