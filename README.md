# Hyperledger_Market
stop and remove running docker container
```
docker stop $(docker ps -aq)
docker rm $(docker ps -aq)
```
run
```
docker-compose -f docker-compose.yml up -d
```
