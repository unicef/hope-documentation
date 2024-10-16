# Setup


Prerequisites:

- This project uses [pdm](https://github.com/pdm-project/pdm#installation) as package manager
- A Postgres DB v14+
- A Redis server

!!! note

    PDM will create a virtualenv in <project_root>/.venv, and install dependencies into it.
    If you wand to change this behaviour please read the [PDM Documentation](https://pdm-project.org/en/latest/usage/venv/)


## Create virtualenvironment

1. Checkout code

    ```
    git clone https://github.com/unicef/hope-aurora
    git config branch.autosetuprebase always

    ```
   
2. In the shell:
    
    ```
    pdm venv create
    pdm use
    pdm venv activate
    ```
   
3. Check your virtualenv is properly created

    ```pdm info```


4. Install the package

    ```
     pdm install
     pdm run pre-commit install
    ```


5. Add `export PYTHONPATH="$PYTHONPATH:./src"`


6. Check your environment: 

    `./manage.py env --check` and configure the missing variables.

    !!! hint
    
        You can generate a list for your development environment with the command 
    
            ./manage.py env --develop --config --pattern='export {key}={value}'   

7. Run upgrade command to properly initialize the application: 

    `./manage.py upgrade --admin-email ${ADMIN_EMAIL} --admin-password ${ADMIN_PASSWORD}`
    
    !!! note
        
          Django migrations and collectstatic commands are automatically included in this step


## Configure environment for .direnv

If you want to use [direnv](https://direnv.net/) and automatic loading of environment variables from a _.envrc_ file:
    
```
./manage.py env --develop --config --pattern='{key}={value}' > .envrc

echo 'export PYTHONPATH="$PYTHONPATH:./src"' >> .envrc
echo 'eval $(pdm venv activate)' >> .envrc
echo "unset PS1" >> .envrc
```

!!! warning

    The first time after you have created or modified the _.envrc_ file you will have to authorize it using:

        direnv allow
