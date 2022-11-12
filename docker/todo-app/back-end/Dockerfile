FROM node:14-alpine

EXPOSE 3001

WORKDIR /app

ADD ./node_modules.tar.gz .

COPY . .

CMD ["npm", "start"]