# Stage 1: Build the frontend
FROM node:16 AS fronted-builder
WORKDIR /app/fronted
COPY fronted/package.json fronted/package-lock.json ./
RUN npm install
COPY fronted ./
RUN npm run build

# Stage 2: Build the backend
FROM node:16 AS backend-builder
WORKDIR /app/backend
COPY backend/package.json backend/package-lock.json ./
RUN npm install
COPY backend ./

# Stage 3: Final container
FROM node:16
WORKDIR /app
COPY --from=fronted-builder /app/fronted/build ./fronted
COPY --from=backend-builder /app/backend ./
EXPOSE 3002 8002
CMD ["node", "src/server.js"]