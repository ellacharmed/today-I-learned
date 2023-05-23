# Sharing data across notebooks, scripts

Q: How to carry over variables across different files, if everything is split by the areas of concern?

A: In `.py` scripts, pass variables just like modules `package_name.module.var`. More reading 

* [Jason Brownlee blog post](https://machinelearningmastery.com/running-and-passing-information-to-a-python-script/)
* [stackoverflow pass-variable-between-python-scripts](https://stackoverflow.com/questions/16048237/pass-variable-between-python-scripts)

A: In Jupyter notebooks, with the `%store` magic command.

Example from: 
- [source](https://avichawla.substack.com/p/transfer-variables-between-jupyter)
- [stackoverflow answer #1](https://stackoverflow.com/questions/35935670/share-variables-between-different-jupyter-notebooks)
- [stackoverflow answer #2](https://stackoverflow.com/questions/31621414/share-data-between-ipython-notebooks)

```
# in notebook 1 
value = 10

%store value
```

```
# in notebook 2 
%store -r value
print(value)
```