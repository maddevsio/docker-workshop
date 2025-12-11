FROM ubuntu:22.04

ENV LC_ALL=C.UTF-8
ENV LANG=C.UTF-8
ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update -y && \
    apt-get install -y software-properties-common && \
    add-apt-repository ppa:deadsnakes/ppa && \
    add-apt-repository ppa:ubuntu-toolchain-r/test && \
    apt-get update -y && \
    apt-get install -y python3.12 python3.12-dev pkg-config  \
        git gcc wget build-essential libgmp-dev python-is-python3  \
        default-libmysqlclient-dev curl libtbb-dev libwebp-dev && \
    apt-get install --only-upgrade -y libstdc++6 && \
    update-alternatives --install /usr/bin/python python /usr/bin/python3.12 1 && \
    update-alternatives --install /usr/bin/python3 python3 /usr/bin/python3.12 1 && \
    curl https://bootstrap.pypa.io/get-pip.py -o get-pip.py && \
    python3.12 get-pip.py

RUN pip install poetry==1.8.2
RUN poetry config virtualenvs.create false

WORKDIR /app

COPY ./pyproject.toml pyproject.toml
COPY ./poetry.lock poetry.lock
COPY ./Makefile Makefile
RUN poetry config virtualenvs.create false && poetry install --only main --no-root --no-cache

ADD . .

RUN ./manage.py collectstatic --no-input

EXPOSE 8001
