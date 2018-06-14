#1 json to bin
```
curl http://localhost:8888/v1/chain/abi_json_to_bin -d '{"code": "eos.token","action": "transfer", "args": {"from":"keintest1","to":"keintest2","quantity":"7777.0000 EOS","memo":"RPC"}}'
```
result
```
{"binargs":"00000819ab3c9d8200001019ab3c9d8210ada2040000000004454f530000000003525043"}
```

#2 get info
```
curl http://localhost:8888/v1/chain/get_info
```
result
```
{"server_version":"012dc012","chain_id":"cf057bbfb72640471fd910bcb67639c22df9f92470936cddc1ade0e2f2e7dc4f","head_block_num":70335,"last_irreversible_block_num":70334,"last_irreversible_block_id":"000112be188abb416e77a5875cb646748da417fb4a53b76917efe9de157d660d","head_block_id":"000112bf38c3d8ab054c1a9ea1b5d8bb861e38fb7e4e9d921ee718ddb1d59af6","head_block_time":"2018-06-14T18:12:45","head_block_producer":"eosio","virtual_block_cpu_limit":200000000,"virtual_block_net_limit":1048576000,"block_cpu_limit":199900,"block_net_limit":1048576}
```
head_block_number: 70335

#3 get block
```
curl http://localhost:8888/v1/chain/get_block -d '{"block_num_or_id":70335}'
```
result
```
{"timestamp":"2018-06-14T18:12:45.500","producer":"eosio","confirmed":0,"previous":"000112be188abb416e77a5875cb646748da417fb4a53b76917efe9de157d660d","transaction_mroot":"0000000000000000000000000000000000000000000000000000000000000000","action_mroot":"ca4a65f73dedd317698cc0c344207b4292d0f3ec97cc4f1932cae4ac13408de3","schedule_version":0,"new_producers":null,"header_extensions":[],"producer_signature":"SIG_K1_JuNrHanhjvBbh5QiPQCmTexhH4dSGbYqwUR8hbQXqC6pLRjSCrxzosRMZKPDrisxgqghJLGNH54fuZLbxhXVAeejjiQxjZ","transactions":[],"block_extensions":[],"id":"000112bf38c3d8ab054c1a9ea1b5d8bb861e38fb7e4e9d921ee718ddb1d59af6","block_num":70335,"ref_block_prefix":2652523525}
```
timestamp: 2018-06-14T18:12:45.500
ref_block_prefix: 2652523525

#4 unlock Wallet
```
curl http://localhost:8888/v1/wallet/unlock -d '["default", "PW5KDynKoH8aj3vGD3UsrKcc66QoBA3TXz9fH5PKNHM7ZWvEweH72"]'
```

#5 get_required_keys
```
curl http://localhost:8888/v1/chain/get_required_keys -d '{
    "available_keys": [
        "EOS8KeP92hNe7tv1JTSJuk1TuSTnHGWWH3SgaF7bdBeLdtfDx8nsy",
        "EOS69Zb6ogiCCJZ7B2ckCNEsQepouteZd4edo6wESbj2FEcGTxwgr",
        "EOS6MRyAjQq8ud7hVNYcfnVPJqcVpscN5So8BhtHuGYqET5GDW5CV"
    ],
    "transaction": {
        "actions": [
            {
                "account": "eos.token",
                "authorization": [
                    {
                        "actor": "keintest1",
                        "permission": "active"
                    }
                ],
                "data": "00000819ab3c9d8200001019ab3c9d8210ada2040000000004454f530000000003525043",
                "name": "transfer"
            }
        ],
        "context_free_actions": [
        ],
        "context_free_data": [
        ],
        "delay_sec": 0,
        "expiration": "2018-06-14T19:12:45.500",
        "max_kcpu_usage": 0,
        "max_net_usage_words": 0,
        "ref_block_num": 70335,
        "ref_block_prefix": 2652523525,
        "signatures": [
        ]
    }
}'
```
result
```
{"required_keys":["EOS8KeP92hNe7tv1JTSJuk1TuSTnHGWWH3SgaF7bdBeLdtfDx8nsy"]}
```

#6 sign_transaction
```
curl http://localhost:8888/v1/wallet/sign_transaction -d '[
  {
    "ref_block_num": 70335,
    "ref_block_prefix": 2652523525,
    "expiration": "2018-06-14T19:12:45.500",
    "actions": [
      {
        "account": "eos.token",
        "name": "transfer",
        "authorization": [
          {
            "actor": "keintest1",
            "permission": "active"
          }
        ],
        "data": "00000819ab3c9d8200001019ab3c9d8210ada2040000000004454f530000000003525043"
      }
    ],
    "signatures": []
  },
  [
    "EOS8KeP92hNe7tv1JTSJuk1TuSTnHGWWH3SgaF7bdBeLdtfDx8nsy"
  ],
  ""
]'
```
result
```
{"expiration":"2018-06-14T19:12:45","ref_block_num":4799,"ref_block_prefix":2652523525,"max_net_usage_words":0,"max_cpu_usage_ms":0,"delay_sec":0,"context_free_actions":[],"actions":[{"account":"eos.token","name":"transfer","authorization":[{"actor":"keintest1","permission":"active"}],"data":"00000819ab3c9d8200001019ab3c9d8210ada2040000000004454f530000000003525043"}],"transaction_extensions":[],"signatures":["SIG_K1_JybSXSJTSwVie9j85XGvtmJSBFDURiKTYYRrPTZJ6QmXpS6VsvgGtJrjA9J8oyPSQND56wSMzrU25QcAf59ASrZmbzuyLE"],"context_free_data":[]}
```
signatures: SIG_K1_JybSXSJTSwVie9j85XGvtmJSBFDURiKTYYRrPTZJ6QmXpS6VsvgGtJrjA9J8oyPSQND56wSMzrU25QcAf59ASrZmbzuyLE

#7 push_transaction
```
curl http://localhost:8888/v1/chain/push_transaction -d '{
  "compression": "none",
  "transaction": {
    "expiration": "2018-06-14T18:58:06.500",
    "ref_block_num": 4799,
    "ref_block_prefix": 2652523525,
    "context_free_actions": [],
    "actions": [
        {
            "account": "eos.token",
            "name": "transfer",
            "authorization": [
                {
                    "actor": "keintest1",
                    "permission": "active"
                }
            ],
            "data": "00000819ab3c9d8200001019ab3c9d8250c300000000000004454f530000000003525043"
        }
    ],
    "transaction_extensions": []
  },
  "signatures": [
        "SIG_K1_JybSXSJTSwVie9j85XGvtmJSBFDURiKTYYRrPTZJ6QmXpS6VsvgGtJrjA9J8oyPSQND56wSMzrU25QcAf59ASrZmbzuyLE"
   ]
}'
```

result Failed
```
{"code":500,"message":"Internal Service Error","error":{"code":3090003,"name":"unsatisfied_authorization","what":"provided keys, permissions, and delays do not satisfy declared authorizations","details":[{"message":"transaction declares authority '{\"actor\":\"keintest1\",\"permission\":\"active\"}', but does not have signatures for it under a provided delay of 0 ms, provided permissions [], and provided keys [\"EOS6LtXznHeMS8fSMw5Dfn8KHHpjQmo49bNt8fo9SBHHUS8Lsvsj3\"]","file":"authorization_manager.cpp","line_number":409,"method":"check_authorization"}]}}
```
