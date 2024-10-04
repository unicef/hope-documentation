# Test Suite

The test suite is located within the tests directory and is organized into two subdirectories: unit and selenium. 
The unit directory contains unit tests, which focus on testing individual components of the project in isolation. 
The selenium directory contains tests that utilize Selenium for browser-based testing,
ensuring that the user interface and web interactions function as expected.

## Run "Unit" tests 
Unit tests are executed within a Docker container using the pytest framework.
This ensures a consistent testing environment, isolated from local machine configurations.

    docker compose run --rm backend pytest -n auto --reruns 3  -rP -p no:warnings --cov-report= --capture=sys  ./tests/unit


## Run "Selenium" functional test


Selenium tests run on the host machine. 
This is due to the fact that Selenium does not currently support the ARM64 architecture for Linux Docker images.
This will require some more steps to be taken before running the tests.
### Prerequisites
- pdm

### Installation
1. **Services**

   To run the tests locally, the following services are required:
   
   1. **Postgres**
   1. **Redis**
   1. **Elasticsearch**
   
   You can either install these services manually or use the `docker-compose` file located in the `development_tools` directory.

1. **Running Services with Docker Compose**
   
   Make sure you have the required `.env` file from the backend setup, then you can run the services using the following command:

   ```bash
   cd development_tools
   docker compose --profile services up
1. Install system requirements
   1. MACOS
      1. `brew install wkhtmltopdf pango postgis gdal`
1. Crate virtual env
   1. `pdm venv create`
1. Register the created venv for the project with 
   1. `pdm use` 
1. Activate your venv 
   1. `eval $(pdm venv activate)`
1. Check your environment
   1. eg. $`python --version` -> see that it uses Python 3.11.*
1. Install the packages
   1. `pdm sync --no-editable --no-self --no-isolation`
1. Run the tests
   1. `source ./development_tools/local_selenium_init.sh`
   1. `python -m pytest -svvv ./tests/selenium --html-report=./report/report.html`


