FROM node:latest


WORKDIR /app/storefront

# Install build dependencies
RUN apt-get update && apt-get install -y \
    python3 \
    make \
    g++ \
    && rm -rf /var/lib/apt/lists/*

# Copy package files first
COPY package.json package-lock.json* ./

# Install dependencies
RUN npm install --legacy-peer-deps

# Copy rest of application
COPY . .

# Expose port
EXPOSE 8000

# Start development server (use npm script instead of gatsby directly)
CMD ["npm", "run", "dev"]