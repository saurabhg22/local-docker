# local-docker
Docker-compose for local development.

[![Build Status](https://travis-ci.org/joemccann/dillinger.svg?branch=master)](https://travis-ci.org/joemccann/dillinger)

## Installation
* Clone the repository
* Install docker-desktop from https://www.docker.com/get-started
* Start docker-desktop
* Get inside local-dokcer repository folder.

## MongoDB
* To run the MongoDB inside the docker container run the command
```sh
docker-compose up -d MongoDB
```

* If you want to connect with MongoDB from your host machine to the container then install mongo client on the host machine.
```sh
xcode-select --install
```
```sh
brew tap mongodb/brew
```
```sh
brew install mongodb-community-shell mongodb-database-tools mongosh
```
Now you can access your MongoDB instance by running the `mongo` command on the terminal.


## Elasticsearch
### Setup
* Bring up the containers by running
```sh
docker-compose up -d elasticsearch
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
docker-compose up -d elasticsearch
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

* To run the kibana inside the docker container run the command
```sh
docker-compose up -d kibana
```
Now you can access your kibana instance on http://localhost:5601. It will require a username and password.
username will be `elastic` and password will be `<YOUR_ELASTIC_USER_PASSWORD>`
