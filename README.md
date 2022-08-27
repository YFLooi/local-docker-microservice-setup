# local-docker-microservice-setup
Run multiple repos as microservices on local using docker-compose

## Start command
`docker compose -f docker-compose.local-microservices.yml --env-file ./.env up`

For older docker-compose installations, replace `docker compose` with `docker-compose`

Add flag `--detach`  to stop showing logs

## Stop command
`docker compose -f docker-compose.local-microservices.yml --env-file ./.env down`

Add flag `-v` to also remove created volumes

## Services in this repo:
1. nestjs-orders-app (PORT 3200)
   Records and retrieves orders in DB

2. operations-portal (PORT 3000)
   Allows viewing and editing incoming orders
   Count of send attempts maintained using state machine

3. payment-app (PORT 3400)
   Process payments. Randomly decides payment response to mock payment failure

