# ntgbtminer 

ntgbtminer is a no thrills Bitcoin miner.
It is not performant, but demonstrates basic use of the `getblocktemplate`
protocol for a standalone Bitcoin miner. It has no dependencies outside of
standard Python libraries and a JSON-HTTP connection to your local Bitcoin
daemon.

### Changes :factory:

The following changes has been made w.r.t. to the Bitcoin version of the miner:

* adding Peercoin transaction timestamp
* using [P2PK](https://learnmeabitcoin.com/technical/p2pk) for coinbase transactions instead of [P2PKH](https://learnmeabitcoin.com/technical/p2pkh)
* adding timer for when difficulty gets too low

### Setup :hammer:

To initialize the miner, move into this repo and type the following command:

```sh
RPC_USER=any_username RPC_PASS=any_password RPC_URL="http://127.0.0.1:9904" \
    BLOCK_INTERVAL=600 python3 ntgbtminer.py "<RANDOM_MESSAGE>" "<PUB_KEY>"
```

It is possible to get the public key associated to an address using the `getaddressinfo` command on peercoin-cli.

### References :books:

* Repo forked from: [vsergeev/ntgbtminer](https://github.com/vsergeev/ntgbtminer.git)
