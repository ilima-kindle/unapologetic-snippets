---
layout: default
title: Notebooks
nav_order: 1
parent: Algorithms and Data Structures
has_children: false
has_toc: true
permalink: /docs/algorithms-and-data-structures/notebooks
---

# My Notebooks

- [Python]({% link docs/languages/python/index.md %})
  - [ipynb]({% link docs/algorithms-data-structures/notebooks/files/python-workspace.ipynb %})
  - [html]({% link docs/algorithms-data-structures/notebooks/html/python-workspace.html %})
  - nbviewer
- [Golang]({% link docs/languages/golang/index.md %})
  - ipynb
  - html
  - nbviewer
- [NodeJS]({% link docs/languages/node-js/index.md %})
  - ipynb
  - html
  - nbviewer
- [Bash]({% link docs/languages/shell/index.md %})
  - ipynb
  - html
  - nbviewer

## Notebook Viewer

- a simple way to share Jupyter Notebooks:
  - [nbviewer](https://nbviewer.org/)
- convert notebooks to other formats
  - ```sh
    # nbconvert
    # convert notebooks to other formats
    # https://nbconvert.readthedocs.io/en/latest/
    jupyter nbconvert --to html mynotebook.ipynb
    jupyter nbconvert --to markdown mynotebook.ipynb
    jupyter nbconvert --to pdf mynotebook.ipynb
    ```
  - ```sh
    python3 -m venv my-env-jupyter
    source my-env-jupyter/bin/activate
    deactivate          # how to leave/exit/deactivate
    source deactivate   # if this doesn't work, try

    pip3 install --upgrade --force-reinstall jupyter
    pip3 install --upgrade --force-reinstall notebook
    pip3 install --upgrade --force-reinstall ipython_genutils
    # the ‘Templates’ folder is not included in version 6.0.0
    pip3 install --upgrade --force-reinstall nbconvert==5.6.1

    cd docs/algorithms-data-structures/notebooks/files
    jupyter nbconvert --to html *.ipynb
    mv *.html ../html/
    ```

------ ------

[^1]: [...](...)