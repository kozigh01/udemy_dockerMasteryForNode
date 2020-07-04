FROM node:10-alpine as prod
EXPOSE 3000
ENV NODE_ENV=production
RUN apk add --no-cache tini
WORKDIR /app
COPY package*.json ./
RUN chown -R node:node .
USER node
RUN npm install --only=production && npm cache clean --force
COPY --chown=node:node . .
ENTRYPOINT [ "/sbin/tini", "--" ]
CMD ["node", "./bin/www"]


FROM prod as dev
ENV NODE_ENV=development
RUN npm install --only=development
CMD ["npm", "run", "dev"]


FROM dev as test
ENV NODE_ENV=test
CMD ["npm", "run", "test"]
