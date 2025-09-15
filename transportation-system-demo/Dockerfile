# --------------------------
# Stage 1: Build React app
# --------------------------
FROM node:20-alpine AS build

# Set working directory inside container
WORKDIR /app

# Copy package.json and package-lock.json first for caching
COPY transportation-system-demo/package*.json ./

# Install dependencies
RUN npm ci

# Copy the rest of your source code
COPY transportation-system-demo/ ./

# Copy locales if needed
COPY locales ./locales

# Build the app for production
RUN npm run build

# --------------------------
# Stage 2: Production with Nginx
# --------------------------
FROM nginx:alpine

# Remove default nginx HTML
RUN rm -rf /usr/share/nginx/html/*

# Copy built React app from previous stage
COPY --from=build /app/dist /usr/share/nginx/html

# Expose port 80
EXPOSE 80

# Start nginx
CMD ["nginx", "-g", "daemon off;"]
