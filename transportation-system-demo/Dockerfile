# Stage 1: Build React app
FROM node:20-alpine AS build

# Set working directory
WORKDIR /app

# Copy package files
COPY package*.json ./

# Install dependencies
RUN npm ci

# Copy the rest of the source code
COPY . .

# Copy locales folder if it exists
COPY locales ./locales

# Build the app
RUN npm run build

# Stage 2: Serve with Nginx
# Use nginx as base
FROM nginx:alpine

# Copy the built React app
COPY dist /usr/share/nginx/html

# Expose port 80
EXPOSE 80

# Start nginx
CMD ["nginx", "-g", "daemon off;"]

