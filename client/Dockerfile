# This is a multi-stage docker file.

# For the first stage a node image has been used.
FROM node:14 AS web-build  

# Define a working directory to place the resources relavant to the work we're doing within the image's filesystem.
WORKDIR /usr/src/app

# Copy everything from the current directory where the Dockerfile exists, to the destination
# inside the image's filesystem: /usr/src/app/client
COPY ./ ./client

# Change directory to "client" inside the working directory and perform the specified commands.
RUN cd client && npm install && npm run build --prod

# Second stage
# Use official nginx image as the base image
FROM nginx:latest

# Copy the build output to replace the default nginx contents.
COPY --from=web-build /usr/src/app/client/dist/client/ /usr/share/nginx/html
COPY nginx.conf /etc/nginx/conf.d/default.conf

# Expose port 4200
EXPOSE 4200
