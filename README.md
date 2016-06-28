# py2ipynb

Converts a .py python source file to a V.4 .ipynb jupyter/ipython notebook.

Based on [this](http://stackoverflow.com/a/32994192/4720148) and [this](http://stackoverflow.com/a/35720002/4720148) posts. Question originally asked on [stackoverflow](http://stackoverflow.com/questions/23292242/converting-to-not-from-ipython-notebook-format).

*(Forked from [py2ipynb](https://github.com/gatsoulis/py2ipynb))*

This fork aims to allow back in forth between an ipynb jupyter/ipython notebook and the exported .py file. We want to allow using source control and revision comments on the .py file and import back into a notebook as a deployment step.

*Adaptations*

- Using pycharm style since it seems to correspond to the notebook export style
- Make Python3 friendly

## Prerequisites

This script has been tested with Python 3.5.2. The versions of dependencies specified in the [requirements.txt](requirements.txt) are based on the versions needed by jupyter 1.0.0. If you upgrade your jupyter installation, you might have to adjusts the requirements accordingly.

## Usage

```shell
$ python3 py2ipynb.py from-notebook.py to-notebook.ipynb
```

### Caveats

Unfortunately, the out-of-the-box Jupyter converter to .py does not deliminate Markdown cells, it just puts the Markdown in comments. Doing so, we don't know when a code cell ends and a Markdown cell begins. If we do want to restore Markdown properly, this suggests we should develop a custom exporter. The project is [nbconvert](https://github.com/jupyter/nbconvert). The current [Jinja](http://jinja.pocoo.org/) template file is [python.tpl](https://github.com/jupyter/nbconvert/blob/master/nbconvert/templates/python.tpl). The template and/or code must be modified to suit the Markdown cell marker like so:

```python
##
# md
"""
# Header

* item 1
* item 2
"""
```

