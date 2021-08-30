# As community manager

My learnings"

### About documentation :

There could be three kinds of documentation:
1) Introduction and marketing material
2) Installation guides
3) Configuration guides ( like how to use various configuration option, enable disable features, setup basic usecases )
4) Technical documentation (this is technical documentation of code, modules and architecture)
5) developer documentation (How to setup workspace, run tests, remote debug,Contribution process, guidelines etc)

All of above documentation can also be assisted with video tutorials, FAQs etc



### Reference material

#### books
- https://www.amazon.com/Art-Community-Building-New-Participation-ebook-dp-B008224FMC/dp/B008224FMC/ref=mt_other?_encoding=UTF8&me=&qid= 


#### videos 

- https://www.youtube.com/watch?v=nGKSnMdBFsk https://www.youtube.com/watch?v=Js0gW8pAnh4
- quick and informative : https://www.youtube.com/watch?v=b1pyh2XCyrg

#### Live examples:

On community chat platform (gitter/slack) :
as understood from what 'Pop' user is doing on Falco slack channel.
- welcome new users
- setup community calls ( ones a week ). and send reminders.
- setup and conduct surveys
- respond to tech queries if possible.
- encourage people to appreciate others like this :
https://kubernetes.slack.com/archives/CMWH3EH32/p1617024285139200


Large open-source projects that are actively managed and can be looked at as reference:
[spring](https://github.com/spring-projects)
[kubernetes](https://github.com/kubernetes/kubernetes)
[falco](https://github.com/falcosecurity/falco)

#### Articles and sites:
- https://opensource.guide/best-practices/
- https://18f.github.io/open-source-program/pages/maintainer_guidelines/




### Regular house holding checks :

- stale branches across repos
- (for sometime)Track PR merges and see if they had met quality criteria and let code owner and developer know
- issue triage
- are all the automation successfully running? For example, github actions can fail silently. You have to periodically check their logs to ensure that there are no errors. For instance, one of my github action script was referring to a module in the build command. Later this module was removed from the project and github action script started failing, but nobody knew until a person spotted it. Note: I found out that I was not paying attention to my emails. Github sends email with subject similar to `[JanssenProject/jans-auth-server] Run failed: Code quality check - feature-flags-using-ff4j (276ae10)` in case there is a failure in the action run .

