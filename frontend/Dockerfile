FROM node:16

WORKDIR /app

# Set npm registry to avoid timeout issues
RUN npm config set registry https://registry.npmmirror.com \
    && npm config set fetch-retries 5 \
    && npm config set timeout 60000

# Copy only package.json to avoid errors if package-lock.json is missing
COPY package.json ./

# Clean npm cache before install
RUN npm cache clean --force && npm install --legacy-peer-deps

COPY . .

CMD ["npm", "start"]
