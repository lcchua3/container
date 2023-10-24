FROM python:latest

### INSTALL
# create /app and cd into /app
WORKDIR /app

# inside /app.. Can also use ADD instead of COPY 
# file can just put a . # dir use directory name
# in case don't have curl
RUN apt update && apt install -y curl 

COPY main.py .
COPY requirements.txt .
COPY run.sh .
COPY utils.py .
COPY public public
COPY templates templates

# install dependencies
RUN pip install -r requirements.txt

## RUN
HEALTHCHECK --interval= --timeout=30s --retries=3 \
    CMD curl -s http://localhost:${port}/healthz || exit 1

# set environment variable
ENV PORT=5000
ENV INSTANCE_NAME=dov-bear
ENV INSTANCE_HASH='abc'

EXPOSE ${APP_PORT}

ENTRYPOINT python main.py 