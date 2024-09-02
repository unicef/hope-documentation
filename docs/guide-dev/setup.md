---
title: Setup
---

## Prerequisites

This project uses PDM as package manager (see https://github.com/pdm-project/pdm),
and relies on the following components:

- A Postgres DB v15+
- A Redis server
- An ElasticSearch server


## Get started

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
   1. `./manage.py upgrade`
1. Test using runserver $`./manage.py runserver` and logging in the admin `http://locslhost:8000/admin`
