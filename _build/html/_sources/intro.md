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

# Welcome to EllaLearns

A compilation of study notes.

Remember that the Download button to save as `.html` or `.pdf` would "print" only the current html page, not the whole jupyter-book.

## Experiment One

* Added folders by `Subject` and `topic` markdown files to see how it is compiled into a book.
* Not using numbering, so content is sorted alphabetically
* First testing. With one file in each folder.
```yaml
format: jb-book
root: intro
chapters:
- file: markdown
- file: markdown-notebooks
- file: fundamentals/git
- file: jupyter-book/howto-dosomething
- file: machinelearning/classification
- file: python/atopic
```
* Second testing, with at least 2 files in some folders.
```yaml
format: jb-book
root: intro
chapters:
- file: markdown
- file: markdown-notebooks
- file: fundamentals/git
  sections:
  - file: fundamentals/swe
- file: jupyter-book/howto-dosomething
- file: machinelearning/classification
  sections:
  - file: machinelearning/regression
- file: python/atopic
  sections:
  - file: python/oop
```
* moved .md to file: section resulted in errors.

### Result

![output of above toc](images/experiment2-result.png)

## Experiment Two

[x] TODO. Need to figure out how to do .md files as links and not in Topic.
[x] TODO. Using numbering, so content is sorted in the order I want.
[x] TODO. Set up as git repo before doing `{ref}`experiment-two <experiment-two>`. I want to keep the different versions of the _toc without numbering them manually. But then cannot access each file unless I switch to that branch... Hmmm. Maybe manual numbering and then commit each experiments as an atomic change instead of in separate branches.

_note_: ToDos need to be

* in CAPS
* have a checkbox 

before it is gathered by the TODO extension in a tree

## Experiment Three

* renumbered folders with prefixes to folder name to the desired order of appearance
* made a landing page for Topics 0 & 1
* result in some errors as not all folders and files are in _toc.yml

```yaml
format: jb-book
root: intro
chapters:
- file: README
- file: 0_Jupyter-book/landing
  sections:
  - file: 0_Jupyter-book/commands
  - file: 0_Jupyter-book/errors
  - file: 0_Jupyter-book/sample intro
  - file: 0_Jupyter-book/sample markdown
  - file: 0_Jupyter-book/sample markdown-notebooks
  - file: 0_Jupyter-book/sample notebooks.ipynb
- file: 1_Fundamentals/landing
  sections:
  - file: 1_Fundamentals/0_swe
  - file: 1_Fundamentals/1_git
- file: 2_Python/landing
  sections:
  - file: 2_Python/atopic
  - file: 2_Python/oop
- file: 4_Machine Learning/landing 
  sections:
  - file: 4_Machine Learning/0_Python resources
  - file: 4_Machine Learning/0_ML resources
  - file: 4_Machine Learning/0_How to Learn ML  
  - file: 4_Machine Learning/1_classification
  - file: 4_Machine Learning/2_regression
  - file: 4_Machine Learning/WWCode NLP Workshop
- file: 9_Books/landing
  sections:
  - file: 9_Books/Burkov, Hundred Page Machine Learning Book
  - file: 9_Books/Burkov, Machine Learning Engineering
- file: 9_Courses/landing
  sections:
  - file: 9_Courses/cs50-path
  - file: 9_Courses/scikit-learn-mooc
- file: 9_Practicals/landing
  sections:
  - file: 9_Practicals/Practice
  - file: 9_Practicals/Predict AIAP timeline
  - file: 9_Practicals/titanic-dataset
```

### Results

Looking good! Understood the structure and desired naming conventions now.

![experiment3-result](images/experiment3-result.png)

## Questions / Next Actions

[x] TODO, if want to convert one markdown file or several files into an `article`, how do I go about doing that?
* see [Build an article from a single file](https://jupyterbook.org/en/stable/structure/toc.html#structure-of-an-article)

[x] TODO. Is `myst` errors due to some missing package?

It was perhaps because `_config.yml` was renamed to `_config_v0.yml`. Made a copy with my edits. No more errors.

Yes, missing packages needed :
* jupytext

And then to run the command, to use MySt version of markdown, the `.md` file need the yaml frontmatter
`jupyter-book myst init today-i-learned/intro.md --kernel python3`

And to use myst syntax instead of markdown
`{ref}`MyST syntax lecture <myst_cheatsheet>`

So, for my error: `{ref}`experiment-two <experiment-two>`

Source: https://jupyterbook.org/en/stable/reference/cheatsheet.html

[ ] TODO. How to generate .pdf instead of html?
* [Build a PDF](https://jupyterbook.org/en/stable/advanced/pdf.html)
* Need to install more packages. Either `pyppeteer` or `texlive`
  * [pyppeteer](https://github.com/pyppeteer/pyppeteer)
  * [texlive](https://www.tug.org/texlive/)

## Table of Contents
```{tableofcontents}
```
