# stage 0: build the node assets
FROM node:20-alpine

WORKDIR /app/client

COPY package.json .

COPY package-lock.json .

RUN npm install

COPY . .

RUN npm run build

# stage 1: set up nginx
FROM nginx:1.26.2

EXPOSE 3000

COPY --from=0 /app/client/build/ /usr/share/nginx/html/

RUN echo ' \n\
server { \n\
    listen 3000; \n\
    server_name localhost; \n\
    \n\
    location / { \n\
        root /usr/share/nginx/html; \n\
        index index.html index.htm; \n\
        try_files $uri $uri/ /index.html; \n\
    } \n\
}' >> /tmp/pro_conf

RUN cp /tmp/pro_conf /etc/nginx/conf.d/default.conf
