FROM node:20-alpine

WORKDIR /app

# Install deps first (better Docker layer caching)
COPY package.json package-lock.json ./
RUN npm ci

# Copy the rest of the frontend code
COPY . .

EXPOSE 5173

# Vite must listen on 0.0.0.0 to be reachable from outside the container
CMD ["npm", "run", "dev", "--", "--host", "0.0.0.0", "--port", "5173"]