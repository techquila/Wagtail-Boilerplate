FROM python:3.6
MAINTAINER Techquila
LABEL version="v0.1.0"

ENV PYTHONUNBUFFERED=1 \
    DJANGO_SETTINGS_MODULE=core.settings.local \
    ALLOWED_HOSTS=* \
    INTERNAL_IPS=0.0.0.0 \
    SECRET_KEY=generatesecretkeyhere \
    MEDIA_PATH=/app/media \
    STATIC_PATH=/app/static \
    APP_LOG_DIR=/var/log/ \
    REQUIREMENTS=local.txt \
    DATABASE_USER=postgres \
    DATABASE_PASSWORD=postgres \
    DATABASE_NAME=postgres \
    DATABASE_HOST=db \
    REACT_HOST=http://ssr:3000

WORKDIR /app
ADD . /app/

RUN apt-get update \
    && apt-get install -y netcat \
    && apt-get install -y binutils libproj-dev gdal-bin \
    && rm -rf /var/lib/apt/lists/*

RUN apt-get update && apt-get -y install postgresql

RUN pip install -r requirements/$REQUIREMENTS --no-cache-dir \
    && pip install ipython \
    && pip install pyinotify

EXPOSE 8000

ENTRYPOINT ["./docker-entrypoint.sh"]
CMD ["runserver"]
