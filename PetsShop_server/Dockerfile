# ----- Build Stage -----
FROM node:20-alpine AS builder

# Set working directory
WORKDIR /app

# Copy source code
COPY . .

# Copy production env variables via --build-arg
ARG NODE_ENV=production
ENV NODE_ENV=$NODE_ENV

# Install production dependencies only
RUN yarn install --production

# Port exposed by the app 
EXPOSE 8080

# Default command 
ENTRYPOINT yarn start
