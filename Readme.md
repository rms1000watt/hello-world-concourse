# Hello World Concourse

## Introduction

Hello World project to Concourse CI

## Contents

- [First Time Usage](#first-time-usage)
- [Start Concourse](#start-concourse)
- [Pipelines](#pipelines)
- [TODO](#todo)

## First Time Usage

First time usage only:

```bash
# Generate keys
./gen-keys.sh

# Download the "Fly" cli
curl -LO https://github.com/concourse/concourse/releases/download/v3.8.0/fly_darwin_amd64
chmod a+x fly_darwin_amd64
sudo mv fly_darwin_amd64 /usr/local/bin/fly

# Write your docker creds to file (demo purposes only)
cat << EOF >> pipelines/dummy-projects/creds.yml
docker-email: <EMAIL_HERE>
docker-user: <USERNAME_HERE>
docker-pass: <PASSWORD_HERE>
EOF
```

## Start Concourse

Start concourse:

```bash
docker-compose up -d
```

Login to concourse from the cli:

```bash
fly -t lite login -c http://localhost:8080

# username: concourse
# password: changeme
```

## Pipelines

### Hello World Pipeline

Add the Hello World pipeline & "unpause" it:

```bash
fly -t lite set-pipeline -p hello-world -c pipelines/hello-world/hello-world.yml

# apply configuration? [yN]: y

fly -t lite unpause-pipeline -p hello-world

open http://localhost:8080/teams/main/pipelines/hello-world
```

- Login with: concourse/changeme
- Click on the "hello-world" square
- Click on the "+" on the top right of the screen
- Watch the output

### Dummy Projects Pipeline

```bash
fly -t lite set-pipeline -p dummy-projects -l pipelines/dummy-projects/creds.yml -c pipelines/dummy-projects/dummy-projects.yml
fly -t lite unpause-pipeline -p dummy-projects
fly -t lite trigger-job --job dummy-projects/build-dummy-golang-project
fly -t lite trigger-job --job dummy-projects/build-dummy-nodejs-project
open http://localhost:8080/teams/main/pipelines/dummy-projects
```

## TODO

- [ ] Implement proper security model
- [ ] Implement multitenant model
- [ ] Implement maching tagging of Github & versioning of Docker images
