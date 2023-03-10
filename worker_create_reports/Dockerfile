FROM python:3.10.8-slim-bullseye
COPY . /python_worker
WORKDIR /python_worker
RUN apt-get update \
    && apt-get -y install libpq-dev gcc \
    && apt-get install -y locales \
    && sed -i -e 's/# ru_RU.UTF-8 UTF-8/ru_RU.UTF-8 UTF-8/' /etc/locale.gen \
    && dpkg-reconfigure --frontend=noninteractive locales

ENV PYTHONDONTWRITEBYTECODE 1
ENV PYTHONUNBUFFERED 1
ENV LANG ru_RU.UTF-8
ENV LC_ALL ru_RU.UTF-8

RUN pip install --upgrade pip \
    && pip install psycopg2 \
    && pip install -r requirements.txt
CMD [ "celery", "-A", "create_report_task", "worker", "-l", "INFO"]