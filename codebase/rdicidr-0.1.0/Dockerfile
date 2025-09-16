# Build stage
FROM node:15-alpine AS builder

WORKDIR /app

# Copy package files and install all dependencies
COPY package*.json ./
RUN npm install --ignore-engines

# Copy the rest of the application source
COPY . .

# Build the React application
RUN npm run build

# Production stage
FROM nginx:alpine

# Copy the built application from the builder stage
COPY --from=builder /app/build /usr/share/nginx/html

# Copy the custom nginx configuration
COPY nginx.conf /etc/nginx/nginx.conf

# Expose port 80
EXPOSE 80

# Start Nginx
ENTRYPOINT ["nginx", "-g", "daemon off;"]
