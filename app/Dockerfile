FROM node:18-apine
WORKDIR /app

COPY package.json package.lock.json* ./

RUN npm install

EXPOSE 3000

CMD [ "npm", "start" ]
