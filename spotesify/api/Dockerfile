FROM node:20-alpine

WORKDIR /app

RUN addgroup -S spotesify && adduser -S spotesify -G spotesify

COPY package*.json ./

RUN npm install --omit=dev && npm cache clean --force

COPY . .

RUN mkdir -p /data/music && chown -R spotesify:spotesify /app /data/music

USER spotesify

EXPOSE 5000

HEALTHCHECK --interval=10s --timeout=3s --retries=3 \
  CMD node -e "require('http').get('http://localhost:5000/api/health', r => process.exit(r.statusCode === 200 ? 0 : 1)).on('error', () => process.exit(1))"

CMD ["npm", "start"]
