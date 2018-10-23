# Auto Documentation using Sphinx
1. Preparation
- document your code in google style or numpy style
- install Sphinx `python3 -m pip install Sphinx`

2. Start
```shell
$ mkdir project
$ cd project
$ mkdir scripts rst html  # scripts for your Python code
# rst for document files
# html for generating html
$ sphinx-quickstart .     # build a scaffold of documentation for us
```
- `quickstart` mode will walk you through a series of questions, and mostly you can use the defaults except `Project name: ` and `autodoc: y`
- NOTES about some of the questions:
- `doctest: y` can automatically test code snippets in doctest blocks
- `viewcode: y` can include links to the source code of documented Python objects

- After this step, we will have several new files and directories:
- directories: `_build`, `_static`, `_templates`
- files: `conf.py`, `index.rst`, `Makefile`

3. Configure settings
in `conf.py`
- choose a html theme, e.g. `html_theme = 'sphinx_rtd_theme'`
- more themes can be found [here](http://www.sphinx-doc.org/en/stable/theming.html#builtin-themes)
- tell where our scripts are; after `import sys` and `import os`
- `sys.path.append('/path/to/project/scripts')`
- or simply use the one provided `sys.path.insert(0, os.path,abspath('.'))`
- translate our google or numpy style documentation
- `extensions = [ ..., 'sphinx.ext.napoleon']`
- below that, we can add some configuration options e.g. how the parameters and return types for functions are formatted in the generated documentation to [tastes](http://www.sphinx-doc.org/en/stable/usage/extensions/napoleon.html#configuration)

4. Make html
```shell
$ make clean
$ make html  # generate some of the static HTML
```

5. Auto generate docs
```shell
$ sphinx-apidoc -o /path/to/project/rst /path/to/project/scripts
```

6. Tricks
```shell
$ cd rst

$ cp modules.rst index.rst
$ mkdir _static
$ cp ../conf.py .
```

7. Build html
```shell
$ sphinx-build -b html /path/to/project/rst /path/to/project/html
```


- DONE! You have just build all static HTML docs under directory `/html`

- THEN, serve the docs locally on your computer!
```shell
$ cd /path/to/project
$ python3 -m http.server
```

- THEN, you can see your docs at http://localhost:8000/_build/html/index.html

- BUT, what if you want to change something?
1. `$ cd rst`
2. Remove all files in `rst`: `$ rm -rf *`
3. Do tricks again: `$ cp ../conf.py .` and `$ mkdir _static`
4. Auto generate docs again: `$ sphinx-apidoc -o /path/to/project/rst /path/to/project/scripts` 
5. `$ cp /path/to/project/index.rst .`
6. Build again: `$ sphinx-build -b html /path/to/project/rst /path/to/project/html/` 


*references:*
> [python3 sphinx documentation generator - YouTube](https://www.youtube.com/watch?v=qrcj7sVuvUA)  
> [Practical Sphinx PyCon 2018](https://www.youtube.com/watch?v=0ROZRNZkPS8)  
> [How to sphinx and readthedocs](https://samnicholls.net/2016/06/15/how-to-sphinx-readthedocs/)  
