FROM node:latest

WORKDIR /app/admin

# Install build dependencies for native modules
RUN apt-get update && apt-get install -y \
    python3 \
    make \
    g++ \
    && rm -rf /var/lib/apt/lists/*

# Copy package files first for better caching
COPY package.json package-lock.json* ./

# Install dependencies
RUN npm install --legacy-peer-deps

# Copy rest of application
COPY . .

# Expose port
EXPOSE 7000

# Start development server
CMD ["npm", "run", "develop"]