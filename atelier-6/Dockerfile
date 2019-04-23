FROM python:3.7.3

ENV http_proxy $http_proxy
ENV https_proxy $http_proxy
ENV no_proxy $no_proxy

RUN pip install flask

RUN mkdir /src
VOLUME /src
WORKDIR /src

RUN groupadd -g 2200 appuser && \
    useradd -r -u 2200 -g appuser appuser

USER appuser

ENV FLASK_APP=server.py
ENV FLASK_DEBUG=1
CMD flask run --host=0.0.0.0
