FROM node:22.19-bullseye AS build
WORKDIR /app

# Copy package files first (for caching)
COPY package*.json ./

# Copy the rest of the app
COPY . .

RUN npm i

# Build Nuxt
RUN npm run build

# --- Production stage ---
FROM node:22.19-bullseye AS production
WORKDIR /app
COPY --from=build /app/.output ./
EXPOSE 3000
CMD ["node", "server/index.mjs"]
