# Git Hooks

This is a page that will contain more information about Git Hooks.

<img src="./obrazek1.jpg" alt="Visualization" />

## Local hooks

As already mentioned, the hooks can be modified by the contributor. Local hooks only apply to the repository in which they are installed.
Some examples of the local hooks are:
- pre-commit
- prepare-commit-msg
- commit-msg
- post-commit
- post-checkout
- post-rebase


#### Pre-Commit
The `pre-commit` hook is naturally linked to `git commit` command.
It is executed before you even type in a commit message.
Serves to check the snapshot to be committed, to ensure your commits meet some (formal) requirements or do not break any existing functionality.
If the script in the `pre-commit` hook returns a non-zero exit code, the commit is prevented.

This example of a `pre-commit` prevents incorrect authors from committing and checks the signing key:

```bash
#!/bin/bash

PWD=`pwd`
globalEmail=`git config --global --get user.email`
signingKey=`git config --global --get user.signingkey`
workEmail="example@axosoft.com"

if [[ $PWD != "*demo*" && $globalEmail != $workEmail ]];
then
        echo "Commit email and global git config email differ"
        echo "Global commit email: "$globalEmail""
        echo "Committing email expected: $workEmail"
        exit 1
elif [[ $signingKey -eq "" ]];
then
        echo "No signing key found. Check global gitconfig"
        exit 1
else
        echo ""
        exit 0
fi
```
