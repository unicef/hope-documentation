---
title: Development Guide
---
#  Development Guide

## Setup development environment


### Prerequisites

- This project uses PDM as package manager (see https://github.com/pdm-project/pdm).
- A Postgres DB v15+
- A Redis server
- An Elastic Search server


## Technology Stack

- Python
- Postgres
- Redis
- ElasticSearch


## To start developing:

### Pull Requests

Every pull requests should contain tests to coverage the functionality.

- Coverage of 95% on written lines is required in order to merge.
- Two reviews are needed before merging PRs


### Get started

1. Install [pdm](https://github.com/pdm-project/pdm#installation) amd create virtualenv
1. Crate virtual env
   1. `pdm venv create`
1. Register the created venv for the project with 
   1. `pdm use` 
1. Activate your venv 
   1. `pdm venv activate`
1. Check your environment
   1. eg. $`python --version` -> see that it uses Python 3.12.*
   1. eg. $`which python` -> see that it matches you python executable in the venv you have created: $```echo `pwd`/.venv/bin/python```
1. Install the package
   1. `pdm install`
1. Setup PYTHONPATH
   1. `export PYTHONPATH="$PYTHONPATH:./src"`
1. Check and configure your environment: 
   1. `./manage.py env --check` and configure the missing variables.
      You can generate a list for your development environment with the command `./manage.py env --develop --config --pattern='export {key}={value}'`
1. Once the environment has been set up run the initial migrations
   1. `./manage.py migrate`
1. Make sure to set up environment variables:
1. Test using runserver $`./manage.py runserver` and logging in the admin `http://locslhost:8000/admin`


### Code quality

To enhance readability of code and increase code standars we use the following  
- pep8 - https://peps.python.org/pep-0008/
- flake8 - https://flake8.pycqa.org/en/latest/
- isort - https://pycqa.github.io/isort/
- black - https://black.readthedocs.io/en/stable/
- mypy - https://mypy-lang.org/
