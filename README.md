# local-docker
Docker compose for local development.

[![Build Status](https://travis-ci.org/joemccann/dillinger.svg?branch=master)](https://travis-ci.org/joemccann/dillinger)

## Installation
* Install docker-desktop from https://www.docker.com/get-started
* Start docker-desktop

## MongoDB
* To run the mongodb inside docker container run the command
```sh
docker-compose up monogdb -d
```

* If you want to connect with mongodb from your host machine to container then install mongo client on host machine.
```sh
xcode-select --install
```
```sh
brew tap mongodb/brew
```
```sh
brew install mongodb-community-shell mongodb-database-tools mongosh
```

## Elasticsearch
### Setup
* Bring up the containers by running
```sh
docker-compose up elasticsearch -d
```
* While docker-compose up is running, get inside the elasticsearch container by running the command:
```sh
docker-compose exec elasticsearch bash
```
Then run the following command to generate passwords for all the built-in users:
```sh
[root@a4f615e87653 elasticsearch]# bin/elasticsearch-setup-passwords auto
```
Note them down and keep them somewhere safe. Exit the container by pressing CTRL+D

* Now restart the elasticsearch docker container by running the command:
```sh
docker-compose down elasticsearch
docker-compose up elasticsearch -d
```
Now you can access your elasticsearch instance on http://elastic:<YOUR_ELASTIC_USER_PASSWORD>@localhost:9200

> Note: You can change your elastic password by making a post request from Postman or Kibana.

```
POST /_security/user/elastic/_password
{
  "password" : <YOUR_NEW_PASSWORD>
}
```

## Kibana

* Open the kibana.yml file and change the `elasticsearch.password`. It should look like this:
```yml
server.name: kibana
server.host: "0"
elasticsearch.hosts: [ "http://elasticsearch:9200" ]
elasticsearch.username: kibana
elasticsearch.password: <kibana password>
```

* To run the kibana inside docker container run the command
```sh
docker-compose up kibana -d
```
Now you can access your kibana instance on http://localhost:5601. It will require username and password.
username will be `elastic` and password will be `<YOUR_ELASTIC_USER_PASSWORD>`
