#### Build context: /../.. (ie, project root)

#### Stage 1: Build client
# Code from: https://github.com/Microsoft/vscode-remote-try-node
ARG VARIANT="14-buster"
FROM mcr.microsoft.com/vscode/devcontainers/javascript-node:0-${VARIANT} AS build
# FROM node:12.4.0-alpine AS build
# FROM node:14-buster AS build

# Copy whole app to workspace
WORKDIR /workspace
COPY . ./

# # Build self packages first
WORKDIR /workspace/lib/editor
# # TODO: 目前只要app裡的各個file編輯了就需要re-install，應該要將install獨立出來做成cache
RUN yarn

# Copy the package.json as well as the package-lock.json and install
# the dependencies. This is a separate step so the dependencies
# will be cached unless changes to one of those two files
# are made.
# COPY package.json package-lock.json ./client/

WORKDIR /workspace/frontend/web
RUN yarn

# RUN yarn && yarn build

# #### Stage 2: Serve the React application from Nginx
# FROM nginx:1.17.0-alpine

# # Copy the react build from Stage 1
# COPY --from=build /workspace/client/web/build /var/www

# # Copy our custom nginx config
# COPY ./configs/nginx.conf /etc/nginx/nginx.conf

# # Expose port 3000 to the Docker host, so we can access it
# # from the outside.
# EXPOSE 80

# ENTRYPOINT ["nginx","-g","daemon off;"]
