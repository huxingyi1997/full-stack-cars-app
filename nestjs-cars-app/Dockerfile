FROM node:16 AS production

ARG NODE_ENV=production
ENV NODE_ENV=${NODE_ENV}

WORKDIR /usr/src/api

COPY package.json .
COPY yarn.lock .

RUN yarn global add @nestjs/cli
RUN yarn install

RUN apt-get -q update && apt-get -qy install netcat

COPY . .

RUN yarn build 

CMD ["sh", "-c", "yarn typeorm migration:run -d ./src/database/ormconfig.ts && yarn start:prod"]
