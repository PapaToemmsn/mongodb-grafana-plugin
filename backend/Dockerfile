#build stage
# Use the official Node.js image as base
FROM node:20-alpine

# Set the working directory in the container
WORKDIR /usr/src/app

# Copy package.json and package-lock.json to the working directory
COPY package*.json ./

# Install dependencies
RUN npm install

# Copy the rest of the application code
COPY . .

# runtime stage
FROM alpine:3.20
RUN apk add --update nodejs
RUN addgroup -S node && adduser -S node -G node
USER node
RUN mkdir /home/node/code
WORKDIR /home/node/code
COPY --from=0 --chown=node:node /usr/src/app .
CMD ["node", "index.mjs"]

LABEL version="1.0"
LABEL description="Grafana datasource for mongodb. Based on the work here: https://github.com/taowenwei/mongodb-grafana-plugin"
LABEL org.opencontainers.image.authors="thomas.handler@clavisit.com"
