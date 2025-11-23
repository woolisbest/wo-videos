FROM node:18-bullseye

# Install system deps and pin yt-dlp via pip with a fixed version for reproducibility
RUN apt-get update && apt-get install -y python3 python3-pip ffmpeg curl ca-certificates git \
  && pip3 install "yt-dlp==2025.02.01" \
  && apt-get clean && rm -rf /var/lib/apt/lists/*

WORKDIR /usr/src/app

# copy package.json to install production deps only
COPY package.json package-lock.json* ./
RUN npm ci --only=production --no-audit --no-fund

# copy server sources
COPY server ./server

EXPOSE 3333
CMD ["node", "server/index.js"]