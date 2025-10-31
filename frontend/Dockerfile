FROM node:18-alpine AS build
WORKDIR /app

# install dependencies
COPY package*.json ./
# Use npm install instead of npm ci because this repo doesn't include a package-lock.json
# `npm ci` requires a lockfile; `npm install` will work without it (slightly less deterministic).
RUN npm install --silent

# copy sources and build
COPY . .
RUN npm run build

FROM nginx:stable-alpine
COPY --from=build /app/dist /usr/share/nginx/html
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
