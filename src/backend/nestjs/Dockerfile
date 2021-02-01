FROM node:12.13-alpine As development

WORKDIR /app

RUN apk add --no-cache bash git && yarn add global rimraf

COPY package*.json ./

RUN yarn install

COPY . .

RUN npm run build

#========================================

FROM node:12.13-alpine as production

ARG NODE_ENV=production
ENV NODE_ENV=${NODE_ENV}

WORKDIR /app

COPY package*.json ./

RUN yarn install --production

COPY . .

COPY --from=development /app/dist ./dist

CMD ["yarn", "run", "start:prod"]