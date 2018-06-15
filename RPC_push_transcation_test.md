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
{"server_version":"012dc012","chain_id":"cf057bbfb72640471fd910bcb67639c22df9f92470936cddc1ade0e2f2e7dc4f","head_block_num":80666,"last_irreversible_block_num":80665,"last_irreversible_block_id":"00013b19b1fd7aece04b8ea27681dbbcb330b9cbf8d622146668f6678efffa7b","head_block_id":"00013b1a9cc16765f26884a70427f71c720ddd837545e2ae67dce9af838377c8","head_block_time":"2018-06-15T12:37:41","head_block_producer":"eosio","virtual_block_cpu_limit":200000000,"virtual_block_net_limit":1048576000,"block_cpu_limit":199900,"block_net_limit":1048576}
```
head_block_number: 80666
chain_id: cf057bbfb72640471fd910bcb67639c22df9f92470936cddc1ade0e2f2e7dc4f

#3 get block
```
curl http://localhost:8888/v1/chain/get_block -d '{"block_num_or_id":80666}'
```
result
```
{"timestamp":"2018-06-15T12:37:41.500","producer":"eosio","confirmed":0,"previous":"00013b19b1fd7aece04b8ea27681dbbcb330b9cbf8d622146668f6678efffa7b","transaction_mroot":"0000000000000000000000000000000000000000000000000000000000000000","action_mroot":"ef281698af58adbd6f7e5d842c7118fc0db854c0cec0a2a51b777bffcff34236","schedule_version":0,"new_producers":null,"header_extensions":[],"producer_signature":"SIG_K1_KZZyJbHzJMcGbp97gSNpztjwfe5Xi9KSHL95erU8K2UtdFJTLqkdCmdZ2KeQPYECPcj31PWULdPG7cj4iK2EQ6keJryMra","transactions":[],"block_extensions":[],"id":"00013b1a9cc16765f26884a70427f71c720ddd837545e2ae67dce9af838377c8","block_num":80666,"ref_block_prefix":2810472690}
```
timestamp: 2018-06-15T13:37:41.500
ref_block_prefix: 2810472690

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
        "expiration": "2018-06-15T13:37:41.500",
        "max_kcpu_usage": 0,
        "max_net_usage_words": 0,
        "ref_block_num": 80666,
        "ref_block_prefix": 2810472690,
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
    "expiration": "2018-06-15T13:37:41.500",
    "ref_block_num": 80666,
    "ref_block_prefix": 2810472690,
    "scope": ["keintest1", "keintest2"],
    "read_scope": [],
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
  "cf057bbfb72640471fd910bcb67639c22df9f92470936cddc1ade0e2f2e7dc4f"
]'
```
result
```
{"expiration":"2018-06-15T13:37:41","ref_block_num":15130,"ref_block_prefix":2810472690,"max_net_usage_words":0,"max_cpu_usage_ms":0,"delay_sec":0,"context_free_actions":[],"actions":[{"account":"eos.token","name":"transfer","authorization":[{"actor":"keintest1","permission":"active"}],"data":"00000819ab3c9d8200001019ab3c9d8210ada2040000000004454f530000000003525043"}],"transaction_extensions":[],"signatures":["SIG_K1_JwP6znVRZh6yMMV9auKioLfs9H1ZLAtL35g99uV5VdJojCuE2UTP5vTJrpp4yeDEH5P3Wiew4cVG3dtA6hjmWGYz4LpALx"],"context_free_data":[]}
```
signatures: SIG_K1_JwP6znVRZh6yMMV9auKioLfs9H1ZLAtL35g99uV5VdJojCuE2UTP5vTJrpp4yeDEH5P3Wiew4cVG3dtA6hjmWGYz4LpALx

#7 push_transaction
```
curl http://localhost:8888/v1/chain/push_transaction -d '{
  "compression": "none",
  "transaction": {
  "expiration": "2018-06-15T13:37:41",
  "ref_block_num": 15130,
  "ref_block_prefix": 2810472690,
  "context_free_actions": [],
  "max_net_usage_words": 0,
  "max_cpu_usage_ms": 0,
  "delay_sec": 0,
  "actions": [{
    "account": "eos.token",
    "name": "transfer",
    "authorization": [
      {
        "actor": "keintest1",
        "permission": "active"
      }
      ],
      "data": "00000819ab3c9d8200001019ab3c9d8210ada2040000000004454f530000000003525043"}],
      "transaction_extensions": []
    },
  "signatures": ["SIG_K1_JwP6znVRZh6yMMV9auKioLfs9H1ZLAtL35g99uV5VdJojCuE2UTP5vTJrpp4yeDEH5P3Wiew4cVG3dtA6hjmWGYz4LpALx"]
}'
```

result 
```
{"transaction_id":"bc0d8490b5e2ba0c5934c3cfff45e18756d3cf74e8150551276d9b9f9dc094ba","processed":{"id":"bc0d8490b5e2ba0c5934c3cfff45e18756d3cf74e8150551276d9b9f9dc094ba","receipt":{"status":"executed","cpu_usage_us":587,"net_usage_words":16},"elapsed":4680,"net_usage":128,"scheduled":false,"action_traces":[{"receipt":{"receiver":"eos.token","act_digest":"ac80d66adcbc40d13b45371139dcf6e72d6faab6beb6d4cd25e4d76ab7af8afa","global_sequence":81636,"recv_sequence":5,"auth_sequence":[["keintest1",10]],"code_sequence":1,"abi_sequence":1},"act":{"account":"eos.token","name":"transfer","authorization":[{"actor":"keintest1","permission":"active"}],"data":{"from":"keintest1","to":"keintest2","quantity":"7777.0000 EOS","memo":"RPC"},"hex_data":"00000819ab3c9d8200001019ab3c9d8210ada2040000000004454f530000000003525043"},"elapsed":4534,"cpu_usage":0,"console":"","total_cpu_usage":0,"trx_id":"bc0d8490b5e2ba0c5934c3cfff45e18756d3cf74e8150551276d9b9f9dc094ba","inline_traces":[{"receipt":{"receiver":"keintest1","act_digest":"ac80d66adcbc40d13b45371139dcf6e72d6faab6beb6d4cd25e4d76ab7af8afa","global_sequence":81637,"recv_sequence":6,"auth_sequence":[["keintest1",11]],"code_sequence":1,"abi_sequence":1},"act":{"account":"eos.token","name":"transfer","authorization":[{"actor":"keintest1","permission":"active"}],"data":{"from":"keintest1","to":"keintest2","quantity":"7777.0000 EOS","memo":"RPC"},"hex_data":"00000819ab3c9d8200001019ab3c9d8210ada2040000000004454f530000000003525043"},"elapsed":3,"cpu_usage":0,"console":"","total_cpu_usage":0,"trx_id":"bc0d8490b5e2ba0c5934c3cfff45e18756d3cf74e8150551276d9b9f9dc094ba","inline_traces":[]},{"receipt":{"receiver":"keintest2","act_digest":"ac80d66adcbc40d13b45371139dcf6e72d6faab6beb6d4cd25e4d76ab7af8afa","global_sequence":81638,"recv_sequence":4,"auth_sequence":[["keintest1",12]],"code_sequence":1,"abi_sequence":1},"act":{"account":"eos.token","name":"transfer","authorization":[{"actor":"keintest1","permission":"active"}],"data":{"from":"keintest1","to":"keintest2","quantity":"7777.0000 EOS","memo":"RPC"},"hex_data":"00000819ab3c9d8200001019ab3c9d8210ada2040000000004454f530000000003525043"},"elapsed":2,"cpu_usage":0,"console":"","total_cpu_usage":0,"trx_id":"bc0d8490b5e2ba0c5934c3cfff45e18756d3cf74e8150551276d9b9f9dc094ba","inline_traces":[]}]}],"except":null}}
```
