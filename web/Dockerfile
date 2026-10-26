# 1) Build the static site with Node
FROM node:26-alpine AS build
WORKDIR /app
# Deps first: this layer stays cached until package files change
COPY package.json package-lock.json .npmrc ./
RUN npm ci
COPY . .
RUN npm run build

# 2) Serve the static files with Caddy, Node is not shipped
FROM caddy:2-alpine
COPY --from=build /app/build /srv
COPY Caddyfile /etc/caddy/Caddyfile
