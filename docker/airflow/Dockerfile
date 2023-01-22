FROM apache/airflow:slim-2.5.1-python3.10

USER root
RUN apt-get update \
    # Install git that is needed for dbt.
    && apt-get install -y --no-install-recommends \
    git \
    && apt-get autoremove -yqq --purge \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

# Create directories for dbt artifacts.
RUN mkdir -p \
    ${AIRFLOW_HOME}/dbt/target \
    ${AIRFLOW_HOME}/dbt/dbt_packages \
    ${AIRFLOW_HOME}/dbt/logs \
    ${AIRFLOW_HOME}/dbt/models \
    ${AIRFLOW_HOME}/dbt/analyses \
    ${AIRFLOW_HOME}/dbt/tests \
    ${AIRFLOW_HOME}/dbt/seeds \
    ${AIRFLOW_HOME}/dbt/macros \
    ${AIRFLOW_HOME}/dbt/snapshots

# Allow the airflow user to write into the dbt directories
RUN chown airflow -R ${AIRFLOW_HOME}/dbt

# Copy dbt configs into the container.
COPY ./dbt/dbt_project.yml ${AIRFLOW_HOME}/dbt/dbt_project.yml
COPY ./dbt/profiles.yml ${AIRFLOW_HOME}/dbt/profiles.yml

USER airflow
# Install dbt-trino adapter.
RUN pip install --upgrade pip \
    && pip install --no-cache-dir --user dbt-trino==1.3.2
