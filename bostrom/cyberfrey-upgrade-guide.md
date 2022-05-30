# How to prepare your node for Cyberfrey upgrade

This guide will include all the steps you need to make to get ready for `cyberfrey` upgrade in Bostrom.

Hereby we assume that you run your node in docker with cyber ["official"](https://hub.docker.com/layers/cyber/cyberd/cyber/bostrom-1/images/sha256-6383de3e4562690907b0dbb99b752f53ef2d41f44a7d452a903d24397e49911b?context=explore) image, otherwise this giude will not siute your node. 

## Step 1: Pull new docker image

New cyber binary is wrapped in new docker image, so we have to pull it first: 

```js
docker pull cyberd/cyber:bostrom-2
```
It may take few minutes to pull new image, when done check that you have it with: 

```js
docker images
```

## Step 2: Replace docker image for bostrom container

*In this step you will have to operate fast to reduce your node downtime, so please read all the sub-steps first!*

Stop your current docker container with bostrom: 

```js
docker stop bostrom
```

Remove bostrom container (do not worry, files will stay untouched):

```js
docker rm bostrom
```

Create bostrom container from new image (note: if you have custom ports set, please adjust accordingly): 

```sh
docker run -d --gpus all --name=bostrom --restart always -p 26656:26656 -p 26657:26657 -p 1317:1317 -e ALLOW_SEARCH=true -v $HOME/.cyber:/root/.cyber  cyberd/cyber:bostrom-2
```

Check logs, block production should restore after start:

```sh
docker logs bostrom -f --tail 20 
```

## Step 3: Verify that everything is OK

After container lauch new cyber binary should appear inside `$HOME/.cyber/cosmovisor/` folder. Check that you have similar folder layout: 

```sh
cd $HOME/.cyber/cosmovisor/
tree
```

You should have similar layout of filed and folders:

```sh
root@node:~/.cyber/cosmovisor# tree
.
├── current -> /root/.cyber/cosmovisor/genesis/bin
├── genesis
│   └── bin
│       └── cyber
└── upgrades
    └── cyberfrey
        └── bin
            └── cyber


6 directories, 2 files
```

## You done! What's next? 

Now it's a good time to go and vote for prop #7, if you havent do this yet, report that you prepared for the upgrade in our [Hall of Fame](https://t.me/fameofcyber) and chill utill the upgrade block 3098000 which should come arount 9:00am UTC Friday 03.06.2022 ( proposal says 04.06.2022 but that's incorrect). 
Also you may track timer until upgrade at `cybernode.ai`, actuall block time is used there so estimate is more or less correct.

What will happen at the block 3098000: 

- chain will halt with message `CONSENSUS FAILURE!!! err="UPGRADE \"cyberfrey\" NEEDED at height: 3098000:`
- cosmovisor inside container will catch this event and change symlink inside `.cyber/cosmovisor/` folder
- node will start and as soon as 66%+ of voting power is online blocks will resume

## Crisis protocol 

Process of upgrade should go pretty smooth and should not require any direct action, but in case if something will go wrong cyber devs may concider certain ways to recover. Just check up your node at the time of the upgrade and check  [Hall of Fame](https://t.me/fameofcyber) chat for possible coordination. 