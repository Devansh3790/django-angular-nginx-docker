FROM nginx:1.17.8-alpine


RUN apk add --update nodejs nodejs-npm \
    && npm install -g @angular/cli

WORKDIR /app

COPY ./frontend ./frontend

# Remove default nginx website
RUN rm -rf /usr/share/nginx/html/*
RUN rm -rf /etc/nginx/conf.d/*

RUN cd frontend \
    && npm ci \
    && ng build --prod --outputPath=../../usr/share/nginx/html/ \
    && cd ..
    
# start app
COPY ./compose/nginx/start /start
RUN sed -i 's/\r//' /start
RUN chmod +x /start