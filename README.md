# pino-papertrail-runner

Utility for running a node-project in a docker container and logging with pino to [papertrail](https://papertrailapp.com/).

Uses the technique from https://github.com/mattiash/docker-pino-sample to make sure that the exit codes are passed correctly.

## Usage

In your Dockerfile, do the following:

```
FROM node

RUN npm install -g pino-papertrail-runner

...

CMD ["pino-papertrail-runner"]
```

For this to work:

- The last WORKDIR command before CMD must be the root of your node project
- Your package.json must have a "start" script that runs your project
- You must pass in the environment variables PAPERTRAIL_HOST and PAPERTRAIL_PORT to specify the log target

The "appname" for your logs will be set to the name-property in your package.json.
To set the hostname for your papertrail logs,
pass a `--hostname` parameter to docker run. 

