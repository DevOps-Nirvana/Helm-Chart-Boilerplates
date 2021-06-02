###
# First, using a NodeJS builder container build our frontend assets
FROM node:12 as builder
# Setup
WORKDIR /app
# Copy just our package so we can install deps, this helps with Docker layer caching
COPY package.json /app/
# Run npm install for our dependencies for production builds no dev/test stuff
RUN npm install 
# Now copy our entire app, which will be new every time (not using a docker layer cache)
COPY . /app/
# And run our npm build
RUN npm run build

###
# Second, using an Apache 2.4 image with modifications for kubernetes and SPA already
FROM andrewfarley/docker-kubernetes-apache-proxy:latest
# Then copy in our pre-built static files
COPY --from=builder /app/build/ /usr/local/apache2/htdocs/
