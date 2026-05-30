FROM node:18

WORKDIR user/src/app

COPY package*.json ./

RUN npm install

COPY . . 

CMD ["npm", "start"]
