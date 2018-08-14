# turtlepool

## Deployment
```
docker network create --driver=overlay --attachable traefik_public
docker stack deploy --compose-file docker-compose.yaml abc
```


curl -d '{"jsonrpc":"2.0","id":1,"password":"passw0rd","method":"getStatus","params":{}}' http://47.75.124.123:8070/json_rpc