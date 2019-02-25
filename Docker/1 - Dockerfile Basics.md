# 1 - Dockerfile Basics

## What is a Dockerfile

A `Dockerfile` is a text document that contains a set of instructions which are passed on command line to assemble the _image_ which sets up the container. An **image** is just the term used to specify the blueprint of the environment created for running the contained software.

All docker commands are executed by using a _COMMAND_ followed by the command _VALUES_ or _OPERATIONS_. Instead of listing off every command with their use case, an explanation and all its combinations, I'll just reference [this great resource](https://kapeli.com/cheat_sheets/Dockerfile.docset/Contents/Resources/Documents/index) that does just that.

Here is an example of completed Dockerfile:

```Dockerfile
# ./Dockerfile

FROM node:boron-alpine              # base image: Alpine Linux + Node.js
RUN mkdir -p /usr/app               # mkdir inside container
WORKDIR /usr/app                    # cd to /usr/app
COPY package.json .                 # copy package.json to current directory
RUN npm cache clean && npm install  # install node_modules
VOLUME /usr/app/node_modules        # specify fs mount point
COPY . .                            # copy all source code into /usr/app
VOLUME /usr/app                     # specify fs mount point
EXPOSE 8080                         # specify port to expose on container

# Other commands: CMD, ENV. ADD, USER, ENTRYPOINT, ONBUILD
```
