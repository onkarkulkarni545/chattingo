# Stage 1: Build deps
FROM node:18-alpine AS deps
WORKDIR /app
COPY package.json yarn.lock* ./
RUN npm ci

# Stage 2: Build assets
FROM node:18-alpine AS builder
WORKDIR /app
COPY --from=deps /app/node_modules ./node_modules
COPY . .
RUN npm run build

# Stage 3: Static web server
FROM nginx:1.25-alpine AS runner
COPY --from=builder /app/build /usr/share/nginx/html
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
