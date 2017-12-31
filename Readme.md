# Hello World Concourse

## Introduction

Hello World project to Concourse CI

## Contents

- [Usage](#usage)
- [TODO](#todo)

## Usage

First time usage only:

```bash
# Generate keys
./gen-keys.sh

# Download the "Fly" cli
curl -LO https://github.com/concourse/concourse/releases/download/v3.8.0/fly_darwin_amd64
chmod a+x fly_darwin_amd64
sudo mv fly_darwin_amd64 /usr/local/bin/fly
```

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

```bash
fly -t lite set-pipeline -p hello-world -c pipelines/dummy-golang-project/dummy-golang-project.yml
```

## TODO

- [ ] Everything
