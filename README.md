#### Spark and PySpark Learning Repo

This repository hosts some of my learning path for  **Apache Spark** and **PySpark**.

##### Environment

This project uses the `jupyter/pyspark-notebook` container image. This allows for a fully functional Spark environment without requiring a complex local installation on the host machine.


##### Quick Start

To launch the Jupyter environment and mount this repository to the container, run the command below.

**Run this in your terminal:**

```bash
podman run --rm -it \
  --userns=keep-id \
  -p 8888:8888 \
  -v ~/Repositories/learning/data_eng_stuffs/learning_spark_pyspark:/home/jovyan/work:Z \
  docker.io/jupyter/pyspark-notebook:latest
```

What this does

  * **Starts Jupyter:** Maps port `8888` 
  * **Syncs Data:** Maps specific local repository (`~/Repositories/learning/...`) to the container's workspace. Any notebook saved in the browser is physically saved to local folder.
  * **Clean Exit:** The `--rm` flag ensures the container deletes itself when stopped, keeping the machine clean.
  * --userns=keep-id: Without this, Podman might map the container user to a high number (like 100999). With this, it maps the container user to actual ID (e.g., 1000), granting it the rights to write to the home folder.

If you are already inside the `learning_spark_pyspark` folder in your terminal, you can replace the long path with `$(pwd)` to save typing:

```bash
podman run --rm -it \
  -p 8888:8888 \
  -v "$(pwd)":/home/jovyan/work \
  docker.io/jupyter/pyspark-notebook:latest
```