# Monorepo notes

Reference:
1) overview: https://www.youtube.com/watch?v=rdeBtjBNcDI
2) optimize git performance for a monorepo: https://www.youtube.com/watch?v=RcqLV1lU408
3) 

Plan:
- branching strategy
- branch protections
- checks (commit message check, sonar check etc)
- Know what will stay with old repo and not move to new repo
  - branches
  - PR conversations and review comments.
  - PR commit history (it'll be single commit in new repo)
  - issue labels

Create a new repo which will be you Monorepo
- Create labels (labels can't be transferred). Most importantly have labels for each component. Like `comp-componentname`. You will apply this labels to issues and PRs as you move them from respective repository to monorepo. In absence of these labels, issues/prs will be lumped together at the repo-level. No way to find out which issue/PR belonged to which component/module.
- enable checks (like signed commit, convensional commit and other branch protection)
- give write permissions to the team members who will need it to push branches for PR move

Move each repo as subfolder of monorepo
- transfer issues manually and relabel them with appropriate `comp-` label
- moving PRs
  - don't move closed PRs. They say in the old repo which will be archived. And commits have been already merged so commits will move.
  - Open PRs basically represent code which is not yet merged in trunk. Code is still in the feature branches. There are two ways get this code over to new repo
    - Copy over
      - In this approach, we ask PR owner to 
        - clone new monorepo
        - create a new branch from the trunk of the monorepo (name prefixed with `modulename-`)
        - then copy over files with code changes to new branch
        - push the new branch
        - create new PR.
      - Basically, we are not moving PR here. We are just copying the code. Easiest and least error prone approach. 
    - Rebase branch
      - In this approach, we ask PR owner to 
        - add monorepo as a new remote
        - create a new branch from the trunk of the monorepo (name prefixed with `modulename-`)
        - rebase you current branch with changes on this new branch
        - push and create new PR
      - In this approach, we maintain the commit history. More complex than `copy over` approach.
  - In either approach, we had following points as checklist for PR owners:
    - branch name should have component name as prefix, like `modulename-`
    - commits should be signed
    - use convensional commits
    - link new PR to old PR
    - Apply appropriate component label `comp-`
