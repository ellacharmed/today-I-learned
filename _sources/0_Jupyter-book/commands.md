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

# jb Commands Compilation

Compilation of commands and notes on how-to use jupyter-book

[Reference](https://jupyterbook.org/en/stable/intro.html) for the Official Documentation

## Generate _toc.yml

Using `base` venv,

`jupyter-book toc from-project today-I-learned -f jb-book`

`jb toc from-project . -f jb-book`

## Build the book

From the parent of the book ie from outside the `<book-to-be-build>` directory, 

`jupyter-book build today-I-learned/`

or

`jb build today-I-learned/`

or 

`jb build .`

Result: some errors:

```{error}
/Users/ellaair/MEGA/2 Projects/jupyterbook/today-i-learned/markdown.md:39: ERROR: Unknown interpreted text role "cite".
/Users/ellaair/MEGA/2 Projects/jupyterbook/today-i-learned/markdown.md:49: ERROR: Unknown directive type "bibliography".
/Users/ellaair/MEGA/2 Projects/jupyterbook/today-i-learned/notebooks.ipynb: WARNING: Executing notebook failed: CellExecutionError [mystnb.exec]
/Users/ellaair/MEGA/2 Projects/jupyterbook/today-i-learned/notebooks.ipynb: WARNING: Notebook exception traceback saved in: /Users/ellaair/MEGA/2 Projects/jupyterbook/today-i-learned/_build/html/reports/notebooks.err.log [mystnb.exec]
```

## publish to github pages

Caveat to using gh-pages: repo must be public. Link to [ellalearns book](https://ellacharmed.github.io/today-I-learned/intro.html)

For a new book, execute following snippet in terminal.
```{tip}
pip install ghp-import
ghp-import -n -p -f _build/html/
```

`ghp-import` will push to gh-pages branch in the current repo

From the PyPi docs of this package

```
Usage: ghp-import [OPTIONS] DIRECTORY

Options:
  -n, --no-jekyll       Include a .nojekyll file in the branch.
  -c CNAME, --cname=CNAME
                        Write a CNAME file with the given CNAME.
  -m MESG, --message=MESG
                        The commit message to use on the target branch.
  -p, --push            Push the branch to origin/{branch} after committing.
  -x PREFIX, --prefix=PREFIX
                        The prefix to add to each file that gets pushed to the
                        remote. Only files below this prefix will be cleared
                        out. [none]
  -f, --force           Force the push to the repository.
  -o, --no-history      Force new commit without parent history.
  -r REMOTE, --remote=REMOTE
                        The name of the remote to push to. [origin]
  -b BRANCH, --branch=BRANCH
                        Name of the branch to write to. [gh-pages]
  -s, --shell           Use the shell when invoking Git. [False]
  -l, --follow-links    Follow symlinks when adding files. [False]
  -h, --help            show this help message and exit
```

## Build to PDF (whole book)

from outside `today-I-learned/` use 
`jb build today-I-learned/ --builder pdflatex`

from within book folder
`jb build . --builder pdfhtml` or `jb build . --builder pdflatex`

## Next actions

[x] Change `yml` to `yaml` in `intro.md`
