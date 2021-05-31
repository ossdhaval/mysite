# Github Actions


Reference :
https://app.pluralsight.com/library/courses/github-actions-getting-started/table-of-contents

### How to run a workflow for all branches but run an action on a specific branch

https://stackoverflow.com/questions/58139406/only-run-job-on-specific-branch-with-github-actions

### Action that can build multiple dependent projects

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
