# Stage 1: Build stage
FROM node:18-alpine AS build

WORKDIR /app

COPY package*.json ./

RUN npm ci --omit=dev

COPY . .

# Stage 2: Run stage
FROM node:18-alpine

WORKDIR /app

COPY --from=build /app .

ADD https://truststore.pki.rds.amazonaws.com/global/global-bundle.pem ./global-bundle.pem

CMD ["node", "server.js"]