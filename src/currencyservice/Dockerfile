FROM nexuss.mahbod.com:8082/base/node:20.17.0-alpine AS builder

WORKDIR /usr/src/app

RUN apk add --update --no-cache python3 make g++

COPY package*.json ./

RUN npm install --only=production

COPY . .

FROM nexuss.mahbod.com:8082/base/node:20.17.0-alpine

WORKDIR /usr/src/app

COPY --from=builder /usr/src/app/node_modules ./node_modules
COPY . .

EXPOSE 7000

ENTRYPOINT ["node", "server.js"]