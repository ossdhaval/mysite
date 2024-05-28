# MKDocs notes

Used [material for Mkdocs](https://squidfunk.github.io/mkdocs-material/) for documentation. It is a robust theme on top of mkdocs. When you install `material for Mkdocs` it also install Mkdocs. 

## install on Ubuntu

```
pip install mkdocs-material=="8.3.0"
```

after installation, if you want to locally see your changes being effective, run `mkdocs serve` from the directory where you have stored mkdocs.yml

### installing plugins

you can search plugins on pypi and then install using pip command given there. For example: `https://pypi.org/project/mkdocs-git-committers-plugin-2/`

```
pip install mkdocs-git-revision-date-localized-plugin
pip install mkdocs-git-committers-plugin-2
```

### Icons sets available in mkdocs by default

https://squidfunk.github.io/mkdocs-material/reference/icons-emojis/#configuration


## reference
- https://squidfunk.github.io/mkdocs-material/reference/
- url for local deployment: http://127.0.0.1:8000/

## troubleshooting

### index.md getting mapped to the category header

See this [PR](https://github.com/JanssenProject/jans/pull/8147) Here since there was only one index.md under the `plugins` directory, it was getting mapped to the category and ignoring the mapping given in the mkdocs.yml. This got fixed when file name was changed to something apart from `index.md`.
