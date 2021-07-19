# ntgbtminer

ntgbtminer is a no thrills
[getblocktemplate](https://en.bitcoin.it/wiki/Getblocktemplate) Bitcoin miner.
It is not performant, but demonstrates basic use of the getblocktemplate
protocol for a standalone Bitcoin miner. It has no dependencies outside of
standard Python libraries and a JSON-HTTP connection to your local Bitcoin
daemon.

### Changes

* adding Peercoin transaction timestamp
* using P2PK for coinbase transactions instead of P2PKH
* adding empty block signature at the end of the block to avoid "Block decode failed" error from peercoind

Forked from: [vsergeev/ntgbtminer](https://github.com/vsergeev/ntgbtminer.git)

### Setup miner

```sh
RPC_USER=any_username RPC_PASS=any_password RPC_URL="http://127.0.0.1:9904" \
    python3 ntgbtminer.py "Random coinbase message" \
    "03ee5e86bad451416d8be66c4c08e980fc90d5003e4bc5026026e295f039fb9064"
```

### Block structure

The following is the structure of any Bitcoin/Peercoin block (block 3 in Peercoin Testnet):

Block structure | Hex | Bytes
------- | --------- | ------
Version | 01000000 | 4
Previous block hash | 6c5fa7bf58277ca33ee5c459b7e2a7a30df7a71c0f54b2c96931861205000000 | 32
Merkle root | e04b48748c03f27c98d94f8e45f0e25e34e29dce8feaf4cdb15b5472f042e850 | 32
Timestamp | 19cc3a50 | 4
Difficulty | 41fc071d | 4
Nonce | 2d25990b | 4
N. of transactions | 01 | -
Transactions | coinbase_transaction | -
Signature length | 23 | -
Block signature | 304502205e76ed4e6d5e54771a750116968b79bc390d55af04d0fd88a4cc7ce12129fa2b022100aa7cb078d805bfa8ac7563a5bd7645808516be69972da0f375dbeaf968ba1a09 | -


A block can be obtained by running this command: 

```
peercoin-cli getblock $(peercoin-cli getblockhash <BLOCK_HEIGHT>) <VERBOSITY>
```

with verbosity set to 0 if you want the hexadecimal version of the block.

### References

* [How to create a Docker Image](https://www.linux.com/training-tutorials/how-create-docker-image/?utm_source=pocket_mylist)
* [How to share Docker Images with others](https://www.cloudsavvyit.com/12326/how-to-share-docker-images-with-others/?utm_source=pocket_mylist)


