# Github Actions

### References

#### course :
https://app.pluralsight.com/library/courses/github-actions-getting-started/table-of-contents

#### How to run a workflow for all branches but run an action on a specific branch

https://stackoverflow.com/questions/58139406/only-run-job-on-specific-branch-with-github-actions

#### Options for yml tags of a github workflow:

https://docs.github.com/en/actions/reference/workflow-syntax-for-github-actions

#### Checkout action documentation:

https://github.com/actions/checkout

#### insightful article on `pull_request` action trigger
https://frontside.com/blog/2020-05-26-github-actions-pull_request/

#### list of workflow trigger events
https://docs.github.com/en/actions/learn-github-actions/events-that-trigger-workflows

#### A good reference of a major project that uses github action for ci-cd

cpython which is official python interpreter: https://github.com/python/cpython

#### Action that can build multiple dependent projects

Here current repository needs BOM project, which is a separate project, to be built first.

```

jobs:
  build:

    runs-on: ubuntu-latest

    steps:
      - name: Set up JDK 11
        uses: actions/setup-java@v2
        with:
          java-version: '11'
          distribution: 'adopt'

      - name: Checkout Maven BOM repo
        uses: actions/checkout@v2
        with:
          repository: JanssenProject/jans-bom
          path: bom

      - name: Build Maven BOM repo
        run: mvn install
        working-directory: ./bom

      - name: checkout current repo
        uses: actions/checkout@v2
        with:
          fetch-depth: 0  # Shallow clones should be disabled for a better relevancy of sonarqube analysis

      - name: Build with Maven
        run: mvn clean -fae jacoco:prepare-agent test install jacoco:report


```

#### Contexts and expressions available to workflow: 

https://docs.github.com/en/actions/reference/context-and-expression-syntax-for-github-actions#github-context


#### github action contexts vs Runner variables:
https://docs.github.com/en/actions/reference/context-and-expression-syntax-for-github-actions#determining-when-to-use-contexts

basically, in your workflow code, the part apart from 'run:' is executed by Github action and code under 'run:' is executed by runner. You have [contexts](https://docs.github.com/en/actions/reference/context-and-expression-syntax-for-github-actions#contexts) like `github.repository` in the part which is executed by github action, while runner doesn't have context but it has many [environment variables](https://docs.github.com/en/actions/reference/environment-variables#default-environment-variables), like `$GITHUB_REF`. The `github` context contains information about the workflow run and the event that triggered the run.You can also read most of the `github` context data(available to action) in environment variables `env` context (available in `run`).

### Run scripting

[run:](https://docs.github.com/en/actions/reference/workflow-syntax-for-github-actions#jobsjob_idstepsrun) basically runs commands on operating system shell. In case of `runs-on: ubuntu-latest`, you can write all commands and scripts that you can run on ubuntu shell.


### how to print all values in any context.

```
- name: Dump github context
  shell: bash
  env:
   GITHUB_CONTEXT: ${{ toJson(github) }}
  run:   echo "$GITHUB_CONTEXT"
```

### print all the environment variables:

```
      - name: Get env variables
        run: 
          echo ${ENV}
```

### convert context value to lowercase:
https://github.community/t/additional-function-s-lowercase-uppercase/140632

### setting a variable in one action and using it in another:
https://docs.github.com/en/actions/reference/workflow-commands-for-github-actions#setting-an-environment-variable


### how to work with a list, set and access environment variable, run linux commands 

```
name: workflow with list
on:
  push:
    branches:
      - main
  pull_request:
    branches:
      - main
  workflow_dispatch:
jobs:
  job-1:
    name: job-1
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
        with:
          fetch-depth: 0
      - name: print all
        env:
          JVM_PROJECTS: |
            mod1
            mod2
        run: |
          ls
          echo $JVM_PROJECTS
          for module in $JVM_PROJECTS
          do
            echo "Module: $module"
            echo "=============="
            mvn -f $module/pom.xml javadoc:javadoc
            ls $module/target/site/apidocs/
          done
```

### how to create an array of values returned from a command and loop through it

```
        run: |
          pwd
          sub_modules=($( mvn help:evaluate -Dexpression=project.modules -q -DforceStdout | tail -n +2 | head -n -1 | sed 's/\s*<.*>\(.*\)<.*>/\1/'))
          for module in "${sub_modules[@]}"
          do
            echo "Module: $module"
            echo "=============="
            mvn -f $module/pom.xml javadoc:javadoc
            echo "=============================================================="
            ls $module/target/site/apidocs/
          done
```

### Misc

- Actions can be looked at from two different places:
  - from `actions` tab under repository's main screen.
  - go to PR->checks
- PR checks may have more checks than directly triggered by workflows in `action` tab. For example, when `code quality check` workflow get triggered for a PR, at the end of it, sonar cloud also pushes a check in the PR->checks section that summarizes result of the scan. So, in `action` section you'll just see `code quality check` workflow, but in PR->checks you'll see `sonarcloud` check as well. 
- A workflow run is made up of one or more jobs, which run in parallel by default. Each job runs in a runner environment specified by runs-on. By default, GitHub will maximize the number of jobs run in parallel depending on the available runners on GitHub-hosted virtual machines. To run jobs sequentially, you can define dependencies on other jobs using the jobs.<job_id>.needs keyword. 
- Each step runs in its own process in the runner environment and has access to the workspace and filesystem. Because steps run in their own process, changes to environment variables are not preserved between steps. GitHub provides built-in steps to set up and complete a job. [Reference](https://docs.github.com/en/actions/using-workflows/workflow-syntax-for-github-actions#jobs)
- Commands run using non-login shells by default. You can choose a different shell and customize the shell used to run commands. For more information, see jobs.<job_id>.steps[*].shell. Each run keyword represents a new process and shell in the runner environment. When you provide multi-line commands, each line runs in the same shell
- Strategy matrix is at job level and not at step level
-  
