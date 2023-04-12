CI/CD stands for **Continuous Integration, Continuous Deployment**. It's a process that involves the high-level tooling and project management of serving production-grade software, while being able to continuously integrate and deploy changes from developer branches to production efficiently, quickly, and with accuracy.

Not only is it challenging to manage what and how changes should make it to production, when other developers and team members are involved, it becomes really difficult to figure out a tight process on how to manage all the valuable work everyone does.
___
# Vocabulary

## Branches
- Branches are copies or *versions* of code that exist seperately without overwriting each other
- In a *git* repo, the default (any only branch) is *master* or *main*
	- All branches *branch* off the the "root"
	- A branch is a seperate version from the one you branch *off of*, with various changes to the code
- Enables the ability to work on a foundation, an existing codebase and create branches from some master copy, to apply changes to, without disturbing the master copy until the new changes are ready to become part of the master

## Pull Request
- Based on branches, if you have an off-branch and want to *merge* changes from that branch to another one, you typically initiate a **pull request** (PR)
- It's a *manual request and check process*, to verify that the new changes to code are actually suitable for merging

## Build
- Depends on the contextual environment
	- Python / Ruby are entirely *interpreted* (line-by-line), and there doesn't need to be a *build step* to pre-process code to be able to run.
- Build steps depend not only on the language you use, but where you intend to run the code on, and any various optimizations you would like to add.

## Deploy
- Putting some version of the software on a platform that enables users to access and use it
- Web application deployment has various levels of complexity. 
	- If we "deploy" our code to netlify for example, and we don't care about anything else - assuming our built code works, the code will easily be deployed on the internet for end-users
	- however, if we are not using Netlify, and are self-hosting instead, there's a lot more complexity to deploy
- In any project, you'd want to set up a *deployment pipeline* which is an automatic sequence of operations that allows you to deploy software

# CI? CD?
- CI = Continuous Integration
	- "integration" is the merging of changes to some main branch\
- CD = Continuous Delivery
	- "delivery" is the ability to deploy changes, typically automatically, with a high degree of availability to the product itself, and consistency in the output of changes (that we are not deploying breaking changes)
- Sure, it's simple enough to just merge your changes, but there's a lot more that needs to happen to offer protection to your code.
	- For example, do you test *after* the changes are merged? what if there's a bug? would you *revert*, then test and fix, then re-merge?
	- Thus, it's pretty obvious that we only want to merge when code is clean, working, and has little likelihood to break other code when merged
- Typical steps of integration:
	1. Linting
		- Clean, formatted code
	2. Building
		- Process code to bundle into a runnable state
	3. Testing
		- Some process to be able to run tests and verify against known truths
	4. Packaged
		- Put code into an easily movable batch/medium
	5. Deploy
		- Release code into the runnable environment

- In development and testing, it might not be a big deal that these operations takedown the production or halt access, but this process is a really difficult and tedious one because it deals almost entirely with configuration and tools. 

# Why?
- Whether its working on a solo project, or with other developers, creating a CI/CD process is the best move because having to manually take care of these long steps can lead to errors. 
- It's a process that exists in the middle to make it harder to let mistakes through to production, because sometimes all that's needed is a hotfix, and if you try and bypass these stages, you're going to introduce *more* errors.

## Goal
> The goal of CI/CD is not CI/CD itself, but the outcome and automation of these tasks that leads to better, less buggier code.

# Principles
- Documented Behaviour
- The best tests are worthless if we don't run them
- The same things should happen everytime, or the required tasks are performed in the same order
- Keep code always deployable, so that it minimizes the amount of time spent "catching up"
- Keep track of what version of code *is* deployed, through some unique ID; even better if we have a mapping of versions to history of releases

# Types of CI Setups
CI/CD processes or tools should have their own server setup inde\pendent of all other processes to minimize conflict

- Self-hosted
	- Jenkins
- Cloud-based
	- Github Actions

# GitHub Actions
- This solution is a great one if you use GitHub, as it's a cloud-based CI/CD tool, and it comes directly from the same source as your repository
	- Although it's a different tool from GitHub repos, since it integrates super easily and well, it enables this CI/CD solution to skip various configuration steps of authentication, pub-sub events, etc...

## Workflows
- process flows that run automated steps
- it's a collection of *at least* one or more Jobs, which each have 1+ steps
	- Jobs are executed in parallel, while each step within a single job is sequential

- Workflows execute on the action of of a *trigger*:
	- GitHub event (pushes commit to repo, issue or PR created)
	- time scheduled event (cron-syntax)
	- external event such as a Slack/Discord message/command

# Deployment
- This is one of the most intense and complex areas to configure
- Having a bad deployment process can lead to very bad things for the users of the app, and perhaps even for developers!

## The Point
- The entire point of having some CI/CD process is that we are able to automate the various cross-platform, sequential steps 
- If at any point in the CI/CD process something fails, we shouldn't continue the process, and we especially shouldn't deploy any code that is not processed, tested, etc ...
- A good deployment system will:
	- fail gracefully *anywhere*, 
	- should never leave production/releases broken, 
	- be verbose about errors and when/what/why
	- should allow *rollbacks* in the case of broken software
	- should only deploy when the requirements are met
		- all tests pass, there's a certain level of total code coverage with tests, etc...

# Versioning
- Important to understand which versions of code are released, a "snapshot" can be identified by the version that is assigned to it.
- If versioning is in place, we can identify the history, either relative to timestamps, or to the versions themselves. If a specific version has some critical bug, we can "rollback" to the previous, given that we have version

## Semantic
- AKA *semver*, is a versioning strategy
	- `{major}.{minor}.{patch}`
		- patches are about *fixing* existing functionality
		- small changing to functionality are *minor*
		- complete changes of application/functionality are *major*
	- npm packages use semver

## Hash
- Hash versioning, AKA SHA versioning
- the version "number" is a *hash* based on the contents of the version itself
- all git commits are SHA versioned

## `semver` vs. `sha`
- The semver approach is very useful for any releases that are meant to be human readable, that you are able to parse information about history, chronology, and general information about a release through its semantic version
	- for example, if you're upgrading an *npm* package, you might want to upgrade to a version that is the *next* highest minor update, because changing major versions much introduce too many breaking changes
		- even though knowing this depends on knowing changes of the package itself, and whether or not your specific use would introduce breaking changes - it's still really easy to find out
	- 
- the SHA approach is much more suited to an *artifact* version, say the artifact of a build phase. 
	- because it's a hash, it's inherentely unique based on the contents
	- since it's unique, and quite difficult for human comparison, it's really great for automated comparison between hashes, 