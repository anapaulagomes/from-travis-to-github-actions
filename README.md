# Moving from Travis to Github Actions

An attempt to create an "from/to" document and help people move from Travis to Github Actions.

Table Content

* [Travis to Github Actions Cookbook](#travis-to-github-actions-cookbook)
* [Interesting stuff](#interesting-stuff)
* [Contributing](#contributing)

# Travis to Github Actions Cookbook

## Installing dependencies

Travis

```
install:
- pip install --upgrade pip pipenv
- pipenv sync --dev
```

Github Actions

```
jobs:
    build:
    steps:
    - name: Install dependencies
      run: |
        pip install --upgrade pip pipenv
        pipenv sync --dev
```

## Specifying language and version

Travis

```
language: python
python:
- '3.6.8'
```

Github Actions

```
jobs:
    build:
    steps:
    - name: Set up Python 3.6.9
      uses: actions/setup-python@v1
      with:
        python-version: 3.6.9
```

## Running specific branches

Travis

```
branches:
  only:
  - master
```

Github Actions

```
on:
  pull_request:
    branches:
    - master
```

## Dist

Travis

```
dist: xenial
```

Github Actions

```
jobs:
    build:
        runs-on: ubuntu-latest
```

It's possible to test your library across a matrix of operating systems and
runtime versions using [matrix strategy on Github Actions](https://help.github.com/en/articles/workflow-syntax-for-github-actions#jobsjob_idstrategy).

## Global environment variables

Not supported by GitHub Actions yet (see the discussion [here](https://github.community/t5/GitHub-Actions/Support-global-environment-variables/td-p/30481)).

A [hack](https://github.com/DaanDeMeyer/reproc/blob/master/.github/workflows/vsenv.bat) to make them global.

## Services

Travis

```
services:
- redis-server
```

Github Actions

```
jobs:
    services:
        redis:
            image: redis
            ports:
            - 6379:6379
```

# Interesting stuff

* [Github Actions vs Travis CI](https://knapsackpro.com/ci_comparisons/github-actions/vs/travis-ci)
* [Starter Workflows](https://github.com/actions/starter-workflows)
* [Service examples](https://github.com/actions/example-services)
* [Run your GitHub Actions locally](https://github.com/nektos/act)
* [Awesome Actions](https://github.com/sdras/awesome-actions)

# Contributing

Open your Pull Request using the following format:

```

## Title

Travis

```
```

Github Actions

```
```

```
