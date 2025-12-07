# Stage 1: Build stage
FROM node:18-alpine AS build
WORKDIR /app
COPY package*.json ./
RUN npm ci --omit=dev
COPY . .

# Stage 2: Run stage
FROM node:18-alpine

# Create non-root user
RUN addgroup -g 1001 -S nodejs && \
    adduser -S nodejs -u 1001 -G nodejs

WORKDIR /app

# Copy files with proper ownership
COPY --from=build --chown=nodejs:nodejs /app .
ADD --chown=nodejs:nodejs https://truststore.pki.rds.amazonaws.com/global/global-bundle.pem ./global-bundle.pem

# Switch to non-root user
USER nodejs

CMD ["node", "server.js"]
