# docker_tutorial/frontend/Dockerfile

FROM node:14-alpine AS builder

COPY . ./
WORKDIR /frontend
RUN npm install

ENV PATH="./node_modules/.bin:$PATH"

RUN npm run build

FROM nginx:1.20.1-alpine
COPY /frontend/nginx.config /etc/nginx/nginx.template
RUN apk --no-cache add curl
RUN curl -L https://github.com/a8m/envsubst/releases/download/v1.1.0/envsubst-`uname -s`-`uname -m` -o envsubst && \
    chmod +x envsubst && \
    mv envsubst /usr/local/bin
CMD ["/bin/sh", "-c", "envsubst < /etc/nginx/nginx.template > /etc/nginx/conf.d/default.conf && nginx -g 'daemon off;'"]
COPY --from=builder /frontend/build /usr/share/nginx/html