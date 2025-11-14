FROM node:18-alpine

WORKDIR /app/medusa

# Enable corepack
RUN corepack enable

# Copy package files
COPY package.json yarn.lock* package-lock.json* ./

# Install dependencies
RUN npm install --legacy-peer-deps

# Copy source files
COPY . .

# Expose Medusa port
EXPOSE 9000

# Run migrations and start in development mode
CMD ["sh", "-c", "npx medusa migrations run && npm run dev"]