# Chain space-pussy-1 

This chain is live staging testnet of [cyber](https://github.com/cybercongress/go-cyber)

Genesis file: 

```s
https://gateway.ipfs.cybernode.ai/ipfs/QmYe81dBfxgYsVhX1mX4uiLQyu3jx2kJvR6CgytDnFgKzc
```

**[Peers](peers.md)**
**[Endpoints](endpoints.md)**

Run with docker 

```s
docker run -d --gpus all --name=space-p-1 --restart always -p 26756:26756 -p 26657:26657 -p 26660:26660 -p 26317:1317 -p 26990:9090 -e ALLOW_SEARCH=true -v $HOME/.cyber:/root/.cyber  cyberd/cyber:space-pussy-1
```