### Getting started
Avoid merge conflicts when using jupyter notebooks with `git`.

### Install [nbdev](https://nbdev.fast.ai)

[`nbdev`](https://nbdev.fast.ai) works on macOS, Linux, and most Unix-style operating systems. It works on Windows under WSL, but not under cmd or Powershell.

You can install `nbdev` with pip:
```
pip install -U nbdev
```
... or with conda:
```
conda install -c fastai nbdev
```
Note that nbdev must be installed into the same Python environment that you use for both Jupyter and your project.

To install the nbdev hooks, run `nbdev_install_hooks`. That's it, you're mostly set up. You can now run `nbdev_clean --fname demo_notebook.ipynb` to get rid of the metadata for a single notebook or `nbdev_clean --fname .` for all notebooks in your repo before commiting the changes. Check out `nbdev_clean --help` for more details.

Running this manually before every commit is tedious however, so let's automate this. There is two ways to do this:
If you're working with native jupyter-notebooks or jupyter-lab you can just do [this](https://nbdev.fast.ai/tutorials/git_friendly_jupyter.html#quickstart-install-nbdev-hooks-for-a-repo). This is great, as it takes care of most jupyter related problems for you automatically, however I think this also introduces a bit too much overhead (mainly because it works off of remote repo). Alternatively (also if you want to work in an editor) you can run git hooks on your local repository.

### Install [pre-commit](https://pre-commit.com)
In order to use local git hooks you can use [`pre-commit`](https://pre-commit.com)

You can install `pre-commit` with pip:
```
pip install pre-commit
```
... or with conda:
```
conda install -c conda-forge pre-commit
```
Then (in your repository) create a file named `.pre-commit-config.yaml`with the following content:
```
repos:
-   repo: local
    hooks:
    - id: nbdev_clean # hook id 
      name: nbdev clean # some readable name
      entry: nbdev_clean --fname # the actual script that gets run on the files.
#      entry: nbdev_clean --clear_all --fname # the actual script that gets run on the files
      language: system # how to run the script
      types: [jupyter] # what to run it on
```

This file should be added to staging or `.gitignore` depending on if you want to work off of the same `pre-commit` config. 
In your repository run `pre-commit install` to set up the git hook scripts and your done! Now `pre-commit` will run `nbdev_clean` automatically on git commit!.
Depending on what hooks you'd like to run you can also add `nbdev_merge` or `nbdev_trust` to your config in a similar fashion.

More details can be found [here](https://pre-commit.com/#quick-start) and [here](https://nbdev.fast.ai/tutorials/pre_commit.html).