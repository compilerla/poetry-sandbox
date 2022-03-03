# Poetry

## What is it?
`poetry` is a tool for Python that
 - handles dependency installation
 - handles building and publishing Python packages
 - uses the standardized `pyproject.toml`

From its README:
> ... `poetry` uses `pyproject.toml` to replace `setup.py`, `requirements.txt`, `setup.cfg`, `MANIFEST.in` and the newly added `Pipfile`.

`pyproject.toml` is not an invention of `poetry` -- it comes from PEP 518: https://www.python.org/dev/peps/pep-0518/#rationale

## How do you use it?

### Installing

#### General recommendation

The general recommendation is to `curl` the install script and pipe it to Python:
```
curl -sSL https://install.python-poetry.org | python3 -
```
This ensures an isolated, platform-specific install.

#### In containers

You can also install it using `pip`, which when installing in a Docker container and locking the version, should be stable enough.

```
pip install poetry==1.1.13
```

You can quickly confirm a successful installation by running `poetry --version`.

### Creating a new Python project with Poetry

Create the project and initialize files with:

```
poetry new <project-name>
```

Example: 
 - Open a terminal in this VS Code devcontainer. The current working directory should be `/workspaces/poetry-sandbox`. 
 - Run `poetry new compiler-poetry`.

Result:
A new folder named `compiler-poetry` is created with some initial, generated configuration.
```
compiler-poetry/
├── README.rst
├── compiler_poetry
│   └── __init__.py
├── pyproject.toml
└── tests
    ├── __init__.py
    └── test_compiler_poetry.py
```

To start working in the project, you'll need to change into that directory 
```
cd compiler-poetry
```


**Add dependencies** by running
```
poetry add <package-name>
```

Example: `poetry add requests`

Notice this modified our `pyproject.toml` file.

Running `poetry install` will resolve dependencies and create/update a `poetry.lock` file. This file specifies the exact versions for dependencies and their transitive dependencies. Poetry projects should have this file checked-in to version control.


**Virtual environments**

By default, `poetry` will create a virtual environment where it will install your dependencies and where you will run your code.

For example, to run tests, you'd run `poetry run python -m pytest`. (Make sure you've installed dependencies first.)

You can turn this off by running:

```
poetry config virtualenvs.create false
```

Run `poetry env list` to see the list of virtual environments that Poetry has created.


### Adding Poetry to an existing project

```
poetry init
```
will run you through a series of interactive prompts to set up your `pyproject.toml` file.

If you want it to read in your existing `requirements.txt` file, you can do via:
```
poetry add `cat requirements.txt`
```

### Building and publishing Python packages

`poetry` provides a simple interface for building and publishing Python packages. The commands are `build` and `publish`, respectively, and configuration is specified in `pyproject.toml`.

## Helpful reading material
 - For `poetry` specifically:
    - A thorough overview, including explanation of `pyproject.toml`: _Dependency Management With Python Poetry_, https://realpython.com/dependency-management-python-poetry/
    - Poetry README: https://github.com/python-poetry/poetry#introduction
    - Overview of poetry, including usage in containers: https://nanthony007.medium.com/stop-using-pip-use-poetry-instead-db7164f4fc72
    - Publishing Python Packages with Poetry: https://realpython.com/pypi-publish-python-package/#poetry
    - The official docs: https://python-poetry.org/
       - https://python-poetry.org/docs/basic-usage/
 - For broader context:
    - Helpful article for understanding the history and comparison of all these tools that have a lot of overlap: _Python's New Package Landscape_, http://andrewsforge.com/article/python-new-package-landscape/
    - From Python Packaging Authority:
       - Recommended tooling: https://packaging.python.org/en/latest/guides/tool-recommendations/
       - Key Project summaries: https://packaging.python.org/en/latest/key_projects/

## Open questions
 - Does dependabot know how to look for updates for `pyproject.toml`?