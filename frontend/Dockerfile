# Build step
FROM node:18-alpine as build
WORKDIR /app

ENV NODE_OPTIONS=--openssl-legacy-provider

COPY package*.json ./
RUN npm install
COPY . .
RUN npm run build

# Serve with nginx
FROM nginx:alpine
WORKDIR /usr/share/nginx/html

COPY --from=build /app/build .

# Inject runtime config
COPY ./runtime-config.sh /docker-entrypoint.d/

EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
