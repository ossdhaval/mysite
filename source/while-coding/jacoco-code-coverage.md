# JaCoCo aggregare report

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
