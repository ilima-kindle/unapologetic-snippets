---
layout: default
title: Notebook
nav_order: 4
parent: Python
grand_parent: Programming Languages
has_children: true
permalink: /docs/languages/python/notebbok
---

# Notebook

- [What is a data science Notebook?]({% link docs/algorithms-data-structures/index.md %}#data-science-notebook)
  - [My Notebooks]({% link docs/algorithms-data-structures/notebooks/index.md %})

```sh
# to install
pip3 install jupyter

# to run
# by default, run on: http://localhost:8888
jupyter notebook
```

__virtual env__

```sh
python3 -m venv my-jupyter-env       # to create a virtualenv
source my-juptyer-env/bin/activate   # to activate the virtualenv
deactivate                           # to leave the virtualenv
```

__Jupyter in the terminal__

```sh
# Jupyter in the terminal.
# https://github.com/davidbrochart/jpterm
# Key bindings
# https://github.com/davidbrochart/jpterm/blob/10d9e93105ab80053314944e805689a5c9a01449/docs/plugins/notebook_editor.md

# enter: enter the edit mode, allowing to type into the cell.
# esc: exit the edit mode and enter the command mode.

# to install
pip3 install jpterm

# to install a Python kernel
pip3 install ipykernel

# REFERENCE
# The Predecessor:
# Jupyter Notebooks in the terminal.
#  - https://github.com/davidbrochart/nbterm
#  - https://blog.jupyter.org/nbterm-jupyter-notebooks-in-the-terminal-6a2b55d08b70
#  - `pip3 install nbterm`
#   enter: enter the edit mode, allowing to type into the cell.
#   esc: exit the edit mode and enter the command mode.
#   ctrl-h: show help.
```

<details markdown="block">
  <summary>
    <i>sample notebook</i>
  </summary>

```json
{
  "cells": [
    {
      "source": "This is a raw cell",
      "cell_type": "raw",
      "metadata": {}
    },
    {
      "cell_type": "markdown",
      "metadata": {},
      "source": "This is a markdown cell"
    },
    {
      "execution_count": 1,
      "cell_type": "code",
      "source": "a = 3\nprint(a+1)\n",
      "outputs": [],
      "metadata": {}
    }
  ],
  "metadata": {
    "kernelspec": {
      "language": "python",
      "name": "python3",
      "display_name": "Python 3"
    },
    "language_info": {
      "version": "3.9.2",
      "mimetype": "text/x-python",
      "name": "python",
      "file_extension": ".py"
    }
  },
  "nbformat": 4,
  "nbformat_minor": 4
}
```

-----
<!-- sample notebook -->
</details>

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

## CentOS

- [see jupyter docker in CentOS]({% link docs/languages/containerization/docker.sample.md %}#jupyter-notebook)

```sh
pip3 install --upgrade --force-reinstall jupyter
pip3 install --upgrade --force-reinstall notebook
jupyter notebook --allow-root

# 155.248.192.51:8088/tree?token=xxxxx
# learn.ilima.xyz:8088/tree?token=xxxxx
jupyter notebook --allow-root --ip=0.0.0.0 --port=8888 --NotebookApp.token='xxxxxx'
```

<details markdown="block"><summary><i>other kernels</i></summary>

  <details markdown="block"><summary><i>golang</i></summary>

  ```sh
  apt update
  apt install golang-go
  
  go install github.com/janpfeifer/gonb@latest
  go install golang.org/x/tools/cmd/goimports@latest
  go install golang.org/x/tools/gopls@latest
  
  echo -e "\nexport GOPATH=/root/go" >> ~/.bashrc
  echo -e "\nexport PATH=\"$GOPATH/bin:$PATH\"" >> ~/.bashrc

  export GOPATH="/root/go"
  export PATH="$GOPATH/bin:$PATH"
  
  ~/go/bin/gonb --install
  ```
  
  ```jupyter
  // reference documentation
  %help
  ```
  
  ```jupyter
  import "fmt"
  %%
  fmt.Println("Hello, Gianni!")
  ```
  -----
  <!-- kernel golang -->
  </details>


  <details markdown="block"><summary><i>bash</i></summary>

  ```sh
  pip3 install bash_kernel
  python3 -m bash_kernel.install
  ```
  
  ```jupyter
  cat dog.png | display
  echo "<b>Dog</b>, not a cat." | displayHTML
  echo "alert('It is known khaleesi\!');" | displayJS
  ```
  
  -----
  <!-- kernel bash -->
  </details>


  <details markdown="block"><summary><i>nodejs</i></summary>

  ```sh
  # Instal NodeJS
  apt update
  apt install nodejs
  apt install npm
  # NVM
  curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.3/install.sh | bash
  source ~/.bashrc
  ```
  
  ```sh
  # Install a javascript kernel for the Jupyter notebook
  npm install -g ijavascript
  ijsinstall
  ```
  
  -----
  <!-- kernel nodejs -->
  </details>


  <details markdown="block"><summary><i>deno</i></summary>

  Deno brings __TypeScript__, __JavaScript__, __npm__, and __ES Modules__ to Jupyter with an easy to install kernel.
  - [https://docs.deno.com](https://docs.deno.com/)
  
  ```sh
  # Install
  # https://docs.deno.com/runtime/manual/getting_started/installation
  curl -fsSL https://deno.land/install.sh | sh
  
  # deno jupyter kernel installation:
  deno jupyter --unstable --install
  ```
  
  ```sh
  # Deno was installed successfully to /root/.deno/bin/deno
  # Manually add the directory to your $HOME/.bashrc (or similar)
    export DENO_INSTALL="/root/.deno"
    export PATH="$DENO_INSTALL/bin:$PATH"
  # Run '/root/.deno/bin/deno --help' to get started
  ```
  
  TypeScript kernel alternatives:
  - [https://github.com/winnekes/itypescript](https://github.com/winnekes/itypescript)
  - [https://github.com/yunabe/tslab](https://github.com/yunabe/tslab)
    
  -----
  <!-- kernel deno -->
  </details>


-----
<!-- other kernels -->
</details>


------ ------

[^1]: [...](...)
