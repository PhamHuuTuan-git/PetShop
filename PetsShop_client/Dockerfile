# ----- Build Stage -----
FROM node:20-alpine AS builder

# Set working directory
WORKDIR /app

ARG VITE_API_URL
ARG VITE_SOCKET_URL
ENV VITE_API_URL=$VITE_API_URL
ENV VITE_SOCKET_URL=$VITE_SOCKET_URL

RUN echo "VITE_API_URL=$VITE_API_URL" >> .env \
 && echo "VITE_SOCKET_URL=$VITE_SOCKET_URL" >> .env
 
# Copy source code
COPY . .

# Install dependencies
RUN yarn

# Build for production
RUN yarn build

# ----- Deploy with Nginx Stage -----

# Pull nginx to create web server
FROM nginx:stable-alpine
COPY --from=builder /app/dist /usr/share/nginx/html
COPY nginx.conf /etc/nginx/conf.d/default.conf

# Expose port (default Nginx HTTP port)
EXPOSE 80

# Start Nginx
CMD ["nginx", "-g", "daemon off;"]