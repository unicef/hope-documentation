# Run Test Suite


## Run "Unit" tests 

    docker compose run --rm backend \
            pytest \
            -n auto \
            -rP \
            --create-db \
            -p no:warnings \
            --cov-report= \
            --capture=sys \
            hct_mis_api/ tests/


#### Analyze HTML Report
    
    ...

## Run "Selenium" functional test

    ...

#### Analyze HTML Report

    ...

## Combine coverage and display reports

    ...
