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

Google technical writting style: https://developers.google.com/tech-writing

### Reference material

#### books
- https://www.amazon.com/Art-Community-Building-New-Participation-ebook-dp-B008224FMC/dp/B008224FMC/ref=mt_other?_encoding=UTF8&me=&qid= 


#### videos 

- https://www.youtube.com/watch?v=nGKSnMdBFsk https://www.youtube.com/watch?v=Js0gW8pAnh4
- quick and informative : https://www.youtube.com/watch?v=b1pyh2XCyrg

#### Good articles

- good list of tooling with details : https://www.infoq.com/presentations/monzo-tools-deploy/?itm_source=infoq&itm_medium=videos_homepage&itm_campaign=videos_row1

#### Good tools

- Developer portals : https://backstage.io/
- cloud software licensing: https://licensespring.com/

Flow of implementation of licensespring in gluu flix licensing:
![image](https://user-images.githubusercontent.com/343411/214495951-385f4b4e-7830-4d2d-b33f-e233baf9ea40.png)


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
[Angular](https://github.com/angular/angular)
[falco](https://github.com/falcosecurity/falco)

#### Articles and sites:
- https://opensource.guide/best-practices/
- https://18f.github.io/open-source-program/pages/maintainer_guidelines/
- guidelines for labels : https://seantrane.com/posts/logical-colorful-github-labels-18230/
- good github workflow for contributors: https://www.kubernetes.dev/docs/guide/github-workflow/
- github's own roadmap managed via project board: https://github.com/github/roadmap/projects/1
- 


### Regular house holding checks :

- stale branches across repos
- (for sometime)Track PR merges and see if they had met quality criteria and let code owner and developer know
- issue triage
- are all the automation successfully running? For example, github actions can fail silently. You have to periodically check their logs to ensure that there are no errors. For instance, one of my github action script was referring to a module in the build command. Later this module was removed from the project and github action script started failing, but nobody knew until a person spotted it. Note: I found out that I was not paying attention to my emails. Github sends email with subject similar to `[JanssenProject/jans-auth-server] Run failed: Code quality check - feature-flags-using-ff4j (276ae10)` in case there is a failure in the action run .
- check automated non-dependabot PRs to be merged on Non-CN repos
- check github notifications 
- PR backlog across all repos and aging PRs
  - backlog should not cross certain number of open PR threshold and aging of PRs shouldn't be more than certain days.


### Experience

#### Rolling out branch protections

I recently rolled out branch protections on all the Jans repos. Here I am noting how did we do it, what were the issues and hiccups faced.

##### preconditions:
- CODEOWNERs should be in place
  - though it is not a requirement from github, having two or more code owner for each repo will let people know who is going to shephard that repo. Who is going to be the go to person for that repo. When you turn on protections like `Require PR review before merge` then people would want to know who should they reach out to for review. If your code owner is set then github automatically suggests codeowner as reviewer. Ideally though, reviewer can be anyone from the team who is well aware of the code. Codeowner is usually a person who is responsible for that repo and generally the senior most developer but he/she can't be a reviewer everywhere. 

##### How to roll out:
- we rolled out below mentioned protections
  - for master
  - for all other

- how we should have done it:
  - signed commits and deletion of protected branches first.
  - enabling and mendating a check where github action builds code in the PR
  - Requiring PRs to be reviewed and approved before merge

##### problems faced
- Branches that were created before we enabled protections had unsigned commits.
- Some of the master builds were broken since before we enabled protections (jans-orm had failed testcases, jans-client-api code was not up-to-date with corresponding changes in the jans-auth-client)
- problem with code owner not able to merge without approval from someone else ( may be another code owner)

### Useful github automation:

- If you have PRs that get auto generated by bots and then it is a routine task to just merge those PRs then, to automate that routine task, enabling auto merge for repositories and PRs will help. First you'll have to [enable auto merge for repo](https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/configuring-pull-request-merges/managing-auto-merge-for-pull-requests-in-your-repository) and then configure bot to raise PRs with [automerge enabled](https://docs.github.com/en/github/collaborating-with-pull-requests/incorporating-changes-from-a-pull-request/automatically-merging-a-pull-request).
- 


### Performance parameters for OSS project:
These are metrics and parameters developed by Linux foundation:
- [CII best practice badge](https://bestpractices.coreinfrastructure.org/en): To ensure that project is following OSS best practices. For health and stregth of engineering process in an OSS project.
- [CHAOSS](https://chaoss.community/) project: to define how healthy your community is. They also have tools that will give you analytics on top of your OSS repo data.
- Good OSS tool for Github repo analytics: https://devstats.cncf.io/. Kubernetes is using this tool. Kubernetes dashboard: https://k8s.devstats.cncf.io/d/12/dashboards?orgId=1&refresh=15m
- open decision framework: https://opensource.com/open-organization/resources/open-decision-framework


### issue triage
good article: https://medium.com/@clarkbw/github-issue-triage-and-transparency-be35acd8e85d

issue triaging needs correct set of labels in place: Look at this for reference. https://github.com/falcosecurity/falco/labels?page=1&sort=name-asc

Triage process as Kubernates: https://www.kubernetes.dev/docs/guide/issue-triage/

How to run bug triage:
- triage PRs first, then Issues
- For every issue/PR we want to decide on what is the next action and who is going to take that action. Like status is `require-more-analysis` assign `owner` also who will do that analysis 

Labels:

  - Triage:
    - needs-triage
    - needs-information    
    - triaged(used to flag that PR/Issue has been discussed and it is ready to enter active development), triaged/duplicate, triaged/will-not-fix 
    - kind/bug, enhancement, feature, support
    - size/xs, s, m, l, xl, xxl
    - value/high, medium, low
    - area/<modules like jans-fido2>, release-notes, documentation
    - good first issue

  - Tracking:
    - status/backlog,WIP,test,completed
    - priority/high, medium, low
    - help wanted


- github milestones are usually used to represent sprints    
    
       

## Tech writing notes:
(From: https://developers.google.com/tech-writing)


- Prefer full term over acronym. Benefit of short forms and acronyms is they reduce length of text, but make understanding difficult as user has to translate everytime. So use acronyms when you know a lengthy term is going to be used many times in text. This rule doesn't apply to popular acronyn like HTML.
- If you are referring to a term which reader may not be aware of then give a link to explaination of that term or define yourself.
- Prefer to use noun itself instead of pronoun(it, them, they, this, that etc)  as pronoun may lead to confusion. Use it only if it is situated very close to the noun in the sentence.
- The vast majority of sentences in technical writing should be in active voice. Good sentences in technical documentation identify who is doing what to whom.
  - Prefer active voice to passive voice
    - Use the active voice most of the time. Use the passive voice sparingly. Active voice provides the following advantages:
    - Most readers mentally convert passive voice to active voice. Why subject your readers to extra processing time? By sticking to active voice, readers can skip the preprocessor stage and go straight to compilation.
    - Passive voice obfuscates your ideas, turning sentences on their head. Passive voice reports action indirectly.
    - Some passive voice sentences omit an actor altogether, which forces the reader to guess the actor's identity.
    - Active voice is generally shorter than passive voice.
  - remember: Be bold—be active.
- Write clear sentences
  - Choose strong verbs



## setup meetings and calendar app

- problem is that everyone uses a different calendar. Google, outlook, iOS etc. 
- in Janssen google calendar is generally acceptable to all. So I have created a separate calendar for Janssen in my google account and create event in that
   calendar. then I share link of that `event` on Rocket chat. Problem with this approach is that when you reschedule, everyone's calendar doesn't get updated automatically. I have to send the link again and people have to save the event again. Same for cancellation, You have to verbally cancel the meeting over chat but invites would stay in everyone's calendar.
- Then I started to check how other major open source project do this and I found 
  - Linux foundation : https://events.linuxfoundation.org/lfx-mentorship-showcase/program/schedule/
  - Kubernetes: https://www.kubernetes.dev/resources/calendar/
- most of them give google calendar and may be few others. But there is no unified way of doing this. They also have [this](https://www.kubernetes.dev/events/community-meeting/) kind of instructions for user to 
- then I read about `iCal` a.k.a `.ics` format. This is a neutral format which also allows people to respond to the meetings. May be this is the best way to use do this task.

## how to organize teams in an open source project

https://docs.github.com/en/organizations

- github by default has one distinction: org member and contributor

### create diagrams and flowcharts
https://docs.github.com/en/get-started/writing-on-github/working-with-advanced-formatting/creating-diagrams

### approaches to documentation
There are two places where documentation of a project can live.
- Wiki
- in repo like `docs`

Preferred one is in the repo and not wiki. As there are many advantages:
- it is versioned
- you can integrate it with automation (e.g. trigger a GH action when someone commits in `docs` repo)
- Can become part of release notes
- Developers can submit relevant documentation changes along with code changes in the same PR. Reviewer can see complete set of changes and review it.

Wiki can be used to hold temporary documentation. For example, documenting a workaround for a problem that is going to be fixed very soon. It is kind of notepad for project. 

### storing images in your GH repo for documentation
- There has to be guidelines around storing images in GH repo to support documentation, because images can be huge in size and can increse size of your repo dramatically. You should also specify image types allowed.
- There are two ways of storing images:
  - along with the consuming items. for example, images consumed by `docs` can be stored within that directory/repo
  - In case of polyrepo, have a separate repo at org level or in case of monorepo, store images in the same repo but in a separate top level folder, for example `media-assets`. 
  
  Second approach is better because we will need to keep the size of assets in check. And there is no systematic check for that. So, if the media assets are spread across the repo, it is hard to see what is the total size of media assets. If the all the media assets (images, gifs, mp4 videos etc) are in one place then it is easy to watch the size as well as do the clean up.
  Also, we can have GH actions triggered whenever anything is checked into this separate folder/repo. This action can check the size and type of asset being uploaded. It can fail and stop the merge if the asset is not conforming with recommendations.


### branding guidelines
have something like : https://github.com/falcosecurity/falco/tree/master/brand


### test plans and other project management documents
Question is: what is the approach that OSS project take towards storing project management documents (like test-plan document, or may be an mpp)? I think, most of the time they try to convert documents like test plan in to markdown and maintain it in github. If it has to be in word/pdf of any other format, I think project use google drive etc. But need to find out more.

### OSS projects, writting test cases for manual tests
How to do this when using github? I think Jira (Atlassian) lets you create testcases like issues, but in Github there is nothing similar. So we have to document all the test cases in files and store somewhere.


### Hosting source code documentation (like Javadocs) using mkdocs
https://mkdocstrings.github.io/

Right now, only handlers for python are available

https://mkdocstrings.github.io/handlers/overview/

### running markdown linting tool

To install
```
gem install mdl
```

To run
```
mdl ~/IdeaProjects/Janssen/jans/docs/
```

To run with some rule definitions
```
mdl ~/IdeaProjects/Janssen/jans/docs/ -s ~/IdeaProjects/Janssen/jans/automation/markdown/.mdl_style.rb
```


### API design
- API design should happen by creating skeleton code structure first and then generating swagger spec out of it using annotations. See the section on `code first` approach on [swagger site](https://swagger.io/resources/articles/documenting-apis-with-swagger/)
- Also, [stoplight.io](https://stoplight.io/) is a good tool

### Open source projects and secure supply chain
- Reference: https://github.com/microsoft/oss-ssc-framework/blob/main/specification/framework.md


### tool for providing on-demand k8s instances to devs and testers
for the https://github.com/Federation/easycloud/ lovers coming next week you will be also able to create a hassle free k8s clusters on aws with a simple management ui added on top of it. The ui is rancher UI btw. Here is what to expect:

a full blown k8s cluster
Rancher ui which will allow you to easily toggle and view the k8s cluster, install gluu or jans simply with a click of a button and easily view logs and open a terminal without knowing any k8s terminology , sytnax or anything.
The rancher ui will have a dns record assigned and posted for you with the password to login in the PR
You will also be given another dns url to use for gluu or jans deployment as your hostname
Coming next would be adding https://karpenter.sh/ for autoscalling then the last step will finally be enabling the load tests so that we can view any setup and enjoy it without making a hassle about it 🍿


## How to handle discussions on issues

Here are some examples where the community manager, or dev has supported an issue/troubleshooting in a nice way:

https://github.com/canonical/lxd/issues/7910


## how to revert certain decisions which were not received well by community

https://www.keycloak.org/2023/10/reactivating-discourse.html
