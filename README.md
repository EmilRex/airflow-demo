# Airflow Demo

This repo shows what a minimal pipeline looks like in airflow. There are three versions,

1. [original.py](./dags/original.py) shows the pipeline without any orchestration
2. [airflow_classic.py](./dags/airflow_classic.py) shows the pipeline as a classic airflow DAG
3. [airflow_taskflow.py](./dags/airflow_taskflow.py) shows the pipeline as a [TaskFlow](https://airflow.apache.org/docs/apache-airflow/stable/tutorial_taskflow_api.html) airflow DAG
4. [prefectified.py](./dags/prefectified.py) shows the pipeline as a Prefect 2 flow

## Getting Started

Create a new virtual environment and install the dependencies,

```sh
make install
```

Now you can start a local instance of airflow,

```sh
make start
```

Open up [http://0.0.0.0:8080](http://0.0.0.0:8080) in your browser to access the UI.

## Architecture

The component services of airflow can be understood by looking at the official [docker-compose.yaml](https://github.com/apache/airflow/blob/main/docs/apache-airflow/start/docker-compose.yaml). In a minimal setup you have,

* a **database** for metadata which is sqlite by default but typically postgres
* a **webserver** that serves the UI
* a **scheduler** that runs tasks using an **executor** which is typically `LocalExecutor` for local execution and `CeleryExecutor` for distributed execution

In a more scalable setup using Celery you would add,

* one or more **workers** that executes tasks
* a **redis** instance to broker between scheduler and workers
* optionally a **flower** UI for monitoring Celery

Airflow also has extensive support for Kubernetes, including an [official Helm chart](https://airflow.apache.org/docs/helm-chart/stable/index.html).

![](https://airflow.apache.org/docs/apache-airflow/stable/_images/arch-diag-basic.png)
