# compilation

compilation of commands and notes on how-to use jupyter-book

[Reference](https://jupyterbook.org/en/stable/intro.html) for the Official Documentation

## Generate _toc.yml

Using `base` venv,
`jupyter-book toc from-project today-i-learned -f jb-book`

### Build the book

From the parent of the book ie from outside the `<book-to-be-build>` directory, 
`jupyter-book build today-i-learned/`
or
`jb jupyter-book build today-i-learned/`

Result: some errors:
```
/Users/ellaair/MEGA/2 Projects/jupyterbook/today-i-learned/markdown.md:39: ERROR: Unknown interpreted text role "cite".
/Users/ellaair/MEGA/2 Projects/jupyterbook/today-i-learned/markdown.md:49: ERROR: Unknown directive type "bibliography".
/Users/ellaair/MEGA/2 Projects/jupyterbook/today-i-learned/notebooks.ipynb: WARNING: Executing notebook failed: CellExecutionError [mystnb.exec]
/Users/ellaair/MEGA/2 Projects/jupyterbook/today-i-learned/notebooks.ipynb: WARNING: Notebook exception traceback saved in: /Users/ellaair/MEGA/2 Projects/jupyterbook/today-i-learned/_build/html/reports/notebooks.err.log [mystnb.exec]
```

[x] TODO. Change `yml` to `yaml` in `intro.md`
