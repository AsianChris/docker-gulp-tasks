# docker-gulp-tasks
Docker container to run gulp tasks

## Build Image
```
$ docker build -t gulpd .
```

## Usage
Basic usage where <command> is the command to pass

```
$ docker run --rm --user="$(id -u):$(id -g)" -v $('pwd'):/opt gulpd <command>
```

* `docker` is the docker command
* `--rm` is optional. This is to remove the container when the command is completely or has been manually stopped
* `--user="$(id -u):$(id -g)"` is optional. This is so the Docker container will write files using the currently logged in user on the host machine. Otherwise file permissions will be for `root:root`
* `-v $('pwd'):/opt` is required. It'll mount the current working directory on the host machine into the Docker Container. `/opt` is the working directory within the container
* `gulpd` is the Docker Image
* `<command>` is optional. This is a shell command to be ran within the container. Container will run `gulp build` if no command is passed

Examples:
```
$ docker run --rm --user="$(id -u):$(id -g)" -v $('pwd'):/opt gulpd npm install
$ docker run --rm --user="$(id -u):$(id -g)" -v $('pwd'):/opt gulpd gulp watch
```

By default, if no command is given, it'll automatically run `gulp watch`

Stopping the container will require you to open another terminal window to run the following commands
```
$ docker ps
$ docker stop <container id>
```

## More Information
For more information on (Docker Docs)[https://docs.docker.com/]
