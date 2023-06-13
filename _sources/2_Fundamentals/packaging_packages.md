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

# How to update packages and install locally

Problem:
- projects become abandoned
- dependencies get updated and maintainers not responding to merge PRs, as it is a hobbyist project and not a full-time concern

Solution:
- clone and update locally

Case Study:
- has 2 issues:
  1. dependency `https://github.com/ultrafunkamsterdam/undetected-chromedriver` has been continously updated to keep up with Chrome browser updates, but the main package `https://github.com/TRoboto/datacamp-downloader` has not been touched in 3 years


Steps:

- note: <br/>
  a. after packages installed, need to close powershell window and relaunch; especially to login with `datacamp login` or via `datacamp set-token <token>` commands <br/>
  b. in order to login, Chrome browser needs to be installed

- first thing is to correct the error of <br/> `OSError: [WinError 6] The handle is invalid`
  - merge a specific pull request done by contributor `gvmii` that has not yet been merged by maintainer `TRoboto` : <br/> `pip install git+https://github.com/gvmii/undetected-chromedriver@gvmii-patch-1`

- next is to take care of the issue <br/> `ModuleNotFoundError: No module named 'undetected_chromedriver.v2'`

- edit the datacamp-downloader repo to remove the `.v2` that has been deprecated after being merged into `main` branch in `undetected_chromedriver` package
  - edit line#6 in file `src\session.py` to remove the `.v2` so the <br/> before: `import undetected_chromedriver.v2 as uc` becomes <br/> after: `import undetected_chromedriver as uc`

- after that, we're ready to rebuild package
- first need to install `build` with `pip install build`
- next is to edit the `pyproject.toml` as setuptools is being deprecated.
- the contents of `pyproject.toml` that finally works is

```python
[build-system]
requires = ["setuptools>=42", "wheel"]
build-backend = "setuptools.build_meta"

[project]
name = "datacamp-downloader"
version = "3.2.1"
description = "Download your completed courses on Datacamp easily!"
readme = "README.md"
authors = [
    {name = "Mohammad Al-Fetyani", email = "m4bh@hotmail.com"},
    {name = "Ella", email = "ellacharmed@gmail.com"}
]
license = {file = "LICENSE"}
classifiers = [
    "Programming Language :: Python :: 3",
    "License :: OSI Approved :: MIT License",
    "Operating System :: OS Independent",
]
dynamic = ["dependencies"]
requires-python=">=3.6"

[tool.setuptools.dynamic]
dependencies = {file = ["requirements.txt"]}

[project.scripts]
datacamp = "datacamp_downloader.downloader:app"

[project.urls]
homepage = "https://github.com/TRoboto/datacamp-downloader"
repository = "https://github.com/TRoboto/datacamp-downloader"
"Bug Tracker" = "https://github.com/TRoboto/datacamp-downloader/issues"
```

- to be safe uninstall old version first `pip uninstall datacamp-downloader`
- then `cd dist` 
- and `pip install .\datacamp_downloader-3.2.1-py3-none-any.whl`
- to see list of completed _courses_, use `datacamp courses`
- to see list of completed _tracks_, use `datacamp tracks`
- note that only **_completed_** content would be shown and available for download

```bash
PS D:\tools\datacamp-downloader> datacamp tracks
+--------+------------------------------------------+------------+
| ID     | Title                                    | Courses    |
+--------+------------------------------------------+------------+
| t1     | Python Programmer                        | 17         |
+--------+------------------------------------------+------------+
| t2     | Python Fundamentals                      | 4          |
+--------+------------------------------------------+------------+
```

- and start download with 
  - all tracks: `datacamp download all-t` or 
    > This by default will download videos, slides, datasets, exercises, english subtitles and transcripts in organized folders in the current directory.
  - all courses: `datacamp download all` or
  - individual courses: `datacamp download 1 2` to get the first and second course

```bash
PS D:\tools\datacamp-downloader> datacamp courses
+--------+------------------------------------------+------------+------------+------------+
| ID     | Title                                    | Datasets   | Exercises  | Videos     |
+--------+------------------------------------------+------------+------------+------------+
| 1      | Introduction to Python                   | 2          | 46         | 11         |
+--------+------------------------------------------+------------+------------+------------+
| 2      | Intermediate Python                      | 3          | 69         | 18         |
+--------+------------------------------------------+------------+------------+------------+
| 3      | Data Manipulation with pandas            | 4          | 41         | 15         |
+--------+------------------------------------------+------------+------------+------------+
| 4      | Supervised Learning with scikit-learn    | 4          | 34         | 15         |
+--------+------------------------------------------+------------+------------+------------+
| 5      | Python Data Science Toolbox (Part 1)     | 1          | 34         | 12         |
+--------+------------------------------------------+------------+------------+------------+
| 6      | Joining Data with pandas                 | 23         | 36         | 15         |
+--------+------------------------------------------+------------+------------+------------+
```

