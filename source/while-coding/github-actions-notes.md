# Github Actions


Reference :
https://app.pluralsight.com/library/courses/github-actions-getting-started/table-of-contents

### How to run a workflow for all branches but run an action on a specific branch

https://stackoverflow.com/questions/58139406/only-run-job-on-specific-branch-with-github-actions

### Options for yml tags of a github workflow:

https://docs.github.com/en/actions/reference/workflow-syntax-for-github-actions

### Checkout action documentation:

https://github.com/actions/checkout

### Action that can build multiple dependent projects

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

### Contexts and expressions available to workflow: 

https://docs.github.com/en/actions/reference/context-and-expression-syntax-for-github-actions#github-context


### github action contexts vs Runner variables:
https://docs.github.com/en/actions/reference/context-and-expression-syntax-for-github-actions#determining-when-to-use-contexts

basically, in your workflow code, the part apart from 'run:' is executed by Github action and code under 'run:' is executed by runner. You have [contexts](https://docs.github.com/en/actions/reference/context-and-expression-syntax-for-github-actions#contexts) like `github.repository` in the part which is executed by github action, while runner doesn't have context but it has many [environment variables](https://docs.github.com/en/actions/reference/environment-variables#default-environment-variables), like `$GITHUB_REF`

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
