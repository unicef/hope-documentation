HOPE Documentation
==================

This Repo is used to manage the official HOPE documentation

## Install

    $ uv sync
    $ uv build
    
#### Using .envrc

add in your .envrc

    export PKG_CONFIG_PATH="/usr/local/lib/pkgconfig:/opt/homebrew/lib/pkgconfig:$PKG_CONFIG_PATH"
    export DYLD_LIBRARY_PATH="/usr/local/lib:/opt/homebrew/lib:$DYLD_LIBRARY_PATH"
    source .venv/bin/activate


#### Start
    $ mkdocs build
    $ mkdocs serve
