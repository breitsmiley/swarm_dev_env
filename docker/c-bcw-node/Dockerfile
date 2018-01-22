FROM node:9.4.0-alpine

RUN mkdir -p /opt/app

ARG NODE_ENV=production
ENV NODE_ENV $NODE_ENV

ARG PORT=3000
ENV PORT $PORT
EXPOSE $PORT 5858 9229

# TODO - check that service returns HTTP 200
#HEALTHCHECK CMD curl -fs http://localhost:$PORT/healthz || exit 1

# Install dependencies
#-------------------------------------
WORKDIR /opt
COPY  /apps/book-worker/package*.json ./
RUN npm install && npm cache clean --force
ENV PATH /opt/node_modules/.bin:$PATH
#-------------------------------------

# Copy project files as late as possible
WORKDIR /opt/app
COPY /apps/book-worker ./

CMD [ "node", "app.js" ]