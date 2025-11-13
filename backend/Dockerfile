FROM node:latest

WORKDIR /app/medusa

COPY ./medusa/package.json .

RUN apt-get update


RUN apt-get install -y python3

RUN npm install -g npm@latest

RUN npm install -g @medusajs/medusa-cli@latest
RUN npm install -g yarn

RUN yarn install --loglevel=error

COPY ./medusa .

ENTRYPOINT ["./develop.sh", "develop"]
