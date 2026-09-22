# Docker build context

!!! important
    Using this syntax: `docker build ./folder .` Docker client packs this folder and sends it to the docker daemon.

    1. If `Dockerfile` needs files which are above this folder, it will throw an error.
    2. If you want to optimize your project you should try to use as few resources as possible.
    3. You can pass separately the path to `Dockerfile` and the context folder, e.g.:
    ```bash
    docker build -f ./path/Dockerfile ./nested/folder
    ```
