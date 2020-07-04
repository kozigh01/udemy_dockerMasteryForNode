FROM node:14.5-alpine

ENV CHARCOAL_FACTOR=0.1

RUN apk add --no-cache tini \
  && apk add --no-cache graphicsmagick

WORKDIR /app

COPY package*.json ./
RUN chown -R node:node .
USER node
RUN npm install && npm cache clean --force

COPY --chown=node:node . .

ENTRYPOINT [ "/sbin/tini", "--" ]
# CMD ["tail", "-f", "/dev/null"]
CMD ["node", "index.js"]