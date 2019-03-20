# 2 - Docker Compose

Docker Compose is a useful tool for defining applications that span multiple containers. The configuration for these Docker applications in written in a YAML file, entitled `docker-compose.yml` invoking the `docker-compose up` command will run the entire application within their individual containers. Docker Compose comes in handy when developing for multiple different environments (ex. _staging_, _production_, _development_, _testing_, even _CI_).

If you've ever heard the term `to dockerize` an application, then this is likely what they were referring to. Specifying containers for each component of your app to run inside to create your isolated environment (as specified by your Dockerfile). For automation/QA purposes, docker-compose can make black-box tests a breeze, since you can specify everything without worrying about caches or external factors.

Boiled down, there are main steps to create a basic `docker-compose` setup (these are taken directly from Docker themselves):

1. Define your app’s environment with a `Dockerfile` so it can be reproduced anywhere.
2. Define the services that make up your app in `docker-compose.yml` so they can be run together in an isolated environment.
3. Run `docker-compose up` and Compose starts and runs your entire app.
