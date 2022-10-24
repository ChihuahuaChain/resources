# ChihuahuaChain Restart (3rd Attempt)
## ⚠️ DRAFT ONLY - PREPARE AND DON'T START THE VALIDATOR YET ⚠️


### We are going to restart the network with v3.0.0 (no burning mechanism)

### In order for the chain to sucessfully restart we ask you to STRICTLY FOLLOW this tutorial, failure do to so will result in a failure to resume the block production.

# !!! Before beginning make sure the node is HALTED !!!


## Download & upgrade go to the latest version
```bash
wget https://go.dev/dl/go1.19.2.linux-amd64.tar.gz

sudo rm -rf /usr/local/go && sudo tar -C /usr/local -xzf go1.19.2.linux-amd64.tar.gz

go version
# the output should be
# go version go1.19.2 linux/amd64
```

## Backup your priv_validator_state.json
⚠️ Failure to do will most likely result in your node double-signing and being jailed forever (tombstoned) ⚠️

### In case you need a fresh snapshot you can download it from
 - [Mirror #2](http://65.21.131.216/new_snapshot.tar.gz)

⚠️ Don't forget to Backup your ~/.chihuahuad/data/priv_validator_state.json file before replacing your data dir with the snapshot and place the file back before starting the validator.


```bash

cp ~/.chihuahuad/data/priv_validator_state.json ~/

diff -s ~/.chihuahuad/data/priv_validator_state.json ~/priv_validator_state.json

# the output should be
# Files .../data/priv_validator_state.json and /home/chihuahua/priv_validator_state.json are identical
```
## Installing v3.0.0
```bash
cd ~/chihuahua

git fetch --all

git checkout v3.0.0

make install

chihuahuad version --long |grep commit

# the output should be
# commit: 36ee9133360dadfe8f96527442908407fd04abb7

```
## If you are using Cosmovisor

```bash
rm ~/.chihuahuad/cosmovisor/upgrades/burnmech/bin/chihuahuad

cp ~/go/bin/chihuahuad ~/.chihuahuad/cosmovisor/upgrades/burnmech/bin/chihuahuad

~/.chihuahuad/cosmovisor/upgrades/burnmech/bin/chihuahuad version --long

# the output should be
# commit: 36ee9133360dadfe8f96527442908407fd04abb7
```

## Manually edit the app.toml file
⚠️ It is very important that you <b>VERIFY and ADD THESE LINES</b> at the end of the app.toml file
```bash
# IAVLDisableFastNode enables or disables the fast node feature of IAVL.
# Default is true.
iavl-disable-fastnode = false
```
⚠️ Verify that the pruning is set to "nothing" (We want to be extra safe and we will change it back to custom if needed after the chain resumes)

```bash
# default: the last 100 states are kept in addition to every 500th state; pruning at 10 block intervals
# nothing: all historic states will be saved, nothing will be deleted (i.e. archiving node)
# everything: all saved states will be deleted, storing only the current state; pruning at 10 block intervals
# custom: allow pruning options to be manually specified through 'pruning-keep-recent', 'pruning-keep-every', and 'pruning-interval'
pruning = "nothing"
```

## !!! Before restarting your node !!!

### Fill [this Google Sheet form](https://docs.google.com/spreadsheets/d/1kPSfn916Jp2VyQTqguy1oM179gtvUzLI0m-ub666rvQ/edit#gid=1571541180) and make sure every row on your validator is GREEN and WAIT OUR INSTRUCTION BEFORE STARTING THE VALIDATOR!
### If that's not the case reach out to the #priv-validators channel on Discord and you will find support
### This is not a race to see who makes it first, take your time to verify everything 10 times before restarting.

