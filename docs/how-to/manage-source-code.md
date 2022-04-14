---
title: How to Manage Source Code
---

Source code for EC2U Connect Centre services is collaboratively managed on [GitHub](https://github.com/ec2u). Each
service is hosted on a dedicated GitHub project, managed according to the following shared guidelines.

# Configuration

- install Git / GitHub Desktop
- clone project repository
- configure committer profile to avoid leaking your personal email to Git logs

    ```bash
    git config user.name "Name Surname"
    git config user.email "name.surname@work.com"
    ```

> :exclamation: Make sure to use your work/university email.

# Git Workflow

- Loosely structured according to [http://releaseflow.org/](http://releaseflow.org/) guidelines

## Release Branches

```
release/<major>.<minor>
```

- versions names are assigned according to [https://semver.org/](https://semver.org/) guidelines
- CI pipelines are triggered by pushes / pull requests on release branches
- CD pipelines are triggered by `<major>.<minor>.<patch>` version tags

> :exclamation: Note no leading `v` in version tags

## Work Branches

```
feature/<feature-name>
bugfix/<issue-number>-<short-description>
```

- work branches are branched from and back-merged to the relevant release branch
- after merging into release branch, relevant changes/fixes are back-ported to other release branches by **
  cherry-picking** them

## Main Branch

The `main` branch is automatically synced to the latest stable release branch.

# Commit

## Policies

- before merging to a deployment branch, make sure to interactively squash feature commits to a handful of consistent,
  self contained and documented commits

## Messages

According
to [Spring Contributing Guidelines](https://github.com/spring-projects/spring-framework/blob/30bce7/CONTRIBUTING.md#format-commit-messages)
, with the highlighted deviations

1. Use imperative statements in the subject line, e.g. `Fix broken Javadoc link`
2. Begin the subject line sentence with a capitalized verb, e.g. `Add, Prune, Fix, Introduce, Avoid,  …`
3. Do not end the subject line with a period
4. Keep the subject line to 50 characters or less if possible
5. Wrap lines in the body at 72 characters or less
6. ~~Mention associated issue(s) at the end of the commit comment, prefixed with "#<issue> " as above~~  
   Mention associated GitHub issue(s) in the subject line, e.g. `Fix #<issue number>: now …`,
   using [GitHub issue linking keywords](https://docs.github.com/en/get-started/writing-on-github/working-with-advanced-formatting/using-keywords-in-issues-and-pull-requests)
7. In the body of the commit message, explain how things worked before this commit, what has changed, and how things work
   now