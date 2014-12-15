# Gitography Workflow

The gitography workflow is loosely inspired by the github-flow approach, but with
alterations made to help ensure a greater chain of custody from end to end. Our
goal with this workflow is to enable continuous, stable releases while also
providing a comprehensive audit trail from user story/defect through to release
and issue closure.

## Overview
The gitography workflow uses a central repository to act as the communications
hub between developers. As with most git workflows developers are expected to
work locally and push to the appropriate named branches as needed.

One of the main areas where gitography is different to other workflows is in
it's concept of a project driven model. From the perspective of git, a project
is defined as the combination of two repositories, code and environment. The
code repository contains the source code to be built/deployed where as the
environment defines the infrastructure the source code is to be built/deployed upon.

In addition to the mapping between projects and repositories we also use this
concept to define our branching model. Any user stories or defects raised within
a project will have a coresponding, 1:1 relationship with a branch in both the code
and environment repositories which is branched from master.

When a push is made by a developer to a named branch, an automated build will
take place which comprises of a code repository and named branch and a
corresponding environment repository and named branch. It is not important for
the build or tests at this stage to succeed, merely that the reason for it not
succeeding is reported back into the environment branch and that branches are
being built successfully before being merged to master.

The final element to all of this is that the master branch for a project should
always be kept in a deployable state. The ideal situation is that merges to
master automatically kick of a new deployment, however this is sometimes not
feasible or desirable.

## Key Concepts

The following key concepts are fundamental to the gitography workflow.

- We work from the concept of a project driven workflow with mappings between
projects, user stories/defects and reposotories/branches

- Everything branches from master.

- Anything in master is deployable and SHOULD be deployed as soon as possible 
after a successful merge.

- Work should be conducted on local branches with regular pushes to the server
named branch.

- Any commit to the server named branch will kick of a new build of the
corresponding build repo branch.

## Workflow 

In order to get a better understanding of how Gitography's workflow plays out,
we'll step through a simple project. This project (named StaticWebApp) will consist of 
a simple static web application which exists within a single node and two 
developers, Alice and Bob.

To begin with, Alice creates a new project within the project tracking tool
called 'StaticWebApp', this then creates the associated repositories.

<<<<DIAG PROJECT_CREATION>>>>

After this Alice and Bob both raise user stories. One for the content of the web
application and one for the formating

<<<DIAG Initial User Stories>>>

Alice and Bob both clone the repos to their local machines in order to work on
them. When Alice is ready with her local branch, she pushes up to the
corresponding named branch. This attempts to kick of a build

<<<DIAG Failed Build>>>

Due to the build branch still containing the defaults ( which for this example
is empty ) the build fails. Alice clones the Environment branch to her local
repository in order to setup a Dockerfile build for the job and pushes back to
the named branch.

<<<DIAG Passed Build>>

With her build succeeding, she requests bob does a review of her work. In
parallel, Bob has Alice review his coresponding work on his content branch

<<<DIAG Bobs Work>>>
<<<DIAG Alices Work>>
<<DIAG Completed work>

---TODO---
Master deploy/merge
Upload diags once they are a bit more sane
