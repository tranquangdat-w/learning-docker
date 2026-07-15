ARG NODE_VERSION=20

FROM node:${NODE_VERSION}-alpine AS deps
WORKDIR /node-app
COPY package.json package-lock.json ./
RUN npm ci --only=production 
RUN npm cache clean --force

FROM node:${NODE_VERSION}-alpine AS release
WORKDIR /app
COPY --from=deps /node-app/node_modules ./node_modules
COPY server.js .
EXPOSE 3000
ENTRYPOINT [ "node", "server.js" ]

