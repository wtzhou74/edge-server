# Short Description
Edge Server acts as a gatekeeper preventing unauthorized external requests from passing through.

# Full Description

# Supported Source Code Tags and Current `Dockerfile` Link

[`0.19.0 (latest)`](https://github.com/bhits-dev/edge-server/releases/tag/0.19.0), [`0.18.0`](https://github.com/bhits-dev/edge-server/releases/tag/0.18.0), [`0.17.0`](https://github.com/bhits-dev/edge-server/releases/tag/0.17.0)

[`Current Dockerfile`](../edge-server/src/main/docker/Dockerfile)

For more information about this image, the source code, and its history, please see the [GitHub repository](https://github.com/bhits-dev/edge-server).

# What is Edge Server?

The Edge Server acts as a gatekeeper to the outside world. It keeps unauthorized external requests from passing through. It uses [Spring Cloud Zuul](https://spring.io/guides/gs/routing-and-filtering/) as a routing framework, which serves as an entry point to the Consent2Share (C2S) microservices landscape. Zuul uses [Spring Cloud Ribbon](https://spring.io/guides/gs/client-side-load-balancing/) to lookup available services, and routes the external request to an appropriate service instance, facilitating Dynamic Routing and Load Balancing.

For more information and related downloads for Consent2Share, please visit [Consent2Share](https://bhits-dev.github.io/consent2share/).

# How to use this image

## Start a Edge Server instance

Be sure to familiarize yourself with the repository's [README.md](https://github.com/bhits-dev/edge-server) file before starting the instance.

`docker run  --name edge-server -d bhitsdev/edge-server:latest <additional program arguments>`

*NOTE: In order for this API to fully function as a microservice in the Consent2Share application, it is required to setup the dependency microservices and the support level infrastructure. Please refer to the Consent2Share Deployment Guide in the corresponding Consent2Share release (see [Consent2Share Releases Page](https://github.com/bhits-dev/consent2share/releases)) for instructions to setup the Consent2Share infrastructure.*


## Configure

The Spring profiles `application-default` and `docker` are activated by default when building images.

This API can run with the default configuration which is from three places: `bootstrap.yml`, `application.yml`, and the data which the [`Configuration Server`](https://github.com/bhits-dev/config-server) reads from the `Configuration Data Git Repository`. Both `bootstrap.yml` and `application.yml` files are located in the class path of the running application.

We **recommend** overriding the configuration as needed in the `Configuration Data Git Repository`, which is used by the `Configuration Server`.

Also, [Spring Boot](https://projects.spring.io/spring-boot/) supports other ways to override the default configuration to configure the API for a certain deployment environment. 

The following is an example to override the default database password:

`docker run -d bhitsdev/edge-server:latest --spring.datasource.password=strongpassword`

## Environment Variables

When you start the Edge Server image, you can edit the configuration of the Edge Server instance by passing one or more environment variables on the command line. 

### JAR_FILE

This environment variable is used to setup which jar file will run. you need mount the jar file to the root of container.

`docker run --name edge-server -e JAR_FILE="edge-server-latest.jar" -v "/path/on/dockerhost/edge-server-latest.jar:/edge-server-latest.jar" -d bhitsdev/edge-server:latest`

### JAVA_OPTS 

This environment variable is used to setup JVM argument, such as memory configuration.

`docker run --name edge-server -e "JAVA_OPTS=-Xms512m -Xmx700m -Xss1m" -d bhitsdev/edge-server:latest`

### DEFAULT_PROGRAM_ARGS 

This environment variable is used to setup an application argument. The default value is "--spring.profiles.active=application-default,docker".

`docker run --name edge-server -e DEFAULT_PROGRAM_ARGS="--spring.profiles.active=application-default,ssl,docker" -d bhitsdev/edge-server:latest`

# Supported Docker versions

This image is officially supported on Docker version 1.13.0.

Support for older versions (down to 1.6) is provided on a best-effort basis.

Please see the [Docker installation documentation](https://docs.docker.com/engine/installation/) for details on how to upgrade your Docker daemon.

# License

View [license](https://github.com/bhits-dev/edge-server/blob/master/LICENSE) information for the software contained in this image.

# User Feedback

## Documentation 

Documentation for this image is stored in the [bhitsdev/edge-server](https://github.com/bhits-dev/edge-server) GitHub repository. Be sure to familiarize yourself with the repository's README.md file before attempting a pull request.

## Issues

If you have any problems with or questions about this image, please contact us through a [GitHub issue](https://github.com/bhits-dev/edge-server/issues).