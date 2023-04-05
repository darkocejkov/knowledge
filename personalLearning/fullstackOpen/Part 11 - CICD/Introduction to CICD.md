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
CI/CD processes or tools should have their own server setup independent of all other processes to minimize conflict

- Self-hosted
	- Jenkins
- Cloud-based
	- Github Actions
	- 