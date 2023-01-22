FROM apache/airflow:slim-2.5.1-python3.10

USER root
RUN apt-get update \
    # Install git that is needed for dbt.
    && apt-get install -y --no-install-recommends \
    git \
    && apt-get autoremove -yqq --purge \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

USER airflow
