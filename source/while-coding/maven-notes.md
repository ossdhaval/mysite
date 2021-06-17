# Maven Notes


### Primary uses :

#### As build tool

- compile
- run tests
- build jars
- build wars and ears
- deploy to server

#### As project management tool
- dependency management


### difference between maven and ant :

Ant uses many configurations ( for example specifying in which folder your code is ) while maven use 'convention over configuration' and so reduces configuration. For example, when you run 'mvn compile' it assumes that code is under src/main/java.

#### Maven conventions:

- Java source code is available at {base-dir}/src/main/java

- Test cases are available at {base-dir}/src/test/java

- The type of the artifact produced is a JAR file

- Compiled class files are copied to {base-dir}/target/classes

- The final artifact is copied to {base-dir}/target

- http://repo.maven.apache.org/maven2, is used as the repository URL.

### Maven lifecycle phases and plugin goals :

We usually ask maven ( via mvn ) command to run either of two things : a lifecycle phase or a plugin goal.
eg. 'mvn install' is a asking maven to run install phase. 'mvn archetype:generate' is asking maven to run generate goal within archetype plugin.

Plugin goals are independent and they can be invoked individually. While lifecycle phases are hierarchical. When you ask maven to do 'mvn install', maven is going to run all lifecycle phases before 'install' which are 'prepare-resource, compile, test, package'.

Plugin goals are actual code while lifecycle phases are logical. Maven internally calls a goal of a plugin to execute that lifecycle phase. It also has a default mapping of these phases to plugin goals ( compile phase maps to 'compiler:compiler', test maps to 'surefire:test', package maps to 'jar:jar' ). So, when you say 'mvn install', it is going to invoke lifecycle phases ( a.k.a plugin goals ) one after other.


One tricky thing here : lifecycle phase to plugin goal is not one way binding. Its two way binding where goals also specify what lifecycle phase they attach to. In this case, if you run a goal, maven will invoke all phases ( and associated goals to those phases ) before running actual goal. For example : code of surefire:test plugin mentions that it is a test phase goal. So, whether you run 'mvn test' or 'mvn surefire:test' it'll have same effect. All goals attached to preceding phases will be executed in both cases..

One more tricky thing : There can be phases that don't have any goal attached. And there can be goals that are not associated with any phase.

it is not that there is single lifecycle phase hierarchy. There are different hierarchies for different packaging. So, what you specify in <packaging> tag will control what lifecycle phase hierarchy is invoked. So, packaging determines which one of default hierarchies are invoked, hierarchy has phases. Again based on packaging specified, maven may attach different goal to same phase. For example : 'package' phase will be attached to jar:jar if packaging is mentioned as jar. But for 'war' packaging, maven will attach 'package' phase with war:war.
In all, based on packaging, maven will determine hierarchy and goals attached to phases.


For further reference :
http://maven.apache.org/guides/introduction/introduction-to-the-lifecycle.html#Built-in_Lifecycle_Bindings

### Simplest parent POM :

take pom of a quickstart project and create a copy of it.
Give a group ID. This ID will be same across all modules unless they specify thier own.
Give artifact ID. Doesn't matter much. Give something like 'productparent'.
Give packaging as 'pom'

remove all dependencies


Note :
when you want to create a simple spring project, use below dependency :

<!-- https://mvnrepository.com/artifact/org.springframework/spring-context -->

```
<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-context</artifactId>
    <version>4.3.10.RELEASE</version>
</dependency>
```


### Scopes :

There are total six scopes : 
- compile 
- test
- run
- provided
- system 
- and one more.

'compile' scope is default. 

Also, anything dependency in compile scope is available in test and run as well. So, if you declare a dependency without specifying scope, that jar becomes part of the deployable bundle. So, if there is anything like servlet api etc, it is very imp that you mention explicitely that it is in 'provided' scope, otherwise your deployeble would be very heavy. Similarly, you should mention 'test' scope for junit dependencies.

a good reference : https://maven.apache.org/guides/introduction/introduction-to-dependency-mechanism.html

### Making projects dependent on each other :

common utilities projects like 'shared-kernel' etc which are bundled as jar are often dependency for others. To access util projects in other projects, add following to maven of dependent project :

```
<dependency>
  <groupId>com.gsg.kernel</groupId>
  <artifactId>gsg-shared-kernel</artifactId>
  <version>1.0-SNAPSHOT</version>
</dependency>
```
Don't forget to mention version tag for this.
Also, since by default scope is compile, this jar will be bundled with your project as dependency all the way to deployment.


### Note on Packaging :

“POM” as value to <packaging> like
<packaging>pom</packaging>

“POM” packaging is mentioned for a pom file where there is no out put in form of a war or ear or jar. It is usually used in a pom file along multiple modules, and these modules will actually have packaging as war etc in their pom files. Basically, used when you want a POM file as top level orchestrator between modules.


When no packaging is declared, Maven assumes the artifact is the default: jar

The current core packaging values are: pom, jar, maven-plugin, ejb, war, ear, rar, par


### Note on important maven concepts :


1)      Dependency
2)      Inheritance
3)      Aggregation

#### 2. Inheritance :

Elements in the POM that are merged are the following:
- dependencies
- developers and contributors
- plugin lists (including reports)
- plugin executions with matching ids
- plugin configuration
- resources
inheritance is when you specify <parent> element in your child pom. Primary use of inheritance is to keep common configuration in a central POM which can be used by multiple projects. Super pom is an example of that. 
In inheritance, parent is not aware of its children. ie: if parent is built then build for child projects will not be triggered automatically.

#### 3. Aggregation

aggregation is when you define <module> in top-level POM. Here the purpose is to club together those projects which need to be built together. Here, inheritance of plugins and dependencies ( and other elements ) will not happen but if you build the aggregated POM then the projects mentioned as modules will be triggered for build as well.

useful reference : https://stackoverflow.com/questions/17482320/maven-module-inheritance-vs-aggregation )

*Note* : 

when you want to see what all dependencies your app has, you generally open POM file in eclipse and go to 'dependency Hierarchy' tab. But here, you can't see dependencies pulled by parent POM. But this is visible in 'effective POM' tab.
'Dependency Hierarchy' only shows things defined in current POM as 'dependency'

### Maven versioning :

http://kylelieber.com/2012/06/maven-versioning-strategy/




### Maven commandline options / switches

Source : https://books.sonatype.com/mvnref-book/reference/running-sect-options.html

-e, --errors: Produce execution error messages

-X, --debug: Produce execution debug output

-q, --quiet: Quiet output - only show errors

The -q option only prints a message to the output if there is an error or a problem.

The -X option will print an overwhelming amount of debugging log messages to the output. This option is primarily used by Maven developers and by Maven plugin developers to diagnose problems with Maven code during development. This -X option is also very useful if you are attempting to diagnose a difficult problem with a dependency or a classpath.

The -e option will come in handy if you are a Maven developer, or if you need to diagnose an error in a Maven plugin. If you are reporting an unexpected problem with Maven or a Maven plugin, you will want to pass both the -X and -e options to your Maven process.

`mvn dependency:resolve`
    resolve(or download) dependencies as per pom.xml

To activate one or more build profiles from the command line, use the following option:
-P, --activate-profiles <arg>
Comma-delimited list of profiles to activate

To define a property use the following option on the command line:

-D, --define <arg>: Defines a system property


-h, --help: Display help information

`mvn -h`

#### Multimodule projects:
	
##### failures
	
The following options control how Maven reacts to a build failure in the middle of a multi-module project build:
	
`-fae`, `--fail-at-end` : 
Only fail the build afterwards; allow all non-impacted builds to continue

`-ff`, `--fail-fast` : Stop at first failure in reactorized builds
	
`-fn`, `--fail-never` : NEVER fail the build, regardless of project result
	
The -fn and -fae options are useful options for multi-module builds that are running within a continuous integration tool like Hudson. The -ff option is very useful for developers running interactive builds who want to have rapid feedback during the development cycle.

if you want to skip certain modules from getting build, then use `-pl` option.

`mvn clean -fae -X -pl \!module1,\!module2 jacoco:prepare-agent test install jacoco:report`

Or you can set profile to only build other modules.




Source : https://books.sonatype.com/mvnref-book/reference/_using_advanced_reactor_options.html


### How to find where your .m2 and settings.xmls are which are being used by maven from commandline :

just fire `mvn -X` command. This will trigger a build which will probably fail, but it'll also print all the information on console like below :

```
dhaval@dhaval-Lenovo-U41-70:~/code/ij-projects/java8/Java 8 certification$ mvn -X
Apache Maven 3.6.3
Maven home: /usr/share/maven
Java version: 11.0.8, vendor: Ubuntu, runtime: /usr/lib/jvm/java-11-openjdk-amd64
Default locale: en_IN, platform encoding: UTF-8
OS name: "linux", version: "5.4.0-47-generic", arch: "amd64", family: "unix"
.
.
.
[DEBUG] Reading global settings from /usr/share/maven/conf/settings.xml
[DEBUG] Reading user settings from /home/dhaval/.m2/settings.xml
[DEBUG] Reading global toolchains from /usr/share/maven/conf/toolchains.xml
[DEBUG] Reading user toolchains from /home/dhaval/.m2/toolchains.xml
[DEBUG] Using local repository at /home/dhaval/.m2/repository
[DEBUG] Using manager EnhancedLocalRepositoryManager with priority 10.0 for /home/dhaval/.m2/repository

```

so you'll see all the important info in this.




### command to skip tests

`mvn install -DskipTests`

Starting with the Maven 2.1 release, there are new Maven command line options which allow you to manipulate the way that Maven will build multimodule projects. These new options are:

-rf, --resume-from: Resume reactor from specified project

-pl, --projects: Build specified reactor projects instead of all projects

-am, --also-make: If project list is specified, also build projects required by the list

-amd, --also-make-dependents: If project list is specified, also build projects that depend on projects on the list

### Plugin-management vs plugins (references : [SO](https://stackoverflow.com/questions/10483180/what-is-pluginmanagement-in-mavens-pom-xml))

In pom.xml, you may see plugin definitions at two places.
1. Under 

```
<build>
    <pluginManagement>
	    <plugins>
```

2. Under 

```
<build>
	<plugins>
```

it is important to understand the difference when `<plugins>` appear under `<pluginManagement>`, and when
same tag appears without `<pluginManagement>`.

`<plugins>` mentioned under `<pluginManagement>` tag, are just definition. They provide a central place
to define plugin version, plugin configuration etc in an multi-module project where there are 
multiple pom.xml files in different modules. All of them can not use same plugin configuration as defined
in `<pluginManagement>` in parent or super pom. When you define plugin under `<pluginManagement>`, you 
are actually not activating it. It is just a common definition.

To activate plugins, you have to define same plugins in `<plugins>` tag outside of `<pluginManagement>`.
You can do this either in same same pom where `<pluginManagement>` is defined, or in individual module
pom files. But now, you don't have to define version or any other configuration for those plugins which 
are already defined in the `<pluginManagement>`. Just mention `group` and `artifactId` and maven will 
pickup rest of the details from `<pluginManagement>`. Remember, when you are mentioning `<executions>`, 
you have to do it in `<plugins>` outside of `<pluginManagement>`

It is a classic mistake to put plugin information in `<pluginManagement>` and expect it to start working.
I made this mistake when integrating JaCoCo in a multimodule project.
		
#### Maven profiles:
        
reference : https://maven.apache.org/guides/introduction/introduction-to-profiles.html
        
- Profiles override or add configuration in effective POM at build time
- You can activate profiles automatically by setting certain env variable or by presence of certain file or many other ways.
- From commandline you can use option `-p` like below:
```mvn groupId:artifactId:goal -P profile-1,profile-2```

        
        
Profiles specified in the POM can modify the following POM elements:

```
<repositories>
<pluginRepositories>
<dependencies>
<plugins>
<properties> (not actually available in the main POM, but used behind the scenes)
<modules>
<reports>
<reporting>
<dependencyManagement>
<distributionManagement>
```
    
a subset of the `<build>` element, which consists of:

```
<defaultGoal>
<resources>
<testResources>
<directory>
<finalName>
<filters>
<pluginManagement>
<plugins>
```

### How to build project with forcing all dependencies to be reloaded

	There are two commands.
	1) Using `-U` option ( eg. `mvn -U clean install' ). This will force all the snapshot dependencies to be reloaded from respective maven repos.
	2) Using `dependency:purge-local-repository` option (eg. `mvn dependency:purge-local-repository compile install` ). This is similar to deleting .m2 and reloading everything including release dependencies
	
		
### Troubleshooting:

#### deactivating certain modules using profiles:
Ideally, as per above, if you put `<modules>` tag in a profile and mention list of `<module>` under it, then this should override the modules listed under `<project>` in same pom. But this doesn't happen. Why I don't know. I faced it and also see [here](https://stackoverflow.com/questions/13381179/using-profiles-to-control-which-maven-modules-are-built). `Actual maven behaviour seems to be that that one profile can override modules on if they are defined in another profile.` So the solution is that you remove modules from POM's `<project>` and create a profile that loads by default that lists superset of modules, then you also should have another profile that lists subset of modules that you want to run. Now, when you run `mvn` by mentioning name of profile with subset, the default profile will not load. Hence only subset mentioned in your profile will be taken into account.
  
Another maven behaviour which is documented but not very much known is that default profile mentioned in POM xml using `<activeByDefault>true</activeByDefault>` will only be activated if there are no other profiles getting activated at the time of build. So, it is either the default profile or other profiles that get active. Most multimodule projects run with multiple profiles active at a time, hence default profiles are not very useful in multimodule projects. And due to this behaviour, the above solution of deactivating cetain modules using profiles also not usable. Plus, it seems this is [not recommended too](https://blog.soebes.de/blog/2013/11/09/why-is-it-bad-to-activate-slash-deactive-modules-by-profiles-in-maven/)
  
Finally, I have to deactivate modules using reactor commandline argument `-pl` like below:
  
`mvn clean -fae -X -pl \!module1,\!module2 jacoco:prepare-agent test install jacoco:report`
  
