# Git Hooks

## Introduction

Git Hooks are scripts that are run alongside to some events that happen in a Git repository. The hooks may be used for various workflow purposes, such as deploying new code, linting code, checking errors etc.

## Installation

To install the hooks, simply have a look at the `.git/hooks` folder inside your repository. This folder should be already be present in an existing repository with a few examples. The sample programs are simple Linux shell scripts (identified by the `#!/bin/sh` so-called shebangs). The shebang determines the actual type of the script, some other examples of the shebangs include `#!/bin/bash` and `#!/usr/bin/env python3`.

To ensure that the hooks are runnable, run `chmod +x <script-name>` in the directory. This will update the file permissions for the script.  

## Hook Scopes & Distribution

Hooks are used in both local and server Git repositories and are not copied to the remote by default. This means that every developer working on a specific project may locally define their own scripts they want to run, matching their personal preferences. Still, there are two ways to share the local hooks with the team:

1. Put the hooks into a separate folder. Simply create a normal folder for the hooks and treat the scripts just as regular repository files. Optionally, it is possible to create a Linux symlink to the `.git/hooks` directory (this means that the directory has 2 or more paths which it resides on, but in reality, the directory is stored just once). This means all of the files will be updated automatically.
2. Use the Git template folder directory, which may be set up via the `$GIT_TEMPLATE_DIR` environment variable or via configuring Git. This will also update the hooks automatically.

We will talk about the server hooks later.


