
FROM node:12-alpine as build
WORKDIR /appclient
COPY client /appclient

FROM nginx:1.15.8-alpine
COPY --from=build /appclient/build /usr/share/nginx/html
COPY docker/nginx/app.conf /etc/nginx/conf.d/default.conf
RUN mkdir /etc/nginx/html
RUN mkdir /etc/nginx/html/upload
EXPOSE 80