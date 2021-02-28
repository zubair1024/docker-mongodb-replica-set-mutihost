# MongoDB replica set using docker for multi-host (without using ingress network)

1. Add the following to your `/etc/hosts` file. Replace the addresses with the appropriate ones

```shell
127.0.0.1       mongo1
127.0.0.1       mongo2
127.0.0.1       mongo3
```

1. Start the docker containers

```shell
docker-compose -f ./mongo1-docker-compose.yml up -d
```

```shell
docker-compose -f ./mongo2-docker-compose.yml up -d
```

```shell
docker-compose -f ./mongo3-docker-compose.yml up -d
```

1. You can enter the docker container using the following command:

```shell
docker exec -it mongo1 sh -c "mongo --port 30001"
```

1. Initialize the container

```javascript
rs.initiate({
  _id: "my-replica-set",
  members: [
    { _id: 0, host: "mongo1:30001" },
    { _id: 1, host: "mongo2:30002" },
    { _id: 2, host: "mongo3:30003" },
  ],
});
```

1. Check the replica set status using

```javascript
rs.status();
```

Boom! you're done 😉
