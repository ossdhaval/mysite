# Integration with JaCoCo and SonarCloud

High-level steps :
1. Integrate JaCoCo
2. Onboard to SonarCloud
3. Integrate with SonarCloud
4. Integrate with CI using Github Actions

#### 1. Integrate JaCoCo

This is easy as you just have to add following plug-in in your project POM (parent pom in multimodule project) under `<pluginManagement>`.

```
				<plugin>
					<groupId>org.jacoco</groupId>
					<artifactId>jacoco-maven-plugin</artifactId>
					<version>0.8.7</version>
				</plugin>
```

That is it.

#### 2. Onboard to SonarCloud

1. login to SonarCloud
2. go to `+` sign on top right which says 'add new project or organizationyour profile
3. click organizations
4. get organisations from Github
5. Install SonarCloud app
   Either give permission to see all repos or only select repos.
6. Now you'll see projects under your organization and click 'analyze'
7. Now you'll be taken to project configuration page on SonarCloud
8. click on 'with github actions'
   - step 1 is to create github secret as directed on page ( remember the 'settings' tab is on your github project page and not        under your profile )
   - In the next step, sonarcloud will tell you what changes you need to make in your POM file and in you github repo ( like            adding workflow yml in your .github folder). Be careful when you are making these changes as you might need to change few          things as per your project needs. This is the last step. If you do these changes and execute your workflow in github, this        page will automatically refresh and it'll show you code analysis. Note : for coverage, this assumes that you have integration      with JaCoCo and JaCoCo is generating coverage reports already which SonarCloud will directly use.


### Troubleshooting:

## Aggregare report

**Add aggregate code coverage report to your multimodule**

Reference:
https://github.com/jacoco/jacoco/tree/master/jacoco-maven-plugin.test/it/it-report-aggregate

command to run: 
mvn install jacoco:report-aggregate

But I couldn't implement it at the end due to many issues that I faced.
1. First of all, I started facing `suiteXmlFiles is configured, but there is no TestNG dependency` error when I run `mvn install`.
2. Once I added this dependency, `mvn install` started complaining that it did not find dependency of projects that had `war` packaging. This is due to the fact that we had to add all the projects in the newly created reporting module's pom file, including those projects that were having `war` packaging. Now maven started looking for `.jar` files for those dependencies which it didn't find. Soluiton was to now generate two artifacts from those `war` project. One `war` and other `jar` with contained all the classes.
3. To shortcut the effor and just to see things working, I removed those projects with `war` packaging from the build. Now, I was facing another error in the new reporting module that suit xml (defind in pom by tag `suiteXmlFile`) is invalid. 

Finally I left the effort.

Overall, I felt that with Jacoco, generating aggregate report for multimodule maven project is difficult. Specially, if your project has modules with `war` packaging.


## Troubleshooting

*Message:* Not generating jacoco repot due to :

`Skipping JaCoCo execution due to missing execution data file.`

Helpful links:

https://stackoverflow.com/a/36305148/2331225

http://www.ffbit.com/blog/2014/05/21/skipping-jacoco-execution-due-to-missing-execution-data-file/

[official latest JaCoCo plug-in maven config](https://www.eclemma.org/jacoco/trunk/doc/examples/build/pom.xml)
