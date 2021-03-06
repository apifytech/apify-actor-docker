# Use the specified Python version, fallback to 3.7 as default

ARG PYTHON_VERSION=3.7
FROM python:${PYTHON_VERSION}-alpine

LABEL maintainer="support@apify.com" Description="Base image for simple Apify actors written in Python"

# Don't store bytecode, the Python app will be only run once
ENV PYTHONDONTWRITEBYTECODE 1

# Don't buffer output and flush it straight away
ENV PYTHONUNBUFFERED 1

# Create a virtual environment
ENV VIRTUAL_ENV=/opt/venv
RUN python3 -m venv $VIRTUAL_ENV
ENV PATH="$VIRTUAL_ENV/bin:$PATH"

# Upgrade pip before installing anything else first
RUN pip install --upgrade pip

# Install the specified Python Client version
ARG APIFY_CLIENT_VERSION
RUN pip install apify_client~=${APIFY_CLIENT_VERSION}

# Create app directory
RUN mkdir -p /usr/src/app
WORKDIR /usr/src/app

# Copy the dummy source code to the image
COPY main.py ./

# Set default startup command, using CMD instead of ENTRYPOINT, to allow manual overriding
CMD python3 main.py
