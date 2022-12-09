FROM node:19-alpine as builder


# minimal apk dependencies to be safe
ENV PACKAGES="curl ca-certificates" \
    NODE_ENV="production" \
    HOST="0.0.0.0:8080"

RUN apk add --no-cache $PACKAGES

COPY .  /usr/src/app
WORKDIR /usr/src/app

RUN npm install
RUN npm install --save babel-cli
RUN npm run build

FROM node:19-alpine
COPY --from=builder /usr/src/app/build ./dist
# Run as non-root user for security
USER 1000

# Expose app port (8080/tcp)
EXPOSE 8080

CMD [ "node", "start" ]
