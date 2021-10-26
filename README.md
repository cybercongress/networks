# Cyber networks

This repo contain info about all active and upcoming cyber chains. 

-------

## Bostrom gentx ceremony started!

**GenTx must be submited by 0:00 UTC 1st November**

The relevant guide for praticipating in genesis could be found [here](https://github.com/cybercongress/networks/blob/main/bostrom/genesis-validator.md).


For those who want to verify bostrom genesis file without signing: [QmQAd2SBwypsz5ZqkYgeSTFLq3peGV9xGE3i1gW5oPjcYT](https://gateway.ipfs.cybernode.ai/ipfs/QmQAd2SBwypsz5ZqkYgeSTFLq3peGV9xGE3i1gW5oPjcYT)

-----

## Chainstats

[![chain](https://img.shields.io/badge/Chain-bostrom--testnet--6-success.svg?style=flat-square)](https://github.com/cybercongress/cyberd/blob/master/docs/run_validator.md)
[![block](https://img.shields.io/badge/dynamic/json?color=blue&label=Block%20Height&query=%24.result.sync_info.latest_block_height&url=https://rpc.bostromdev.cybernode.ai/status&style=flat-square)]()
[![negentropy](https://img.shields.io/badge/dynamic/json?color=blue&label=-Entropy&query=%24.result.negentropy&url=https://lcd.bostromdev.cybernode.ai/rank/negentropy&style=flat-square)]()
[![validators](https://img.shields.io/badge/dynamic/json?label=Validators&query=%24.result.validators.length&url=https://rpc.bostromdev.cybernode.ai/validators%3F&style=flat-square)]() 

## How to update from bostrom-testnet-5 to bostrom-testnet-6

If you have your bostrom-testnet-5 node running on our docker container do:

```bash
docker stop bostrom-testnet-5
docker rm bostrom-testnet-5
docker rmi cyberd/cyber:bostrom-testnet-5.1
docker run -d --gpus all --name=bostrom-testnet-6 --restart always -p 26656:26656 -p 26657:26657 -p 1317:1317 -e ALLOW_SEARCH=false -v $HOME/.cyber:/root/.cyber  cyberd/cyber:bostrom-testnet-6
```
This will pull new image and replace genesis and cyber binary to correct versions.

Than you'll have to send create-validator [transaction](https://github.com/cybercongress/go-cyber/blob/bostrom-dev/docs/run_validator.md#send-the-create-validator-transaction).

