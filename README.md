# Tempura mining

### Option 1: ntgbtminer

ntgbtminer is a no thrills
[getblocktemplate](https://en.bitcoin.it/wiki/Getblocktemplate) Bitcoin miner.
It is not performant, but demonstrates basic use of the getblocktemplate
protocol for a standalone Bitcoin miner. It has no dependencies outside of
standard Python libraries and a JSON-HTTP connection to your local Bitcoin
daemon.

The following changes has been made w.r.t. to the Bitcoin version of the miner:

* adding Peercoin transaction timestamp
* using P2PK for coinbase transactions instead of P2PKH like in Peercoin coinbase blocks
* adding empty block signature at the end of the block to avoid "Block decode failed" error from peercoind

Forked from: [vsergeev/ntgbtminer](https://github.com/vsergeev/ntgbtminer.git)

To initialize the miner, move into this repo and type the following command:

```sh
RPC_USER=any_username RPC_PASS=any_password RPC_URL="http://127.0.0.1:9904" \
    python3 ntgbtminer.py "Random useless message" \
    "03ee5e86bad451416d8be66c4c08e980fc90d5003e4bc5026026e295f039fb9064"
```

where the last parameter is the public key and not the address.

### Option 2: generatetoaddress command

A simple alternative to start mining is the following commmand for bitcoin-cli, that triggers a simple CPU miner and successfully mines blocks in regtest mode and testnet (not tried in mainnet):

```sh
peercoin-cli generatetoaddress <N_OF_BLOCKS> <ADDR_TO_GET_REWARD>
```

### Block with single coibase transaction

The following is the structure of any Bitcoin/Peercoin block (block 3 in Peercoin Testnet):

Block structure | Hex | Bytes
------- | --------- | ------
Version | 01000000 | 4
Previous block hash | 6c5fa7bf58277ca33ee5c459b7e2a7a30df7a71c0f54b2c96931861205000000 | 32
Merkle root | e04b48748c03f27c98d94f8e45f0e25e34e29dce8feaf4cdb15b5472f042e850 | 32
Timestamp | 19cc3a50 | 4
Difficulty | 41fc071d | 4
Nonce | 2d25990b | 4
N. of transactions | 01 | needed
Transactions | single_coinbase_transaction | needed
Signature size | 23 | needed
Block signature | 304502205e76ed4e6d5e54771a750116968b79bc390d55af04 d0fd88a4cc7ce12129fa2b022100aa7cb078d805bfa8ac7563a5 bd7645808516be69972da0f375dbeaf968ba1a09 | needed


A block can be obtained by running this command: 

```
peercoin-cli getblock $(peercoin-cli getblockhash <BLOCK_HEIGHT>) <VERBOSITY>
```

with verbosity set to 0 if you want the hexadecimal version of the block.

The following is the coinbase transaction contained in the block described above:

Coinbase structure | Hex | Bytes
------- | --------- | ------
**Version** | 01000000 | 4
**Timestamp** (Peercoin only) | f9c83a50 | 4
**N. of inputs** | 01 | needed
Unspent transaction ID (null) | 0000000000000000000000000000000000000000000000000000000000000000 | 32
Selected output (max value) | ffffffff | 4
Script sig size | 0e | needed
Script sig (random data) | 04f9c83a500101062f503253482f | needed
Sequence | ffffffff | 4
**N. of outputs** | 01 | needed
Output amount | c022eff401000000 | 8
Script pub key size | 23 | needed
Script pub key (P2PK) | 21033745c638d520c6cd46c5fbdb319dfe6d8df5f83431d8b3997f7b097bfdfae2eeac | needed
**Locktime** | 00000000 | 4


### References

* [Bitcoin official docs](https://developer.bitcoin.org/reference/index.html)
* [learnmeabitcoin.com - Bitcoin technical guide](https://learnmeabitcoin.com/technical/)


