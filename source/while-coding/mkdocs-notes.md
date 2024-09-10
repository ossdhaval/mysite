# MKDocs notes

Used [material for Mkdocs](https://squidfunk.github.io/mkdocs-material/) for documentation. It is a robust theme on top of mkdocs. When you install `material for Mkdocs` it also install Mkdocs. 

## install on Ubuntu

1. install mkdocs

  ```
  sudo apt install mkdocs
  ```

2. install mkdocs-material theme

This theme can't be installed with package manager i.e apt. Also, if you try using `pip install mkdocs-material=="8.3.0"` then you get an error `error: externally-managed-environment`. Solution is to create a python virtual environment and then install and use from within it.
-  setup a python virtual environment
    ```
    # create a directory to hold all your python virtual envs
    mkdir ~/python-venvs
    
    # create venv for mkdocs-material
    python3 -m venv ~/python-venvs/mkdocs-material-venv

    # activate venv
    source ~/python-venvs/mkdocs-material-venv/bin/activate

    # install mkdocs-material using pip
    pip install mkdocs-material=="8.3.0"

    # to use and deploy your docs using mkdocs and mkdocs-material
    # go to the directory where the mkdocs.yml is located from within the activated environment
    cd ~/vscode/gluu/GluuFederation/docs-gluu-server-prod/docs

    # start the mkdocs
    mkdocs serve    
    
    ```

### installing plugins

you can search plugins on pypi and then install using pip command given there. For example: `https://pypi.org/project/mkdocs-git-committers-plugin-2/`. You need to install plugins within the venv itself.

```
pip install mkdocs-git-revision-date-localized-plugin
pip install mkdocs-exclude-search
pip install mkdocs-include-markdown-plugin
```

### Icons sets available in mkdocs by default

https://squidfunk.github.io/mkdocs-material/reference/icons-emojis/#configuration


## reference
- https://squidfunk.github.io/mkdocs-material/reference/
- url for local deployment: http://127.0.0.1:8000/

## troubleshooting

### index.md getting mapped to the category header

See this [PR](https://github.com/JanssenProject/jans/pull/8147) Here since there was only one index.md under the `plugins` directory, it was getting mapped to the category and ignoring the mapping given in the mkdocs.yml. This got fixed when file name was changed to something apart from `index.md`.
