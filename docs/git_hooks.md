# Git Hooks

## Introduction

Git hooks are scripts that are run alongside to some events that happen in a Git repository. The hooks may be used for various workflow purposes, such as deploying new code, linting code, checking errors etc.

## Installation

To install the hooks, simply have a look at the `.git/hooks` folder inside your repository. This folder should be already be present in an existing repository with a few examples. The sample programs are simple Linux shell scripts (identified by the `#!/bin/sh` so-called shebangs). The shebang determines the actual type of the script, some other examples of the shebangs include `#!/bin/bash` and `#!/usr/bin/env python3`.

To ensure that the hooks are runnable, run `chmod +x <script-name>` in the directory. This will update the file permissions for the script.  

## Hook scopes & distribution

Hooks are used in both local and server Git repositories and are not copied to the remote by default. This means that every developer working on a specific project may locally define their own scripts they want to run, matching their personal preferences. Still, there are two ways to share the local hooks with the team:

1. Put the hooks into a separate folder. Simply create a normal folder for the hooks and treat the scripts just as regular repository files. Optionally, it is possible to create a Linux symlink to the `.git/hooks` directory (this means that the directory has 2 or more paths which it resides on, but in reality, the directory is stored just once). This means all of the files will be updated automatically.
2. Use the Git template folder directory, which may be set up via the `$GIT_TEMPLATE_DIR` environment variable or via configuring Git. This will also update the hooks automatically.

We will talk about the server hooks later.




### Server hooks

Server hooks have their place in server repositories. Their job mostly is to enforce some code standards by checking the pushed commits.

There are 3 server-side hooks which trigger the scripts:

- `pre-receive`

- `update`

- `post-receive`

`Pre-receive` is run everytime an user uses `git push` to push their commits to the remote repository. This hook runs just once, just before any branch refs are updated. This is the stage where non-conforming commits may be rejected by the server, this includes running code errors, warnings, linting issues, wrong commit messages etc. The script has no parameters and is invoked with `<old-ref-value> <new-ref-value> <ref-name>` on each line of the standard input, which may be parsed by the server.

An example of a `pre-receive` bash script follows:

```bash
#!/bin/bash
set -e

while read -r oldrev newrev refname; do
    echo $oldrev $newrev $refname
done
```

`Update` script is invoked after the `pre-receive` script finishes. It is invoked separately for each pushed branch, so for three pushed branches, the `update` script is invoked three times. The same three arguments are passed to the script, but differently from `pre-commit`, `update` does not ready from the standard input.

`Post-receive` script is invoked after a successful `git push` operation which means it may be used for post-push cleanup or notifications (typically e-mails). It does not receive any arguments, but like the `pre-receive` script, it may read the same values from standard input.

## Connection to CI/CD (bonus)

As a bonus, we may notice that Git hooks are somehow similar to CI/CD (continuous integration & deployment). CI/CD scripts typicall runs code builds, tests and deployments after successful pushes. Many Git online services provide this behaviour including GitHub and GitLab with options to run much more complicated things using Docker containers. This creates an opportunity for highly-automated development. As this is out of the scope for this project, we highly recommend to check it out yourself (e.g. [here](https://resources.github.com/ci-cd/)).

## Summary

Git hooks provide a way to run scripts based on various Git actions. They are put into the `.git/hooks` repository and based on their name they are invoked with certain actions. There were introduced two main types of hooks, local and server-sided. In the end, we have briefly introduced the reader to the topic of CI/CD.
