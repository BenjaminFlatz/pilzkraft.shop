FROM node:latest

WORKDIR /app/medusa

COPY . .

RUN rm -rf node_modules

RUN apt-get update

RUN npm install -g npm@latest

RUN npm install --loglevel=error

# Expose Medusa port
EXPOSE 9000

# Run migrations and start in development mode
CMD ["sh", "-c", "npx medusa db:migrate && npm run dev"]