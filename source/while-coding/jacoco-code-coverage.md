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

### *Message:* Not generating jacoco repot due to :

`Skipping JaCoCo execution due to missing execution data file.`

In my case it was due to Surefire plugin was defining <argLine> property within the <configuration> tag of plugin definition.
Solution as described [here](https://github.com/jacoco/jacoco/issues/964) is to move this property outside of surefire plugin
definition and declare as POM property. Something like below:

Put this as pom property, outside of plugin.
```
<argLine>-your -argline -parameters</argLine>	

```
	
This is how surefire configuration should look like
```
<plugin>
	<groupId>org.apache.maven.plugins</groupId>
	<artifactId>maven-surefire-plugin</artifactId>
	<version>2.19.1</version>
	<configuration>
		<argLine>@{argLine}</argLine>
	</configuration>
	
```

Helpful links:

https://stackoverflow.com/a/36305148/2331225

http://www.ffbit.com/blog/2014/05/21/skipping-jacoco-execution-due-to-missing-execution-data-file/

[official latest JaCoCo plug-in maven config](https://www.eclemma.org/jacoco/trunk/doc/examples/build/pom.xml)
	

### Message: can't have 2 modules with the following key

when you are integrating a multimodule project with sonarcloud it'll ask you to put below properties in your POM

```
<properties>
	<sonar.projectKey>someprojectkey</sonar.projectKey>
	<sonar.organization>someorg</sonar.organization>
	<sonar.host.url>https://sonarcloud.io</sonar.host.url>
</properties>

```
	
but when you run this, sonar will complain with error as follows:
	
```
Error:  Failed to execute goal org.sonarsource.scanner.maven:sonar-maven-plugin:3.9.0.2155:sonar (default-cli) on project someproject: Project 'someprojectkey' can't have 2 modules with the following key: someprojectkey -> [Help 1]
	
```
	
solution to this is to add a module key as below along with three properties suggested by sonarcloud:
	
```
<sonar.moduleKey>${project.groupId}:${project.artifactId}</sonar.moduleKey>
	
```


### Sonarcloud analysis types:
	
There are two types of analysis supported. Automated and CI based.
When you add a new project, sonar will analyse the code and decide whether it should do automatic analysis or not based on these [limitations](https://sonarcloud.io/documentation/analysis/automatic-analysis/). If sonarcloud finds it ok to do automatic analysis then it'll go ahead and perform it. You'll directly see code quality dashboard. 
	
If automatic anaysis is not found suitable, then sonar will ask you to configure CI analysis where you have to make changes in you project to add configurations as suggested by sonar during project onboarding process. 
	
Both of these analysis [can't be active together](https://community.sonarsource.com/t/sonarcloud-task-fails-because-of-ci-analysis-and-auto-analysis-running/22937). If you want CI based analysis, you have to turn off automatic one. (project->administration->analysis types)
	
I suggest CI analysis over automatic as it is easy to setup and gives more control on when a scan should run. For example, automatic analysis only runs on push on master or merge on master. But with CI based scan, you can ask it run for every push on every branch.
	

### Sonar tokens

When you configure CI based analysis, sonar will ask you to add a security token 'SONAR_TOKEN' in your github. Remember that you don't need a separate token for each repo of your org. You can use one token for all the repo by creating an github security token at org level instead of repo level. 
- SonarCloud: go to your profile->security->generate a new token with any name. Name here doesn't matter, just copy the token value.
- github: go to you organization landing page->security->create a new org token with name 'SONAR_TOKEN' with value as you copied above.
- this github token will be used in the github action workflow yml that you will create.
	

	
