FROM node:16-alpine as builder

RUN mkdir /app && chown node:node /app
WORKDIR '/app'

USER node
COPY --chown=node:node package.json package-lock.json* ./
RUN npm install
COPY --chown=node:node . .
RUN npm run build


FROM nginx
EXPOSE 3000
COPY ./nginx/default.conf /etc/nginx/conf.d/default.conf
COPY --from=builder /app/build /use/share/nginx/html
CMD ["npm", "run", "start"]