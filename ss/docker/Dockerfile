FROM python:alpine

# Copy source code and set working directory
COPY . /app
WORKDIR /app

# Install dependencies
# ENV DEBIAN_FRONTEND=noninteractive

# RUN apt-get update && apt-get install --no-install-recommends -y \
#     package1 \
#     package2 \
#     && rm -rf /var/lib/apt/lists/* \
#     && apt-get clean
RUN apk update && \
    apk add postgresql-dev gcc && \
    apk del postgresql-dev gcc && \
    rm -rf /var/cache/apk/*
# RUN apt-get update -y \
#     && apt-get install -y libpq-dev gcc \
#     && pip install --upgrade pip \
#     && pip install psycopg2 \
#     && rm -rf /var/lib/apt/lists/*

# Install the requirements
COPY requirements.txt requirements.txt
RUN pip install -r requirements.txt

# Install the testing requirements
COPY requirements_test.txt requirements_test.txt
RUN pip install -r requirements_test.txt

# Start app
CMD ["gunicorn", "--log-config", "logging.conf", "application:app", "--preload"]
