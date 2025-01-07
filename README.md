# Rack Infra 
rack gateway infra 

[Stack](#stack)     
[Deployment](#deployment)   
[Configuration](#configuration)    


## Stack 
- **Database:** `postgres`
- **Mq:** `nats`
- **Logging:** `parseable`
- **Orchestration:** `docker compose`

## Deployment
- Create [config](#configuration) (path: deploy/.env) 
- Build images:
```sh
# rack api
docker buildx build -t rack/api:1.0 -f api/Dockerfile ./
# rack blockchain
docker buildx build -t rack/blockchain:1.0 -f blockchain/Dockerfile ./
```
- Run:
```
cd deploy
docker-compose --env-file .env -f docker-compose.yml up nats postgres parseable -d
docker-compose --env-file .env -f docker-compose.yml up blockchain -d
docker-compose --env-file .env -f docker-compose.yml up api -d
```

## Configuration 
| Key         | Description        |
| ----------- | -------            |
| `PROD_ENV`    | production env   `(true/false)`  |
| `API_IPV4`     |   api address (`ip:port`)|
| `API_PROTO`      | protocol (`http/https`) |
| `API_ADMIN_KEY`      |  yet unused |
| `COINMARKET_API`      | [coinmarketcap](https://coinmarketcap.com) api key |
| `ETH_RPC_KEY`      | [infura](https://infura.io) api key |
| `ETH_TESTNET`      | enbale testnet for eth (`true/false`)|
| `SOL_TESTNET`      | enable testnet for sol (`true/false`)|
| `TON_TESTNET`      | enable testnet for ton (`true/false`)|
| `DB_HOST`      |  postgres host (`ip`)|
| `DB_USER`      | postgres user |
| `DB_PASSWORD`      | postgres password |
| `DB_NAME`      | postgres db name|
| `DB_PORT`      | postgres db port|
| `DB_SSL_MODE`      | postgres ssl mode (`enable/disable`) |
| `NATS_SERVERS`      | nats servers (`nats://login:pass@ip1:port1, nats://login:pass@ip2:port2, nats://login:pass@ip2:port2, etc`)|
| `TESTING`      | do not enable (`true/false`)|
| `PARSEABLE_USERNAME`      | [parseable](https://github.com/parseablehq/parseable) username |
| `PARSEABLE_PASSWORD`      | [parseable](https://github.com/parseablehq/parseable) password |
| `PARSEABLE_URL`      | [parseable](https://github.com/parseablehq/parseable) url (`http://ip:port`) |
| `UNIX_SOCKET`      | unix socket (`path (/tmp/racklog)`)|
