# INF226 Support Material

[Mandatory 1](mandatory1.md)
[Mandatory 2](mandatory2.md)

## Mandatory 3 : Analyzing the software

## TL;DR

* Install [Docker](https://www.docker.com/products/docker-desktop)
* Use the [docker-compose file](https://mitt.uib.no/courses/24957/files/2835955/download?download_frd=1)
* Create a project in SonarQube
* Analyse
* Use [OWASP ZAP](https://www.zaproxy.org/download/)
* [SonarLint](https://www.sonarlint.org/)
* [Setting up the project guide](sonarguide.md)

### Docker Setup

The easiest way to deal with this is to install Docker on your computer.

[Docker Desktop](https://www.docker.com/products/docker-desktop)

You may have to create an account to use Docker.

[Short 100 seconds introduction to Docker](https://www.youtube.com/watch?v=Gjnup-PuquQ)

There are many ways of using Docker so it's easy to get lost in what is happening.

## How to use Docker-Compose

Håkon has supplied a `docker-compose.yml` file at [MittUiB](https://mitt.uib.no/courses/24957/files/2835955/download?download_frd=1)

When you download this file and place it in a folder.

You have to start __sonarqube__ from this folder everytime.

With `docker-compose` we use the command `docker-compose up` to start the service.

PS: docker-compose.yml has to be in the same directory you are running docker-compose command from.

__Example__:

```sh
kenneth@kefo ~/inf226.h20/docker-example > ls
docker-compose.yml // this file has to be in the directory 
kenneth@kefo ~/inf226.h20/docker-example > docker-compose up
.... lots of text ...
sonarqube_1  | 2020.10.20 09:09:50 INFO  app[][o.s.a.SchedulerImpl] SonarQube is up
// pressing CTRL-C will stop it.
^CGracefully stopping... (press Ctrl+C again to force)
Stopping docker-example_sonarqube_1 ... done
Stopping docker-example_db_1        ... done

kenneth@kefo ~/inf226.h20/docker-example >
```

You can also `-d` option on `docker-compose`.

Here is to start and stop using `docker-compose -d`

```sh
kenneth@kefo ~/inf226.h20/docker-example > docker-compose up -d
Starting docker-example_db_1 ... done
Starting docker-example_sonarqube_1 ... done

kenneth@kefo ~/inf226.h20/docker-example > docker-compose down
Stopping docker-example_sonarqube_1 ... done
Stopping docker-example_db_1        ... done
Removing docker-example_sonarqube_1 ... done
Removing docker-example_db_1        ... done
Removing network docker-example_default
kenneth@kefo ~/inf226.h20/docker-example > 
```

You are now ready to use SonarQube (last section)


### Using Docker Hub

This is more complicated to setup, but is my preferred way of doing things.

#### Fetching the SonarQube image

```sh
kenneth@kefo ~/inf226.h20 > docker pull sonarqube
Using default tag: latest
latest: Pulling from library/sonarqube
cbdbe7a5bc2a: Pull complete 
ad75d47265c8: Pull complete 
43f3acb0c861: Pull complete 
bfe61efc35b0: Pull complete 
cc57849e5ff2: Pull complete 
Digest: sha256:10bb6f658a4a716733b6226a165897237fd031d8b02e6f7eddc639125eb8607e
Status: Downloaded newer image for sonarqube:latest
docker.io/library/sonarqube:latest
kenneth@kefo ~/inf226.h20 >
```

#### Installing the container

This part is only done once, you will get error messages if you do it several times.

`--name` is something we give it.

 I've named mine *sonarqube-inf226*, you can name yours anything.

```sh
docker run -d --name sonarqube-inf226 -p 9000:9000 sonarqube:latest
```

When this command is done, the service is already running.

You can then check it with `docker ps`.

After this use the routines described in the next section.

#### Starting, stopping, status on the SonarQube container

We can now start and stop with the following commands:

* `docker start nameyougaveit` to start sonarqube
* `docker ps` to check what is running on the system
* `docker stop nameyougaveit` to stop sonarqube

__Example__:

```sh
kenneth@kefo ~/inf226.h20 > docker start sonarqube-inf226 
sonarqube-inf226

kenneth@kefo ~/inf226.h20 > docker ps  
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                    NAMES
7463e290d232        sonarqube:latest    "bin/run.sh bin/sona…"   3 minutes ago       Up 7 seconds        0.0.0.0:9000->9000/tcp   sonarqube-inf226


kenneth@kefo  ~/inf226.h20 > docker stop sonarqube-inf226 
sonarqube-inf226

kenneth@kefo ~/inf226.h20 >
```

#### Troubleshooting

`docker rm sonarqube-inf226` will remove the container that we created for this.

### SonarQube

When you have SonarQube up, you can login using the following details:

Now you can open your browser and log in to SonarQube at [http://localhost:9000](http://localhost:9000)

* Username: admin
* Password: admin

[Setting up the project guide](sonarguide.md)

#### Resources

* [SonarLint](https://www.sonarlint.org/)
* [Docker Hub SonarQube](https://hub.docker.com/_/sonarqube/)
* [Docker Compose](https://docs.docker.com/compose/)