# CHAINLENS

## Introduction

Chainlens is a blockchain explorer which helps us to visualize blockchain (blockchain explorer). It supports both public and private ethereum networks.

Chainlens provides an overview of the entire network, including block information, contract metadata, transaction searches.

Chainlens supports **Quorum, Hyperledger Besu and Ethereum networks.**

## Steps to run Chainlens

1. Clone the chainlens repository

```bash
git clone https://github.com/web3labs/chainlens-free
```

2. Now go inside the chainlens-free/docker-compose folder

```bash
cd chainlens-free/docker-compose
```

3. Now to start the chainlens we have to specify the node endpoint and the bring up the docker compose files along with the network

```bash
NODE_ENDPOINT=http://172.16.239.1:9547 docker compose -f docker-compose.yml -f chainlens-extensions/docker-compose-custom.yaml up
```

**Note: You must connect to one of the privacy nodes (for example, member1besu), not the dedicated RPC, to allow access for Besu privacy API methods. In production networks, you must secure access to RPC nodes.**

4. Here we have specified the node endpoint along with the RPC port because this is the endpoint it will connect to

- Note that if setting NODE_ENDPOINT to a local Ethereum instance, you may need to use the IP address associated with the Docker bridged interface.

-On Linux, the bridged adapter should be **172.16.239.1**, as denoted in docker-compose.yml. 

```bash
networks:
  epirus:
    name: epirus-net
    driver: bridge
    ipam:
      driver: default
      config:
        - subnet: 172.16.239.0/24
```

5. The first docker-compose.yml file in the command contains all the services required for Chainlens.

- api
- mongo db
- redis
- nginx
- ui
- ingestion

6. The second docker compose file contains the service required for private network

- This private network runs with CLIQUE consensus
- With 1 peer and 1 validator

7. The explorer runs on port 80 by default. If you want to use custom port 
Eg: 26000, set the PORT env

- Eg: NODE_ENDPOINT=http://localhost:8585 PORT=26000 docker-compose up -d

8. You will be able to access the Explorer UI via: http://localhost/

9. To stop the chainlens container execute the following command

- docker compose down