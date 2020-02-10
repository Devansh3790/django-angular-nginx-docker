# base image
FROM node:12-alpine

# set working directory
WORKDIR /app

# add `/app/node_modules/.bin` to $PATH
ENV PATH /app/node_modules/.bin:$PATH

# install and cache app dependencies
COPY ./frontend/package.json \
    ./frontend/package-lock.json /app/

RUN npm install -g @angular/cli && npm ci

COPY ./frontend /app

# start app
COPY ./compose/frontend/start /start
RUN sed -i 's/\r//' /start
RUN chmod +x /start