FROM node:18-alpine

WORKDIR /app

COPY package*.json .

RUN npm install

COPY . .

RUN sed -i "s/'127.0.0.1'/'0.0.0.0'/g" src/server.js || true
RUN sed -i "s/'localhost'/'0.0.0.0'/g" src/server.js || true


CMD ["npm", "run", "dev"]