# eosio tutorial for MAC

* non Producing-node

## 1. config.ini

```
vim ~/Library/Application Support/eosio/nodeos/config/config.ini

producer-name = eosio
plugin = eosio::http_plugin
plugin = eosio::wallet_api_plugin
plugin = eosio::chain_api_plugin
```

## 2. nodeos

```
./nodeos -e -p eosio 
```

```
Command Line Options for eosio::chain_plugin:
    --fix-reversible-blocks               recovers reversible block database if 
                                          that database is in a bad state
    --force-all-checks                    do not skip any checks that can be 
                                          skipped while replaying irreversible 
                                          blocks
    --replay-blockchain                   clear chain state database and replay 
                                          all blocks
    --hard-replay-blockchain              clear chain state database, recover as 
                                          many blocks as possible from the block 
                                          log, and then replay those blocks
    --delete-all-blocks                   clear chain state database and block 
                                          log
```

## 3. rpc
...ㅇㅓ.. create wallet 을  RPC로 날리면 JSON error가 떨어지는데 왜지?...
