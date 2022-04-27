FROM node:12-alpine

LABEL author="Luis Valgoi"

ENV NODE_ENV=production
ENV PORT=8080

COPY . /var/www
WORKDIR /var/www

VOLUME ["/var/www"]

RUN rm -rf node_modules

RUN npm install

EXPOSE $PORT

ENTRYPOINT [ "npm", "start" ]