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
