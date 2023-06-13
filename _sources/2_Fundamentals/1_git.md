---
jupytext:
  cell_metadata_filter: -all
  formats: md:myst
  text_representation:
    extension: .md
    format_name: myst
    format_version: 0.13
    jupytext_version: 1.14.5
kernelspec:
  display_name: Python 3 (ipykernel)
  language: python
  name: python3
---

# Git and Github

My notes on `git` goes here.

## Basic commands

* `git clone <url-to-remote-repo> .`
  while in the directory `<current dir>`, clone the linked repo to `<current dir>`

* `git status`
  show current branch and status of files in the directory
  
* `git push origin master`
  push to remote `<origin>` repo the local `<master>` branch into the similarly named remote branch


## Undo a push to wrong branch

Problem: Edited file while in wrong branch and pushed to origin. Result as in image.

![Code 0531-1120](https://github.com/ellacharmed/today-I-learned/assets/6437860/bb67f2f9-1916-4c66-9332-44da7057f730)
Initial state

```{figure} https://github.com/ellacharmed/today-I-learned/assets/6437860/bb67f2f9-1916-4c66-9332-44da7057f730
---
scale: 50%
align: left
---
Initial state
```

![Code 0531-1121](https://github.com/ellacharmed/today-I-learned/assets/6437860/ba2148bc-ff1c-4cb8-bb06-9b7332864452)

Solution:
1. `git reset HEAD^` would 
1. then do `git push -f origin <last_known_good_commit>:<branch_name>` to push the named commit to `origin` which means
   - `git push -f origin d7ed56b4:hmwk-2`
1. `git pull --rebase`
1. `git push main`

NOTE: do not merge a branch if there's a PR still pending!
Eg: ella's notes on `#mlops-zoomcamp` _module 01-intro_ is rejected after I merge all WIP hmwk-# branches into `main`
