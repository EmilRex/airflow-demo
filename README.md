# Airflow Demo

## Getting Started

Create a new virtual environment and install airflow plus our dependencies in it,

```sh
export AIRFLOW_VERSION=2.3.3
export PYTHON_VERSION="$(python --version | cut -d " " -f 2 | cut -d "." -f 1-2)"
export CONSTRAINT_URL="https://raw.githubusercontent.com/apache/airflow/constraints-${AIRFLOW_VERSION}/constraints-${PYTHON_VERSION}.txt"

pip install "apache-airflow==${AIRFLOW_VERSION}" --constraint "${CONSTRAINT_URL}"

pip install -r requirements.txt --constraint "${CONSTRAINT_URL}"
```

Now you can start airflow with,

```sh
export AIRFLOW_HOME="$(pwd)"
export AIRFLOW__CORE__LOAD_EXAMPLES=False
export AIRFLOW__CORE__LOAD_DEFAULT_CONNECTIONS=False

airflow standalone
```