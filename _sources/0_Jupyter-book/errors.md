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

# Errors

Initial version withtout the title result is below error.

```{error}
/Users/ellaair/MEGA/2 Projects/jupyterbook/today-i-learned/intro.md:1: WARNING: toctree contains reference to document 'errors' that doesn't have a title: no link will be generated
generating indices... genindex /Users/ellaair/MEGA/2 Projects/jupyterbook/today-i-learned/intro.md:1: WARNING: toctree contains reference to document 'errors' that doesn't have a title: no link will be generated
done
writing additional pages... search /Users/ellaair/MEGA/2 Projects/jupyterbook/today-i-learned/intro.md:1: WARNING: toctree contains reference to document 'errors' that doesn't have a title: no link will be generated
done
```

After running `jupyter-book build today-i-learned/` command, following errors in Terminal.
Is `myst` errors due to some missing package?

```{error}
/Users/ellaair/MEGA/2 Projects/jupyterbook/today-i-learned/notebooks.ipynb: WARNING: Executing notebook failed: CellExecutionError [mystnb.exec]
/Users/ellaair/MEGA/2 Projects/jupyterbook/today-i-learned/notebooks.ipynb: WARNING: Notebook exception traceback saved in: /Users/ellaair/MEGA/2 Projects/jupyterbook/today-i-learned/_build/html/reports/notebooks.err.log [mystnb.exec]
```

```{error}
/Users/ellaair/MEGA/2 Projects/jupyterbook/today-i-learned/intro.md:54: WARNING: 'myst' reference target not found: #experiment-two
```

After adding `# Errors`, less errors. 

```{error}
checking consistency... /Users/ellaair/MEGA/2 Projects/jupyterbook/today-i-learned/fundamentals/git.md: WARNING: document isn't included in any toctree
/Users/ellaair/MEGA/2 Projects/jupyterbook/today-i-learned/fundamentals/swe.md: WARNING: document isn't included in any toctree
```

```{error}
writing output... [100%] intro
/Users/ellaair/MEGA/2 Projects/jupyterbook/today-i-learned/errors.md:5: WARNING: Could not lex literal_block as "bash". Highlighting skipped.
/Users/ellaair/MEGA/2 Projects/jupyterbook/today-i-learned/intro.md:55: WARNING: 'myst' reference target not found: #experiment-two
```

[x] Changed `bash` to `zsh` and rebuild

Same.
```{error}
/Users/ellaair/MEGA/2 Projects/jupyterbook/today-i-learned/errors.md:5: WARNING: Could not lex literal_block as "zsh". Highlighting skipped.
```

[x] Removed formatting altogether.

* Reverted _toc.yml to move first .md file in Sections. Need to figure out how to do .md files as links and not in Topic.
* Last error.

```{error}
writing output... [100%] intro                                                            
/Users/ellaair/MEGA/2 Projects/jupyterbook/today-i-learned/intro.md:55: WARNING: 'myst' reference target not found: #experiment-two
```

[x] How to correct above error?

* Make .md files MySt markdown, either copy from another .md or do the [](catch_up#add-yaml-metadata-to-myst-notebooks) step in terminal
