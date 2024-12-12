FROM node:20-alpine

WORKDIR /app/worker

COPY package.json .
RUN npm install

COPY . .

CMD ["npm", "start"]

# will still need to pass in env vars