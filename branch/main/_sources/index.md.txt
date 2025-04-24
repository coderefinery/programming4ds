# Introduction to Programming for Data Science

In this introductory-level workshop, we will learn the very basics of programming for data science.
What does it mean to code? To "run a script"? Variables and functions?

We will work in [Jupyter Notebooks](https://jupyter.org/) for its simplicity to get started writing
code even without any previous experience. We will learn how to produce some **reproducible plots** using
[Vega-Altair](https://altair-viz.github.io/) and in general how to find your way with programming in Python or R.


## Who is the course for?

- Somebody starting with Python or curious about Python.
- Somebody who needs
  to read, process, and plot data for their work or studies and would like to
  try it out with Python.

:::{prereq} Preparations
- No programming language experience needed, we will start from zero and learn the basics together
- Computer with network access
- {doc}`installation`
:::


## What is not taught?

- Version control. Although super useful it is outside of this workshop.
- Python outside a Jupyter Notebook (e.g. on terminal, or VScode, or spyder) 
- Python sets and tuples are only mentioned.
- File input/output is only used via libraries and doing "own" file-I/O is only part
  of optional material.
- How to choose the right visualization format for the data at hand.
- Python object oriented design.
- Python packaging.
- NumPy arrays.
- Managing environments and installing Python packages.

(episode-overview)=

## Episode overview

Introductory workshop (3h):
- {doc}`intro_to_programming`
- {doc}`jupyter`
  [![nbviewer badge](https://img.shields.io/badge/view%20on-nbviewer-brightgreen.svg)](https://nbviewer.org/github/coderefinery/data-visualization-python/blob/main/notebooks/first-notebook.ipynb)
  [![colab badge](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/coderefinery/data-visualization-python/blob/main/notebooks/first-notebook.ipynb)
  [![binder badge](https://mybinder.org/badge_logo.svg)](https://mybinder.org/v2/gh/coderefinery/data-visualization-python/HEAD?labpath=notebooks%2Ffirst-notebook.ipynb)
- {doc}`python-basics`
- {doc}`plotting`
  [![nbviewer badge](https://img.shields.io/badge/view%20on-nbviewer-brightgreen.svg)](https://nbviewer.org/github/coderefinery/data-visualization-python/blob/main/notebooks/plotting.ipynb)
  [![colab badge](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/coderefinery/data-visualization-python/blob/main/notebooks/plotting.ipynb)
  [![binder badge](https://mybinder.org/badge_logo.svg)](https://mybinder.org/v2/gh/coderefinery/data-visualization-python/HEAD?labpath=notebooks%2Fplotting.ipynb)
- {doc}`plotting_R`

More advanced topics:
- More {doc}`plotting`
- {doc}`tidy-data`
- {doc}`customizing-plots`
  [![nbviewer badge](https://img.shields.io/badge/view%20on-nbviewer-brightgreen.svg)](https://nbviewer.org/github/coderefinery/data-visualization-python/blob/main/notebooks/customizing.ipynb)
  [![colab badge](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/coderefinery/data-visualization-python/blob/main/notebooks/customizing.ipynb)
  [![binder badge](https://mybinder.org/badge_logo.svg)](https://mybinder.org/v2/gh/coderefinery/data-visualization-python/HEAD?labpath=notebooks%2Fcustomizing.ipynb)
- {doc}`gallery`
- {doc}`sharing`

Other:
- {doc}`installation`


```{toctree}
:maxdepth: 1
:caption: Episodes
:hidden:

intro_to_programming.md
jupyter.md
python-basics.md
r-basics.md
data.md
plotting.md
```

```{toctree}
:maxdepth: 1
:caption: Reference

installation.md
colab.md
```

```{toctree}
:maxdepth: 1
:caption: Other materials

tidy-data.md
customizing-plots.md
gallery.md
sharing.md
parsing-custom-format.md
```


## Credit

When preparing this lesson, we have reused these resources:

- <https://aaltoscicomp.github.io/python-for-scicomp/>
- <https://datacarpentry.org/python-ecology-lesson/>
- <https://swcarpentry.github.io/python-novice-inflammation/>
- <https://coderefinery.github.io/jupyter/>
- <https://coderefinery.github.io/data-visualization-python/>
