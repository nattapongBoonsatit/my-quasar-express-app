# Stage 1: Build Quasar SPA
FROM node:22-alpine AS build
WORKDIR /app

COPY package*.json ./
RUN npm ci --ignore-scripts

COPY . .
RUN npx quasar prepare && npx quasar build

# Stage 2: Serve static files with Nginx
FROM nginx:alpine AS runtime
COPY --from=build /app/dist/spa /usr/share/nginx/html

EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]