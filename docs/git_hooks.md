# Git Hooks

## Introduction

Git Hooks are scripts that are run alongside to some events that happen in a Git repository. The hooks may be used for various workflow purposes, such as deploying new code, linting code, checking errors etc.

## Installation

To install the hooks, simply have a look at the `.git/hooks` folder inside your repository. This folder should be already be present in an existing repository with a few examples. The sample programs are simple Linux shell scripts (identified by the `#!/bin/sh` so-called shebangs). The shebang determines the actual type of the script, some other examples of the shebangs include `#!/bin/bash` and `#!/usr/bin/env python3`.

To ensure that the hooks are runnable, run `chmod +x <script-name>` in the directory. This will update the file permissions for the script.  


