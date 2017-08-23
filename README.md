## Gitlab Rancher deployment Example

In this example we will create an installation of Gitlab and Rancher from strach on Digitalocean.

### 1. Gitlab

#### 1.0. create Gitlab Digitalocean VM

````
docker-machine create --driver digitalocean --digitalocean-access-token $DOTOKEN --digitalocean-image ubuntu-16-04-x64 --digitalocean-size 4gb --digitalocean-tags gitlab-rancher-example gitlab-host
eval $(docker-machine env gitlab-host)
````

#### 1.1 start Gitlab UI
````
cd gitlab-ui
cat docker-compose.yml
docker-compose up -d
````


#### 1.2 start Gitlab CI runner

````
cd gitlab-runner
cat docker-compose.yml
docker-compose up -d
````


register gitlab-runner to the gitlab instance:
````
docker exec -it gitlabrunner_web_1 bash
gitlab-runner register
````
* coordinator URL: http://DOCKER_MACHINE_IP
* CI token: login as root in Gitlab UI >> admin area >> runners
* executor: docker
* default docker image: java:8-jdk

check registered runner on Gitlab UI: login as root in Gitlab UI >> admin area >> runners

#### 1.3 create a Gitlab user

#### 1.4 create a Gitlab repository
- Generate Gitlab Personal access token: Github >> Settings Personal Access tokens >> create
- Import from https://github.com/mariodavid/kubanische-kaninchenzuechterei

#### 1.5 configure Gitlab CI
Set up CI >> Gradle template

#### 1.6 run Gitlab CI pipeline

### 2. Rancher

#### 2.0 create Rancher Digitalocean VM
````
docker-machine create --driver digitalocean --digitalocean-access-token $DOTOKEN --digitalocean-image ubuntu-16-04-x64 --digitalocean-size 4gb --digitalocean-tags gitlab-rancher-example rancher-ui-host
eval $(docker-machine env rancher-ui-host)
````

#### 2.1 start Rancher UI
````
cd rancher
cat docker-compose.yml
docker-compose up -d
````

#### 2.2 create access control, environment & API token
