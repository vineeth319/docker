FROM node:20.20.2-alpine3.23 AS builder

WORKDIR /app

COPY package.json .
COPY *.js .

RUN npm install

FROM node:20.20.2-alpine3.23

WORKDIR /app

COPY --from=builder /app /app

ENV REDIS_URL=redis://redis:6379 \
    MONGO_URL=mongodb://mongodb:27017/catalogue

EXPOSE 8080

RUN addgroup -S roboshop && \
    adduser -S roboshop -G roboshop && \
    chown -R roboshop:roboshop /app

USER roboshop

ENTRYPOINT ["node"]
CMD ["server.js"]