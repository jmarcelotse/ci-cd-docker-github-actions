# Etapa 1: build
FROM node:18-alpine AS builder
WORKDIR /app
COPY package*.json ./
RUN npm ci
COPY . .

# Etapa 2: runtime
FROM node:18-alpine
WORKDIR /app
COPY --from=builder /app .

EXPOSE 3000
CMD ["npm", "start"]
