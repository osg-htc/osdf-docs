# OSDF User Documentation

The source files for the OSDF User Documentation website.

## Local preview

### Using Docker
To serve the website locally, download Docker and use the command in the root directory:


```console
docker run --rm -it -p 8000:8000 -v ${PWD}:/docs squidfunk/mkdocs-material
```

ARM
```shell
docker run --rm -it -p 8100:8000 -v  ${PWD}:/docs ghcr.io/afritzler/mkdocs-material
```

### Using Python

Requires that the `mkdocs-material` Python package is installed.

```
conda create -n mkdocs
conda activate mkdocs
python3 -m pip install mkdocs-material
```

To launch the local preview, run

```
mkdocs serve
```

in the top level of the repository.
Then navigate to [http://127.0.0.1:8000](http://127.0.0.1:8000) in your browser.

## Adding Documentation to the Website

### Adding in the Documentation

Documentation is hosted in the ```/docs``` directory. 

Documentation should be referenced in two locations:

#### /docs/index.md

This is an overview page.
        
#### [/mkdocs.yml](https://github.com/osg-htc/user-school-2025/blob/main/mkdocs.yml)

This files generates the website navigation.

If you are adding materials it will look like so:
```yaml
nav:
  - Home: index.md
  - Getting started: gettingstarted.md
```

