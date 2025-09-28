# next js ECS Dockerfile
FROM node:20-alpine AS base
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
RUN npm run build
FROM base AS production
RUN npm install next -g
EXPOSE 3000
ENV NODE_ENV production