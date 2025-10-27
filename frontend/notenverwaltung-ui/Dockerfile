# Build stage: compile React app
FROM node:20-alpine AS builder
WORKDIR /app
COPY package*.json ./
# Install production dependencies (falls kein package-lock vorhanden ist, nutzt npm install)
RUN npm install --production
COPY . .
RUN npm run build

# Production stage: serve static files with nginx
FROM nginx:stable-alpine
COPY --from=builder /app/build /usr/share/nginx/html
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
