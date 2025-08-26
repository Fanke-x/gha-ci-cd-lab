# Simple Node app image; multi-stage for best practices
FROM node:20-alpine AS deps
WORKDIR /app
COPY src/node-app/package*.json ./
RUN npm ci --omit=dev

FROM node:20-alpine AS runner
WORKDIR /app
COPY --from=deps /app/node_modules ./node_modules
COPY src/node-app/src ./src
COPY src/node-app/package*.json ./
CMD ["node", "src/index.js"]