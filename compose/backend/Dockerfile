# Pull official base image
FROM python:3.8-alpine

ARG ENV=local

# Set environment variables
ENV PYTHONDONTWRITEBYTECODE 1
ENV PYTHONUNBUFFERED 1

# install psycopg2 dependencies
RUN apk update && apk add postgresql-dev gcc python3-dev musl-dev

# Upgrade pip 
RUN pip install --upgrade pip

# Requirements are installed here to ensure they will be cached.
COPY ./backend/requirements /requirements
RUN pip install -r /requirements/$ENV.txt

COPY ./compose/backend/entrypoint /entrypoint
RUN sed -i 's/\r//' /entrypoint
RUN chmod +x /entrypoint

COPY ./compose/backend/start /start
RUN sed -i 's/\r//' /start
RUN chmod +x /start

WORKDIR /app

ENTRYPOINT ["/entrypoint"]