Last updated for v1.2.0.

This guide assumes you have already Startup a hyperexchange witness-node using [HyperExchange Witness-node Setup](/wallets/hxnode-setup.md) and a cli-wallet using [Cli-wallet Startup](/wallets/hxwallet-cli.md).

The following will introduce how to use rpc commands to call functions:transfer accounts/deposit/withdrawal/Funds transfer.(Use BTC transfer to LTC as a sample)

---

## Preparatory Work

1.Create two hx accounts(one to bind with BTC,the other one bind with LTC).Please make sure wallet is unlocked.
    
    unlocked >>> wallet_create_account hxtest001
    wallet_create_account hxtest001
    1168399ms th_a   wallet.cpp:1082   save_wallet_file ] saving wallet to file wallet.json
    "HXNUZSB27eoKGki79mioGrS5YyKxdXEzvQu"
    
    unlocked >>> wallet_create_account hxtest002
    wallet_create_account hxtest002
    1680829ms th_a   wallet.cpp:1082   save_wallet_file ] saving wallet to file wallet.json
    "HX8Vx4U1HfPBhHQF8J2z55qyiMCaJBce5gQ"
    
2.Create a BTC address and a LTC address.

    unlocked >>> create_crosschain_symbol BTC
    create_crosschain_symbol BTC
    { "jsonrpc": "2.0", "id" : "45","method" : "Zchain.Addr.importAddr" ,"params" : {"chainId":"btc" ,"addr": "19QmVye31e2QfYXZShBD2VXissoM6QeppM"}}
    1304280ms th_a   wallet.cpp:1082   save_wallet_file ] saving wallet to file wallet.json
    {
      "addr": "19QmVye31e2QfYXZShBD2VXissoM6QeppM",
      "pubkey": "0244d2c2cea8d2324096a0fd2df9d4cc38e4db9e61a896b23fa0ba21d69c274a28",
      "wif_key": "L3tL4hhs1mCFjj6zJqJqF6qPpxZvmSm7cHzakMfTmq8MWBDEfBPJ"
    }
    unlocked >>> create_crosschain_symbol LTC
    create_crosschain_symbol LTC
    { "jsonrpc": "2.0", "id" : "45","method" : "Zchain.Addr.importAddr" ,"params" : {"chainId":"ltc" ,"addr": "LPFnwvJFXziSzk35fXn3tj2JYQe4iHLLY8"}}
    1688432ms th_a   wallet.cpp:1082   save_wallet_file ] saving wallet to file wallet.json
    {
      "addr": "LPFnwvJFXziSzk35fXn3tj2JYQe4iHLLY8",
      "pubkey": "0201115d04f29783acab2ce61fefd5e71678f3b99a1bb029e59600da1b67806b29",
      "wif_key": "T4GPU51McSfjJFtD8NKWnJj1qDWtef2452SjvMvsnqexcs7odn6E"
    }

3.Bind `hxtest001` to created BTC address,bind `hxtest002` to created LTC address.

    unlocked >>> bind_tunnel_account hxtest001 19QmVye31e2QfYXZShBD2VXissoM6QeppM BTC true
    bind_tunnel_account hxtest001 19QmVye31e2QfYXZShBD2VXissoM6QeppM BTC true
    {
      "ref_block_num": 633,
      "ref_block_prefix": 3017921153,
      "expiration": "2018-09-05T06:44:05",
      "operations": [[
      10,{
    "fee": {
      "amount": 0,
      "asset_id": "1.3.0"
    },
    "crosschain_type": "BTC",
    "addr": "HXNUZSB27eoKGki79mioGrS5YyKxdXEzvQu",
    "account_signature": "2002cc5bcd46ef8359e7fd4383fad68b5e583aa57c3a3e0e79d045af54f161aa334f370531646cb48d783005bec6306c63ef7f1fd4b1e3f9f4d16ec8c7964682b9",
    "tunnel_address": "19QmVye31e2QfYXZShBD2VXissoM6QeppM",
    "tunnel_signature": "HyLo47ghpBGKoWzmhzz5urzJ3WlFSoq2beHtrFwBDOpIeDfqWs+7sP8aNRhwztMboi2CjubDsz8dWoPJ0ABwtzc="
      }
    ]
      ],
      "extensions": [],
      "signatures": [
    "1f4eb80b086c2598621bfa2463913ed061d05825302c320db600fad3aec2f5f5c70e76e3056f2cc29a44efeaa81a7f8c42fee277a391e68926f5cdc39e83be90d7"
      ],
      "block_num": 0,
      "trxid": "0cfffec187b994fc6a4f2ff6b5cdadff17fd2c7c"
    }
    
    unlocked >>> bind_tunnel_account hxtest002 LPFnwvJFXziSzk35fXn3tj2JYQe4iHLLY8 LTC true
    bind_tunnel_account hxtest002 LPFnwvJFXziSzk35fXn3tj2JYQe4iHLLY8 LTC true
    {
      "ref_block_num": 644,
      "ref_block_prefix": 1864335149,
      "expiration": "2018-09-05T06:45:00",
      "operations": [[
      10,{
    "fee": {
      "amount": 0,
      "asset_id": "1.3.0"
    },
    "crosschain_type": "LTC",
    "addr": "HX8Vx4U1HfPBhHQF8J2z55qyiMCaJBce5gQ",
    "account_signature": "1f415f619420ec932059322b6a306f9a250309386e9ac8f7d5f1bc511d6ec440e93cf8408e3bb1ea2097d2a11e097a8e76c48354b86379b963191426819f6e6639",
    "tunnel_address": "LPFnwvJFXziSzk35fXn3tj2JYQe4iHLLY8",
    "tunnel_signature": "HydULKgPGMRuRyTLDGjqZCGFkNeSUXU99cRKRK+CxxakGmnA773SkWz8kF6jPwxqKpG0IxpBi5OuO5C4jsXTQrE="
      }
    ]
      ],
      "extensions": [],
      "signatures": [
    "1f060d204b74d7ea171af75cdb4635ac4b510dc4d3416e71ebfc87017961aa09d24e0388a80b8016c2ed7c4f77d391131b81245909d991c29818fcfd8b82fe6f62"
      ],
      "block_num": 0,
      "trxid": "47a0ab550387694d3d5c9068723b44f7954b9281"
    }

4.Query bind result.

    get_binding_account hxtest001 BTC
    [{
    "id": "2.6.0",
    "owner": "HXNUZSB27eoKGki79mioGrS5YyKxdXEzvQu",
    "chain_type": "BTC",
    "bind_account": "19QmVye31e2QfYXZShBD2VXissoM6QeppM"
      }
    ]
    unlocked >>> get_binding_account hxtest002 LTC
    get_binding_account hxtest002 LTC
    [{
    "id": "2.6.1",
    "owner": "HX8Vx4U1HfPBhHQF8J2z55qyiMCaJBce5gQ",
    "chain_type": "LTC",
    "bind_account": "LPFnwvJFXziSzk35fXn3tj2JYQe4iHLLY8"
      }
    ]
5.Import private of BTC and LTC addresses to each other' main blockchain.

## Deposit

> Deposit BTC to account `hxtest001`

1.Make sure created BTC address' balance is not 0 on bitcoin chain.

2.Create BTC asset on hx blockchain,if you want to create asset by senator,please import private key of senator.

    unlocked >>> import_key guard0 5JZe9Hv7twngWSEZzvvvDXP5RG1LJGixSz6WJ4D8te9x45kvDuG
    import_key guard0 5JZe9Hv7twngWSEZzvvvDXP5RG1LJGixSz6WJ4D8te9x45kvDuG
    297029ms th_a   wallet.cpp:532copy_wallet_file ] backing up wallet wallet.json to before-import-key-2856e806.wallet
    297035ms th_a   wallet.cpp:1082   save_wallet_file ] saving wallet to file wallet.json
    297040ms th_a   wallet.cpp:532copy_wallet_file ] backing up wallet wallet.json to after-import-key-2856e806.wallet
    true
    unlocked >>> wallet_create_asset  guard0 BTC 8 210000000 100000  true
    wallet_create_asset  guard0 BTC 8 210000000 100000  true
    {
      "ref_block_num": 1010,
      "ref_block_prefix": 370048593,
      "expiration": "2018-09-05T07:17:00",
      "operations": [[
      75,{
    "fee": {
      "amount": 0,
      "asset_id": "1.3.0"
    },
    "issuer": "1.2.31",
    "symbol": "BTC",
    "issuer_addr": "HXdXPBLRsiUCY1VxcDd4gGrkDcgCV3Jegb",
    "precision": 8,
    "max_supply": 210000000,
    "core_fee_paid": 100000,
    "extensions": []
      }
    ]
      ],
      "extensions": [],
      "signatures": [
    "1f3a0a45c790ea62faa785e94c62cd4c7df2b4eaea51b6762cceb09c5b47c23a6e644af6447ba293e023290f40ec90eede0e4fbd723e05526456fcbb18695e3d87"],
      "block_num": 0,
      "trxid": "6c618b152d4ce1f707e9d07ab834fd19e90bf2ad"
    }
    

2.Update all senators on hx blockchain,after update,system wil create a new BTC hot-cold multisign address.

    unlocked >>> update_asset_private_keys  guard0 BTC true
    unlocked >>> update_asset_private_keys  guard1 BTC true
    unlocked >>> update_asset_private_keys  guard2 BTC true
    unlocked >>> update_asset_private_keys  guard3 BTC true
    unlocked >>> update_asset_private_keys  guard4 BTC true
    unlocked >>> update_asset_private_keys  guard5 BTC true
    unlocked >>> update_asset_private_keys  guard6 BTC true

3.Query hot-cold multisign address.

    unlocked >>> get_multisig_account_pair BTC
    get_multisig_account_pair BTC
    [{
    "id": "2.7.1",
    "chain_type": "BTC",
    "bind_account_hot": "35ymUk9NfK4izhgp55Nphqd6dcgsvQYNfd",
    "redeemScript_hot": "552103e995f361c3267fc3ef15f6c7bbe358d001e92b5768bad416c3ab468e468fe81f210340b554f366427ae07c6ab183da60b8b1cfa90ebc9bf359dfd3e4ea27cced1ac621026d6d3b26619db0c10b36a7261050e4837a9f11955b96628a6178d33c6f1b7018210397551 6fea5a5ca3f9e22d391418013b59e8c4656c62f848b5ad5fdcc50d3a223210283889e1a8391d1459d654f95b8ab3911495045b5afbe2d53ad3ffd9447317bbd2103987d03bb424201a2aee083d5880d53042e47df25419dad0fe2e5b4acd6b181362103a0e353866a3e079479fd7e23f3e70965c5da2b7f740ffb9f6f32968c8f58655157ae",
    "bind_account_cold": "3LDA7iK8N1er3SZRNb5qKxK8WksVVtwCnf",
    "redeemScript_cold": "55210306a1c20bb3e6cfcf1c5dacb2395eac062108f62112ba6e1aa77f569012b08a252102c4c281dd603685082cfc3f7b1ea7d27da941465dcb4d655d664c7d9d4a56d57d21023e1bebbd52c2e54f8b1d1fa5f37f01c9c6698679dacf1c21d068340fab41dc7c210366f8574f741ff635b179e25a403820d0bc629724a4dcc31cb6bea40d0396336e2103728d3228395e284a1eb90e4a0d20ffde72ca8793f9c7e9abf5f978707686251e21022e7fc9b4f34cae2b3e4f2a237d18be0694d509893ac31b88a1a8bd33e0404e7721024a70a72d3d02385b267cd08eeac732a6337df883ae132161aeafbe4be1c56c0f57ae",
    "effective_block_num": 0,
    "end_block": 4294967295
      }
    ]

4.Initiate a proposal to enable multiple signature addresses to take effect.

    unlocked >>> account_change_for_crosschain guard0 BTC 35ymUk9NfK4izhgp55Nphqd6dcgsvQYNfd 3LDA7iK8N1er3SZRNb5qKxK8WksVVtwCnf 10000 true

    account_change_for_crosschain guard0 BTC 35ymUk9NfK4izhgp55Nphqd6dcgsvQYNfd 3LDA7iK8N1er3SZRNb5qKxK8WksVVtwCnf 10000 true
    {
      "ref_block_num": 1163,
      "ref_block_prefix": 3100123180,
      "expiration": "2018-09-05T07:30:15",
      "operations": [[
      28,{
    "type": 0,
    "fee": {
      "amount": 0,
      "asset_id": "1.3.0"
    },
    "proposer": "1.2.31",
    "fee_paying_account": "HXdXPBLRsiUCY1VxcDd4gGrkDcgCV3Jegb",
    "expiration_time": "2018-09-05T10:06:55",
    "proposed_ops": [{
    "op": [
      74,{
    "chain_type": "BTC",
    "fee": {
      "amount": 0,
      "asset_id": "1.3.0"
    },
    "cold": "3LDA7iK8N1er3SZRNb5qKxK8WksVVtwCnf",
    "hot": "35ymUk9NfK4izhgp55Nphqd6dcgsvQYNfd"
      }
    ]
      }
    ],
    "extensions": []
      }
    ]
      ],
      "extensions": [],
      "signatures": [
    "1f093250ceada0f52fa5cc1cbeb1831860779b7efa1915d36e37bb6ea7778ae9021da3c355c056ea455a99127a0d5da60ef22c6990b7b254e51d3a01147bedcb8f"
      ],
      "block_num": 0,
      "trxid": "67e0d0e4eafd8905f49e7e040a70da0550d28933"
    }

5.Get proposal id.

    unlocked >>> get_proposal_for_voter guard0
    get_proposal_for_voter guard0
    [{
    "id": "1.10.0",
    "proposer": "1.2.31",
    "expiration_time": "2018-09-05T10:06:55",
    "proposed_transaction": {
      "ref_block_num": 0,
      "ref_block_prefix": 0,
      "expiration": "2018-09-05T10:06:55",
      "operations": [[
      74,{
    "chain_type": "BTC",
    "fee": {
      "amount": 0,
      "asset_id": "1.3.0"
    },
    "cold": "3LDA7iK8N1er3SZRNb5qKxK8WksVVtwCnf",
    "hot": "35ymUk9NfK4izhgp55Nphqd6dcgsvQYNfd"
      }
    ]
      ],
      "extensions": []
    },
    "required_active_approvals": [],
    "available_active_approvals": [],
    "required_owner_approvals": [],
    "available_owner_approvals": [],
    "available_key_approvals": [],
    "approved_key_approvals": [],
    "disapproved_key_approvals": [],
    "required_account_approvals": [
      "HXdXPBLRsiUCY1VxcDd4gGrkDcgCV3Jegb",
      "HX3HmP3gqcDqYvHvVq2Hn44nuUDfSSBMU55",
      "HXC3X3WoKyqNQZDyPN3Pq55gX5sLhVJxZNh",
      "HXGu1qvt9pG55W3CfAETgwDFi2NwvWQGV4y",
      "HXHd49CtDZZW7ySYZNQYaUurZNWW76HBnhU",
      "HXMGFZwHXyiFj1MUwCVMoyzqBJ4CuTC7xpX",
      "HXMkBpQ9nj1hHXwEGQvyZdFiRgRK78ixKPA"
    ],
    "type": "committee"
      }
    ]

6.Approve proposal，more than two-thirds of the senators agreed with the proposal, multiple addresses will to take effect.

    unlocked >>approve_proposal guard0 1.10.0 {"key_approvals_to_add": ["HXC3X3WoKyqNQZDyPN3Pq55gX5sLhVJxZNh", "HXGu1qvt9pG55W3CfAETgwDFi2NwvWQGV4y", "HXMkBpQ9nj1hHXwEGQvyZdFiRgRK78ixKPA", "HXdXPBLRsiUCY1VxcDd4gGrkDcgCV3Jegb", "HXMGFZwHXyiFj1MUwCVMoyzqBJ4CuTC7xpX"]}  true

    approve_proposal guard0 1.10.0 {"key_approvals_to_add": ["HXC3X3WoKyqNQZDyPN3Pq55gX5sLhVJxZNh", "HXGu1qvt9pG55W3CfAETgwDFi2NwvWQGV4y", "HXMkBpQ9nj1hHXwEGQvyZdFi
    RgRK78ixKPA", "HXdXPBLRsiUCY1VxcDd4gGrkDcgCV3Jegb", "HXMGFZwHXyiFj1MUwCVMoyzqBJ4CuTC7xpX"]}  true
    {
      "ref_block_num": 1257,
      "ref_block_prefix": 4294124370,
      "expiration": "2018-09-05T07:38:20",
      "operations": [[
      29,{
    "fee": {
      "amount": 0,
      "asset_id": "1.3.0"
    },
    "fee_paying_account": "HXdXPBLRsiUCY1VxcDd4gGrkDcgCV3Jegb",
    "proposal": "1.10.0",
    "active_approvals_to_add": [],
    "active_approvals_to_remove": [],
    "owner_approvals_to_add": [],
    "owner_approvals_to_remove": [],
    "key_approvals_to_add": [
      "HXdXPBLRsiUCY1VxcDd4gGrkDcgCV3Jegb",
      "HXC3X3WoKyqNQZDyPN3Pq55gX5sLhVJxZNh",
      "HXGu1qvt9pG55W3CfAETgwDFi2NwvWQGV4y",
      "HXMGFZwHXyiFj1MUwCVMoyzqBJ4CuTC7xpX",
      "HXMkBpQ9nj1hHXwEGQvyZdFiRgRK78ixKPA"
    ],
    "key_approvals_to_remove": [],
    "extensions": []
      }
    ]
      ],
      "extensions": [],
      "signatures": [
    "1f3d876dd861648d7ab8f267ccfe6205c7f87b4976658d5bd96b4054493ab99cd6075017b9eef618471d3f17b4c515244cbf06fd9cafb72d56b700a8efb8d1b103",
    "1f3472cd668850ed8b6c2767ac718109bd3287679573070668ef8b95601e1c15cb7afe3be1b8307c864dad369867bd752c72da99f23d16e0e9ba3bb1df58831d7f",
    "1f65613ac4e54416910dfb04a98b88b6a74eeb2f4d9ecac2066b3f15a9741553854f59fd8d6ee899178a08d319944a8bfe90dde125a85f11e1d4544d8f63df460b",
    "2044b1c7933df43f1fcd887c3c845b2f2edd8fdde1d1bfaceb8615ed984989e4af22966fe4d553f478da1b0f7fe6435531cd509a1f6030f4b4361a7892e2fe004b",
    "1f0b5604c4d32a216da8f631734ea56096ed6d9d164c4d8eb462827d2ae7b2772a747808e6eabd951d4bc9eb5aa589f71972398e96dfea80607d12bc6b466ee1ee"
      ],
      "block_num": 0,
      "trxid": "2e5caf913b77cd0416311fe2a35c8f029619d76e"
    }

7.Query multi-sign address,if "effective_block_num" is not 0,means this addres has take effect.

    unlocked >>> get_multisig_account_pair BTC
    get_multisig_account_pair BTC
    [{
    "id": "2.7.1",
    "chain_type": "BTC",
    "bind_account_hot": "35ymUk9NfK4izhgp55Nphqd6dcgsvQYNfd",
    "redeemScript_hot": "552103e995f361c3267fc3ef15f6c7bbe358d001e92b5768bad416c
    3ab468e468fe81f210340b554f366427ae07c6ab183da60b8b1cfa90ebc9bf359dfd3e4ea27cced1
    ac621026d6d3b26619db0c10b36a7261050e4837a9f11955b96628a6178d33c6f1b7018210397551
    6fea5a5ca3f9e22d391418013b59e8c4656c62f848b5ad5fdcc50d3a223210283889e1a8391d1459
    d654f95b8ab3911495045b5afbe2d53ad3ffd9447317bbd2103987d03bb424201a2aee083d5880d5
    3042e47df25419dad0fe2e5b4acd6b181362103a0e353866a3e079479fd7e23f3e70965c5da2b7f7
    40ffb9f6f32968c8f58655157ae",
    "bind_account_cold": "3LDA7iK8N1er3SZRNb5qKxK8WksVVtwCnf",
    "redeemScript_cold": "55210306a1c20bb3e6cfcf1c5dacb2395eac062108f62112ba6e1a
    a77f569012b08a252102c4c281dd603685082cfc3f7b1ea7d27da941465dcb4d655d664c7d9d4a56
    d57d21023e1bebbd52c2e54f8b1d1fa5f37f01c9c6698679dacf1c21d068340fab41dc7c210366f8
    574f741ff635b179e25a403820d0bc629724a4dcc31cb6bea40d0396336e2103728d3228395e284a
    1eb90e4a0d20ffde72ca8793f9c7e9abf5f978707686251e21022e7fc9b4f34cae2b3e4f2a237d18
    be0694d509893ac31b88a1a8bd33e0404e7721024a70a72d3d02385b267cd08eeac732a6337df883
    ae132161aeafbe4be1c56c0f57ae",
    "effective_block_num": 1267,
    "end_block": 4294967295
      }
    ] 

8.In bitcoin chain,transfer BTC to `hot address` : `"35ymUk9NfK4izhgp55Nphqd6dcgsvQYNfd"`.Wait about 25S,account hxtest001 will receive BTC.Query balance of account hxtest001.
    
    unlocked >>> get_account_balances hxtest001
    get_account_balances hxtest001
    [{
    "amount": 1000000000,
    "asset_id": "1.3.1"
      }
    ]

> Deposit LTC to account `hxtest002`

1.Make sure created LTC address' balance is not 0 on litecoin chain.

2.Create LTC asset on hx blockchain,if you want to create asset by senator,please import private key of senator.

    unlocked >>> import_key guard0 5JZe9Hv7twngWSEZzvvvDXP5RG1LJGixSz6WJ4D8te9x45kvDuG
    import_key guard0 5JZe9Hv7twngWSEZzvvvDXP5RG1LJGixSz6WJ4D8te9x45kvDuG
    297029ms th_a   wallet.cpp:532copy_wallet_file ] backing up wallet wallet.json to before-import-key-2856e806.wallet
    297035ms th_a   wallet.cpp:1082   save_wallet_file ] saving wallet to file wallet.json
    297040ms th_a   wallet.cpp:532copy_wallet_file ] backing up wallet wallet.json to after-import-key-2856e806.wallet
    true

    unlocked >>> wallet_create_asset  guard0 LTC 8 210000000 100000  true
    wallet_create_asset  guard0 LTC 8 210000000 100000  true
    {
      "ref_block_num": 1698,
      "ref_block_prefix": 965591732,
      "expiration": "2018-09-05T08:16:50",
      "operations": [[
      75,{
    "fee": {
      "amount": 0,
      "asset_id": "1.3.0"
    },
    "issuer": "1.2.31",
    "symbol": "LTC",
    "issuer_addr": "HXdXPBLRsiUCY1VxcDd4gGrkDcgCV3Jegb",
    "precision": 8,
    "max_supply": 210000000,
    "core_fee_paid": 100000,
    "extensions": []
      }
    ]
      ],
      "extensions": [],
      "signatures": ["1f440c5e0c94bccb8f270efb8e814ea24f66b1b4f5a5a7fd63b1452571af7ffb5e054bedf8b307b428b3dc32e1e624fbf235575798d29b652949840c70b99456d9"],
      "block_num": 0,
      "trxid": "c035858485c926ea915f4945a6c2ff834a7d0e58"
    }
    

2.Update all senators on hx blockchain,after update,system wil create a new LTC hot-cold multisign address.

    unlocked >>> update_asset_private_keys  guard0 LTC true
    unlocked >>> update_asset_private_keys  guard1 LTC true
    unlocked >>> update_asset_private_keys  guard2 LTC true
    unlocked >>> update_asset_private_keys  guard3 LTC true
    unlocked >>> update_asset_private_keys  guard4 LTC true
    unlocked >>> update_asset_private_keys  guard5 LTC true
    unlocked >>> update_asset_private_keys  guard6 LTC true

3.Query hot-cold multisign address.
    
    unlocked >>> get_multisig_account_pair LTC
    get_multisig_account_pair LTC
    [{
    "id": "2.7.2",
    "chain_type": "LTC",
    "bind_account_hot": "MErU8FfsLhXPvkzgE2BRKTyeJQExTMiZMD",
    "redeemScript_hot": "5521023db7379f0761ccbb4628c74eff5b67937bf2f3a3140d11aac56ca8780d33354d2102f0449390eb888b752fecd1f8dd381d95761c31a9a34511d3f992e9a078e170902103dc79cb12340d4d4f5a40a9ca05e058d1f6ff2691ea61aa1b05eb1330de0b39622102ac93a669ba8d75a8cb29e93e89bba6686886e93dac792222f0ee0dae1f4bd64321033a8a01b9c86746c1e24a4212979439a3a882be78fe572880a3f60aa70bc236fb2103c9e8d18f2a7e55088fae8a9e8d733e1bf167cdb4f2bfddbd285a7956cab8df77210312956e995aa696c3da4e34bdbae5a8f02efcff4ec1d51154eafc7ef64e55270757ae",
    "bind_account_cold": "MUC25gBfgyrUrUX241dT3BfU32AQGaZ19z",
    "redeemScript_cold": "5521036cba57ae77502b6e286b9c04f4074683fc5014d9d84773f0db2fb13d7a6b10f7210345156da8779b5a5c012418968e6f45abda30cbffac2c13d9a82f846ffc5bde67210243fe236e6578945ffbe123602d963ec4bcec6b997775463dfe3c17b90f3b69ab210204e31aa757d19b49171eaf4392bfae8a2e167ab9b0d26211e6bf34f9f345da152102ed336e6612a615aeb97a4ecbdd8de8055f5a0516bfcda8483136d3053c213d9c210367aec8c7ce911ba88f94ff6b16943c3688e3d87c384da6926ea28ea7249db44121035ef1d0343c809639e64799e897169f95b7393645402ebc81e63c955c9e9ff6a757ae",
    "effective_block_num": 0,
    "end_block": 4294967295
      }
    ]

4.Initiate a proposal to enable multiple signature addresses to take effect.

    unlocked >>> account_change_for_crosschain guard0 LTC MErU8FfsLhXPvkzgE2BRKTyeJQExTMiZMD MUC25gBfgyrUrUX241dT3BfU32AQGaZ19z 10000 true

    account_change_for_crosschain guard0 LTC MErU8FfsLhXPvkzgE2BRKTyeJQExTMiZMD MUC25gBfgyrUrUX241dT3BfU32AQGaZ19z 10000 true
    {
      "ref_block_num": 1788,
      "ref_block_prefix": 3124051331,
      "expiration": "2018-09-05T08:24:35",
      "operations": [[
      28,{
    "type": 0,
    "fee": {
      "amount": 0,
      "asset_id": "1.3.0"
    },
    "proposer": "1.2.31",
    "fee_paying_account": "HXdXPBLRsiUCY1VxcDd4gGrkDcgCV3Jegb",
    "expiration_time": "2018-09-05T11:01:16",
    "proposed_ops": [{
    "op": [
      74,{
    "chain_type": "LTC",
    "fee": {
      "amount": 0,
      "asset_id": "1.3.0"
    },
    "cold": "MUC25gBfgyrUrUX241dT3BfU32AQGaZ19z",
    "hot": "MErU8FfsLhXPvkzgE2BRKTyeJQExTMiZMD"
      }
    ]
      }
    ],
    "extensions": []
      }
    ]
      ],
      "extensions": [],
      "signatures": ["20157bc57e7816373e294fa901ac5e0171925a5a0904984775af6b3d20cc56cccb3da02dcc289998115e4ee91af01acf0d704bf28d534eab9b04f4cd52ccc5fd72"],
      "block_num": 0,
      "trxid": "b503fa3d5a2513eba3c4e55c59345ec5376e53ec"
    }

5.Get proposal id.

    unlocked >>> get_proposal_for_voter guard0
    get_proposal_for_voter guard0
    [{
    "id": "1.10.1",
    "proposer": "1.2.31",
    "expiration_time": "2018-09-05T11:01:16",
    "proposed_transaction": {
      "ref_block_num": 0,
      "ref_block_prefix": 0,
      "expiration": "2018-09-05T11:01:16",
      "operations": [[
      74,{
    "chain_type": "LTC",
    "fee": {
      "amount": 0,
      "asset_id": "1.3.0"
    },
    "cold": "MUC25gBfgyrUrUX241dT3BfU32AQGaZ19z",
    "hot": "MErU8FfsLhXPvkzgE2BRKTyeJQExTMiZMD"
      }
    ]
      ],
      "extensions": []
    },
    "required_active_approvals": [],
    "available_active_approvals": [],
    "required_owner_approvals": [],
    "available_owner_approvals": [],
    "available_key_approvals": [],
    "approved_key_approvals": [],
    "disapproved_key_approvals": [],
    "required_account_approvals": [
      "HXdXPBLRsiUCY1VxcDd4gGrkDcgCV3Jegb",
      "HX3HmP3gqcDqYvHvVq2Hn44nuUDfSSBMU55",
      "HXC3X3WoKyqNQZDyPN3Pq55gX5sLhVJxZNh",
      "HXGu1qvt9pG55W3CfAETgwDFi2NwvWQGV4y",
      "HXHd49CtDZZW7ySYZNQYaUurZNWW76HBnhU",
      "HXMGFZwHXyiFj1MUwCVMoyzqBJ4CuTC7xpX",
      "HXMkBpQ9nj1hHXwEGQvyZdFiRgRK78ixKPA"
    ],
    "type": "committee"
      }
    ]
    
6.Approve proposal，more than two-thirds of the senators agreed with the proposal, multiple addresses will to take effect.

    unlocked >>> approve_proposal guard0 1.10.1 {"key_approvals_to_add": ["HXC3X3WoKyqNQZDyPN3Pq55gX5sLhVJxZNh", "HXHd49CtDZZW7ySYZNQYaUurZNWW76HBnhU", "HXdXPBLRsiUCY1VxcDd4gGrkDcgCV3Jegb", "HXMkBpQ9nj1hHXwEGQvyZdFiRgRK78ixKPA", "HX3HmP3gqcDqYvHvVq2Hn44nuUDfSSBMU55"]}  true

    approve_proposal guard0 1.10.1 {"key_approvals_to_add": ["HXC3X3WoKyqNQZDyPN3Pq55gX5sLhVJxZNh", "HXHd49CtDZZW7ySYZNQYaUurZNWW76HBnhU", "HXdXPBLRsiUCY1VxcDd4gGrkDcgCV3Jegb", "HXMkBpQ9nj1hHXwEGQvyZdFiRgRK78ixKPA", "HX3HmP3gqcDqYvHvVq2Hn44nuUDfSSBMU55"]}  true
    {
      "ref_block_num": 1833,
      "ref_block_prefix": 1461401128,
      "expiration": "2018-09-05T08:28:50",
      "operations": [[
      29,{
    "fee": {
      "amount": 0,
      "asset_id": "1.3.0"
    },
    "fee_paying_account": "HXdXPBLRsiUCY1VxcDd4gGrkDcgCV3Jegb",
    "proposal": "1.10.1",
    "active_approvals_to_add": [],
    "active_approvals_to_remove": [],
    "owner_approvals_to_add": [],
    "owner_approvals_to_remove": [],
    "key_approvals_to_add": [
      "HXdXPBLRsiUCY1VxcDd4gGrkDcgCV3Jegb",
      "HX3HmP3gqcDqYvHvVq2Hn44nuUDfSSBMU55",
      "HXC3X3WoKyqNQZDyPN3Pq55gX5sLhVJxZNh",
      "HXHd49CtDZZW7ySYZNQYaUurZNWW76HBnhU",
      "HXMkBpQ9nj1hHXwEGQvyZdFiRgRK78ixKPA"
    ],
    "key_approvals_to_remove": [],
    "extensions": []
      }
    ]
      ],
      "extensions": [],
      "signatures": ["204e95fa9b4f43955e43e3c577d4f262ffc1897e7de31268b5440bbdd4231a20ca46754f39c3e854d811f3684f1a750354edc7bd2c08c046319067f3c6136e4f1f", "1f3e55e7e23ef965fcc91c0637bb2550914d4d9d5a1708e71da6989769c767de0f2cd655083bb371e075ca2d8ffabaf0535d2bbc1b73842446d02988b1a9aa0254","2073a6c02b2bb3bc0d317cca87b192362b643b948df5a738a3a2c666f3958f67617ede3cfc01fcf3fc831cf057dc31e02886d7b431d6c623dbb1caa67265646e27","207d03876702431521094afc59e8635441ef05e0f7f670190608af71db343740d511ec7bc8d76bcfb14be2708b07b2c599f3e582ecb4c0776f9ead9f89714f15d0","20015ef8677508aefdf0a8591779c2befb58d226860d6f1ac4b536da809d4380e74499ee44528db9a536814d3b5d35d1e3e7c1028b9b98172cc85da5cc53a37afd"],
      "block_num": 0,
      "trxid": "ab889c45010eea6768ccff2d0d678c6ddcd71418"
    }

7.Query multi-sign address,if "effective_block_num" is not 0,means this addres has take effect.

    unlocked >>> get_multisig_account_pair LTC
    get_multisig_account_pair LTC
    [{
    "id": "2.7.2",
    "chain_type": "LTC",
    "bind_account_hot": "MErU8FfsLhXPvkzgE2BRKTyeJQExTMiZMD",
    "redeemScript_hot": "5521023db7379f0761ccbb4628c74eff5b67937bf2f3a3140d11aac56ca8780d33354d2102f0449390eb888b752fecd1f8dd381d95761c31a9a34511d3f992e9a078e170902103dc79cb12340d4d4f5a40a9ca05e058d1f6ff2691ea61aa1b05eb1330de0b39622102ac93a669ba8d75a8cb29e93e89bba6686886e93dac792222f0ee0dae1f4bd64321033a8a01b9c86746c1e24a4212979439a3a882be78fe572880a3f60aa70bc236fb2103c9e8d18f2a7e55088fae8a9e8d733e1bf167cdb4f2bfddbd285a7956cab8df77210312956e995aa696c3da4e34bdbae5a8f02efcff4ec1d51154eafc7ef64e55270757ae",
    "bind_account_cold": "MUC25gBfgyrUrUX241dT3BfU32AQGaZ19z",
    "redeemScript_cold": "5521036cba57ae77502b6e286b9c04f4074683fc5014d9d84773f0db2fb13d7a6b10f7210345156da8779b5a5c012418968e6f45abda30cbffac2c13d9a82f846ffc5bde67210243fe236e6578945ffbe123602d963ec4bcec6b997775463dfe3c17b90f3b69ab210204e31aa757d19b49171eaf4392bfae8a2e167ab9b0d26211e6bf34f9f345da152102ed336e6612a615aeb97a4ecbdd8de8055f5a0516bfcda8483136d3053c213d9c210367aec8c7ce911ba88f94ff6b16943c3688e3d87c384da6926ea28ea7249db44121035ef1d0343c809639e64799e897169f95b7393645402ebc81e63c955c9e9ff6a757ae",
    "effective_block_num": 1843,
    "end_block": 4294967295
      }
    ]

8.In litcoin chain,transfer LTC to `hot address` : `MErU8FfsLhXPvkzgE2BRKTyeJQExTMiZMD`.Wait about 25S,account hxtest002 will receive LTC.Query balance of account hxtest002.
    
    unlocked >>> get_account_balances hxtest002
    get_account_balances hxtest002
    [{
    "amount": "84899552000",
    "asset_id": "1.3.2"
      }
    ]
   
## Exchange Flow

> Exchange Contract

Write a exchange contract,compile to gpc file, then register contract to hyperexchange chain.(Please make sure `hxtest001` has enough `HX`)

    unlocked >>> register_contract hxtest001 0.001 10000 "E:/link_mytest/blocklink_e
    xchange.lua.gpc"
    
    "contract_id": "CHX4W971o4Q84ihbAMJ9xbaBMAVwtVJRbP7s"

> Currency Exchange

1.hxtest001 deposit 1 BTC to contract.

    unlocked >>> transfer_to_contract hxtest001 CHX4W971o4Q84ihbAMJ9xbaBMAVwtVJRbP7s
     1 "BTC" "" 0.001 10000 true
    transfer_to_contract hxtest001 CHX4W971o4Q84ihbAMJ9xbaBMAVwtVJRbP7s 1 "BTC" "" 0
    .001 10000 true
    {
      "ref_block_num": 3030,
      "ref_block_prefix": 4031504198,
      "expiration": "2018-09-05T10:13:20",
      "operations": [[
      81,{
    "fee": {
      "amount": 12000,
      "asset_id": "1.3.0"
    },
    "invoke_cost": 10000,
    "gas_price": 100,
    "caller_addr": "HXNUZSB27eoKGki79mioGrS5YyKxdXEzvQu",
    "caller_pubkey": "039541c82bb4cd832ff4c11e39b894609b3c035add4b133d55a6d5
    b72c4ac28ad6",
    "contract_id": "CHX4W971o4Q84ihbAMJ9xbaBMAVwtVJRbP7s",
    "amount": {
      "amount": 100000000,
      "asset_id": "1.3.1"
    },
    "param": ""
      }
    ]
      ],
      "extensions": [],
      "signatures": [
    "2027af412ac03384b9a4ac1d6d81ca1e3947cb6a2e3b18144e0d242b5e09f5bb22754e9b115
    55bf33a22f84576be7b95f1cb0d69fb43e0fc006b701468b8be5f6e"
      ],
      "block_num": 0,
      "trxid": "2f3b7e9b8bc48b158030b27a44e40a4e2ac8b061"
    }

2.Put on a sell order.

    unlocked >>> invoke_contract hxtest001 0.001 10000 CHX4W971o4Q84ihbAMJ9xbaBMAVwtVJRbP7s putOnSellOrder "BTC,100000000,LTC,250000000"
    invoke_contract hxtest001 0.001 10000 CHX4W971o4Q84ihbAMJ9xbaBMAVwtVJRbP7s putOn
    SellOrder "BTC,100000000,LTC,250000000"
    {
      "ref_block_num": 3059,
      "ref_block_prefix": 4003603969,
      "expiration": "2018-09-05T10:15:45",
      "operations": [[
      79,{
    "fee": {
      "amount": 12000,
      "asset_id": "1.3.0"
    },
    "invoke_cost": 10000,
    "gas_price": 100,
    "caller_addr": "HXNUZSB27eoKGki79mioGrS5YyKxdXEzvQu",
    "caller_pubkey": "039541c82bb4cd832ff4c11e39b894609b3c035add4b133d55a6d5b72c4ac28ad6",
    "contract_id": "CHX4W971o4Q84ihbAMJ9xbaBMAVwtVJRbP7s",
    "contract_api": "putOnSellOrder",
    "contract_arg": "BTC,100000000,LTC,250000000",
    "offline": false
      }
    ]
      ],
      "extensions": [],
      "signatures": ["1f76a6144438f6c571607304348307d3c087b332b3548f50154d864932ccca63815c7d357c51f5a67799deed95af070fad416a022e9f058768d08207ebd55baaf0"],
      "block_num": 0,
      "trxid": "9d141aa4782e97187f152031135d1bdc10ef7306"
    }

3.hxtest002 put on a order to buy 1BTC by call the interface of contract.

    unlocked >>> transfer_to_contract hxtest002 CHX4W971o4Q84ihbAMJ9xbaBMAVwtVJRbP7s
     10 "LTC" "BTC,100000000" 0.001 10000 true
    transfer_to_contract hxtest002 CHX4W971o4Q84ihbAMJ9xbaBMAVwtVJRbP7s 10 "LTC" "BTC,100000000" 0.001 10000 true
    {
      "ref_block_num": 13361,
      "ref_block_prefix": 2405013881,
      "expiration": "2018-09-06T01:15:00",
      "operations": [[
      81,{
    "fee": {
      "amount": 12000,
      "asset_id": "1.3.0"
    },
    "invoke_cost": 10000,
    "gas_price": 100,
    "caller_addr": "HX8Vx4U1HfPBhHQF8J2z55qyiMCaJBce5gQ",
    "caller_pubkey": "034317fbda4543caa127aa82a0558194c213066762b6ce15c5215d756ff301efaf",
    "contract_id": "CHX4W971o4Q84ihbAMJ9xbaBMAVwtVJRbP7s",
    "amount": {
      "amount": 1000000000,
      "asset_id": "1.3.2"
    },
    "param": "BTC,100000000"
      }
    ]
      ],
      "extensions": [],
      "signatures": ["1f6f51e1b0406931a47910734b8d8ee2d3a7b1bf9ff7767cf7a8d427a1120534250b5c9fbaeffb1b48d5df9fb6fb46d81bdefaadca19099aa80d58eed1f064e000"],
      "block_num": 0,
      "trxid": "d4ef8b05a42e2cff7a6443902aa4b6cc3d647851"
    }

4.Query balance of hxtest002.Amount will be 1*precision which "asset_id" is "1.3.1"
    
    unlocked >>> get_account_balances hxtest002
    get_account_balances hxtest002
    [{
    "amount": 999995100,
    "asset_id": "1.3.0"
      },{
    "amount": 100000000,
    "asset_id": "1.3.1"
      },{
    "amount": "84649552000",
    "asset_id": "1.3.2"
      }
    ]

5.Withdraw bought 2.5 LTC to hxtest001.

    unlocked >>> invoke_contract hxtest001 0.001 10000 CHX4W971o4Q84ihbAMJ9xbaBMAVwtVJRbP7s withdrawAsset "LTC,250000000"
    invoke_contract hxtest001 0.001 10000 CHX4W971o4Q84ihbAMJ9xbaBMAVwtVJRbP7s withdrawAsset "LTC,250000000"
    {
      "ref_block_num": 13430,
      "ref_block_prefix": 452881267,
      "expiration": "2018-09-06T01:21:00",
      "operations": [[
      79,{
    "fee": {
      "amount": 12000,
      "asset_id": "1.3.0"
    },
    "invoke_cost": 10000,
    "gas_price": 100,
    "caller_addr": "HXNUZSB27eoKGki79mioGrS5YyKxdXEzvQu",
    "caller_pubkey": "039541c82bb4cd832ff4c11e39b894609b3c035add4b133d55a6d5b72c4ac28ad6",
    "contract_id": "CHX4W971o4Q84ihbAMJ9xbaBMAVwtVJRbP7s",
    "contract_api": "withdrawAsset",
    "contract_arg": "LTC,250000000",
    "offline": false
      }
    ]
      ],
      "extensions": [],
      "signatures": ["2052608a77d042af3020341aa6d0e5b965dc8e9447ac17b22302b7fbac2d20c65375cdbf184adf94e39863e043d0f301bf7058745f55dcb8d61aa0556213d47cf1"],
      "block_num": 0,
      "trxid": "7d56c9545a42729ed6e55df43448c53734d72efe"
    }

6.Query balance of hxtest001,amount will be 2.5*precision which "asset_id" is "1.3.2".

    unlocked >>> get_account_balances hxtest001
    get_account_balances hxtest001
    [{
    "amount": 999984290,
    "asset_id": "1.3.0"
      },{
    "amount": 900000000,
    "asset_id": "1.3.1"
      },{
    "amount": 250000000,
    "asset_id": "1.3.2"
      }
    ]

## Withdrawal

1.Withdraw to an address of litecoin chain.Will create a crosschain transaction.

    unlocked >>> withdraw_cross_chain_transaction hxtest001 2.5 LTC LhamrSpU9E55VEfgmKNxuX7VnWNZLdw8uA "" true

    withdraw_cross_chain_transaction hxtest001 2.5 LTC LhamrSpU9E55VEfgmKNxuX7VnWNZLdw8uA "" true
    {
      "ref_block_num": 14011,
      "ref_block_prefix": 2913418489,
      "expiration": "2018-09-06T02:24:15",
      "operations": [[
      61,{
    "fee": {
      "amount": 0,
      "asset_id": "1.3.0"
    },
    "withdraw_account": "HXNUZSB27eoKGki79mioGrS5YyKxdXEzvQu",
    "amount": "2.5",
    "asset_symbol": "LTC",
    "asset_id": "1.3.2",
    "crosschain_account": "LhamrSpU9E55VEfgmKNxuX7VnWNZLdw8uA",
    "memo": ""
      }
    ]
      ],
      "extensions": [],
      "signatures": ["1f73948075b5403e9d99d26bf6cd2c461f46d7844df7bc1ea0dbf107535678add57a836bd947c701a14a13b876939a217ae0c3062e262bc527ec458c550b014251"],
      "block_num": 0,
      "trxid": "9b2df1bc9376fd649d569bf4345165bd4523883a"
    }

2.Query created crosschain transaction.

    unlocked >>> get_crosschain_transaction 1
    get_crosschain_transaction 1
    [[
    "977b443566b1105a2a2159cb7a4d9a023dd44f92",{
      "ref_block_num": 14011,
      "ref_block_prefix": 2913418489,
      "expiration": "2018-09-06T02:14:45",
      "operations": [[
      62,{
    "fee": {
      "amount": 0,
      "asset_id": "1.3.0"
    },
    "ccw_trx_ids": [
      "9b2df1bc9376fd649d569bf4345165bd4523883a"
    ],
    "withdraw_source_trx": {
      "hex": "020000000196aa8d21549926bb0a2b2c163e91c1ff783ff06158756c33f5b4758057c860770000000000ffffffff02e02be50e000000001976a914f542d013712017a417defd6a29615b2e1a2b84a288ac803125450200000017a9144c4691c0f89c01775330e84d307e45f1a4f101478700000000",
      "scriptPubKey": [
    "a9144c4691c0f89c01775330e84d307e45f1a4f1014787"
      ],
      "trx": {
    "hash": "6f9885fae162d1b492cc2e764d48d44c37df6fac7018411f54109f485a7fbd4d",
    "locktime": 0,
    "size": 117,
    "txid": "6f9885fae162d1b492cc2e764d48d44c37df6fac7018411f54109f485a7fbd4d",
    "version": 2,
    "vin": [{
    "scriptSig": {
      "asm": "",
      "hex": ""
    },
    "sequence": 4294967295,
    "txid": "7760c8578075b4f5336c755861f03f78ffc1913e162c2b0abb269954218daa96",
    "vout": 0
      }
    ],
    "vout": [{
    "n": 0,
    "scriptPubKey": {
      "addresses": [
    "LhamrSpU9E55VEfgmKNxuX7VnWNZLdw8uA"
      ],
      "asm": "OP_DUP OP_HASH160 f542d013712017a417defd6a29615b2e1a2b84a2 OP_EQUALVERIFY OP_CHECKSIG",
      "hex": "76a914f542d013712017a417defd6a29615b2e1a2b84a288ac",
      "reqSigs": 1,
      "type": "pubkeyhash"
    },
    "value": "2.49900000000000011"
      },{
    "n": 1,
    "scriptPubKey": {
      "addresses": [
    "MErU8FfsLhXPvkzgE2BRKTyeJQExTMiZMD"
      ],
      "asm": "OP_HASH160 4c4691c0f89c01775330e84d307e45f1a4f10147 OP_EQUAL",
      "hex": "a9144c4691c0f89c01775330e84d307e45f1a4f1014787",
      "reqSigs": 1,
      "type": "scripthash"
    },
    "value": "97.50000000000000000"
      }
    ],
    "vsize": 117
      }
    },
    "miner_broadcast": "1.6.4",
    "miner_address": "HX2WbZT9ZgYQC92BdUGAqkbHXpmYqgxXdex",
    "asset_id": "1.3.2",
    "asset_symbol": "LTC",
    "crosschain_fee": {
      "amount": 0,
      "asset_id": "1.3.2"
    }
      }
    ]
      ],
      "extensions": [],
      "signatures": ["2073f66bb19fd429246d16f377794707461fd9a6efe7264b72eb4b128ebabe6a454adbcf879f0eaaa5c72b124e5ae1b1e0b4b7d339cd5e077c44081366b5c5d286"]
    }],[
    "9b2df1bc9376fd649d569bf4345165bd4523883a",{
      "ref_block_num": 14011,
      "ref_block_prefix": 2913418489,
      "expiration": "2018-09-06T02:24:15",
      "operations": [[
      61,{
    "fee": {
      "amount": 0,
      "asset_id": "1.3.0"
    },
    "withdraw_account": "HXNUZSB27eoKGki79mioGrS5YyKxdXEzvQu",
    "amount": "2.5",
    "asset_symbol": "LTC",
    "asset_id": "1.3.2",
    "crosschain_account": "LhamrSpU9E55VEfgmKNxuX7VnWNZLdw8uA",
    "memo": ""
      }
    ]
      ],
      "extensions": [],
      "signatures": ["1f73948075b5403e9d99d26bf6cd2c461f46d7844df7bc1ea0dbf107535678add57a836bd947c701a14a13b876939a217ae0c3062e262bc527ec458c550b014251"]
    }
      ]
    ]

3.Sign transaction,more than two-thirds of the senators sign the transaction, it will broadcast success.

    unlocked >>> senator_sign_crosschain_transaction 977b443566b1105a2a2159cb7a4d9a023dd44f92 guard0
    unlocked >>> senator_sign_crosschain_transaction 977b443566b1105a2a2159cb7a4d9a023dd44f92 guard1
    unlocked >>> senator_sign_crosschain_transaction 977b443566b1105a2a2159cb7a4d9a023dd44f92 guard2
    unlocked >>> senator_sign_crosschain_transaction 977b443566b1105a2a2159cb7a4d9a023dd44f92 guard3
    unlocked >>> senator_sign_crosschain_transaction 977b443566b1105a2a2159cb7a4d9a023dd44f92 guard4

4.Query balance of hxtest001,amount will be 0 which "asset_id" is "1.3.2".

    unlocked >>> get_account_balances hxtest001
    get_account_balances hxtest001
    [{
    "amount": 999984290,
    "asset_id": "1.3.0"
      },{
    "amount": 900000000,
    "asset_id": "1.3.1"
      },{
    "amount": 0,
    "asset_id": "1.3.2"
      }
    ]

5.On litecoin chain,after create some blocks,you can get balance of address "LhamrSpU9E55VEfgmKNxuX7VnWNZLdw8uA",will be 2.49900000(minus fee 0.001).

## RPC command list

> Basic RPC Interface

1.info

    Return current information, block number and etc. to HX chain
2.wallet_create_account  name

    create wallet account, return account address 
3.dump_private_key name

    obtain private keys of wallet account, return address+private keys. 
4.import_key name private_key

    import private keys of account `name`
5.register_account name true
    
    This account name is registered on-chain
6.transfer_to_address from to amount symbol memo true

    transfer to certain address: 
    from:sent from address 
    to：receive address 
    amount： total transfer amount 
    symbol: currency type 
    memo: other information

7.get_transaction trxid

trxid:transaction id

    acquire all information of this transaction according to transaction ID, only on-chain transaction can be traced. 

8.get_block blocknum

    detail information of one block can be returned according to block number.
    blocknum: block number
9.get_miner name

    return citizen detail information according to user name, if this account is not citizen, return empty/blank/void 

10.get_guard_member name


    return senator detail information according to user name, if this account is not senator, return empty/blank/void
11.create_miner name url true

    register to become a citizen, which can join mining 
    name:account name 
    url: website address 
12.create_crosschain_symbol symbol

    create specific assets addresses, return address 
    symbol: currency type
13.bind_tunnel_account account tunnel_account symbol true

    bind tunnel account, the address on other chain is binding with current actual account, tunnel_account private key is needed.
    account: account name 
    tunnel_account: an appointed assets address 
    symbol：currency type
14.unbind_tunnel_account account tunnel_account symbol true
    
    unbind tunnel account, the address on other chain is bound with current actual account, tunnel_account private key is needed.
15.get_binding_account account symbol 

    inquire tunnel account of specific assets 
    account: current account name
    symbol: currency type
16.get_multisig_account_pair symbol 
    
    acquire current on-chain multi-signature address of specific currency, which includes multi-signature address history
17.get_current_multi_address symbol

    acquire current on-chain multi-signature address of specific currency
18.withdraw_cross_chain_transaction account amount symbol crosschain_addr memo true

    initiate withdrawal request
    account: withdrawal request initiator
    amount:  withdrawal amount 
    symbol： currency type of withdrawal 
    crosschain_addr: specific assets receive address 
    memo: additional information
19.refund_request refund_acount txid true
    
    apply for a cancellation of cross-chain withdrawal 
    runfund_account: account name
    txid: would like to cancel withdrawal transaction ID

> About Acceptance

1.create_guarantee_order account asset_orign asset_target symbol true

    create acceptance fee,this operation is used for those accounts have HX and would like to exchange to other currencies, such as BTC. 
    account:creator of acceptance fee form 
    asset_orign : means the HX can not be used for acceptance fee in this account
    asset_target : the amount of tokens that you would like to exchange to
    symbol:  currency type
2.list_guarantee_order symbol all

    return qualified acceptance order queue
    symbol: assets type/ currency type 
    all true/false,if all acceptance order are listed, including completed orders. HX is need as fees during any transaction, however if there is no HX in the account, use other currencies in the account to pay for fees. 
3.get_my_guarantee_order account all

    return to the acceptance order which was created by this address
    account: account address 
    all： whether includes completed acceptance orders
4.set_guarantee_id guarantee_id
    
    choose an acceptance order before transaction, this operation is valid once only is operated locally.
    guarantee_id : Acceptance ID 
 

> Senator related:

Senator in charge of cross-chain assets, most operations are voting related. 

1.create_guard_member  proposer_account account url expiration_time true

    create an proposal to upgrade specific account(s) to candidate senator(s)
    proposer_account: proposer account 
    account：senator candidate senator 
    url : website address 
    expiration_time: expiration time 
2.update_guard_formal proposer_account formal expiration_time  true
    
    proposal initiator and official senator account 
    formal :default set as true, make senator an official senator 
3.guard_appointed_publisher proposer publisher symbol expiration_time true

    specify publisher for certain asset 
    proposer: proposer
    publisher: feed person (account)/publisher 
    symbol: assets type for feed
4.miner_appointed_crosschain_fee proposer fee symbol expiration_time true

    initiate a proposal, specify cross-chain withdrawel fee of certain specific assets. 
    fee： fee for cross-chain withdrawal 
    symbol： cross-chain assets type 
5.miner_appointed_lockbalance_guard proposer lockbalance expiration_time true

    initiate a proposal to modify the amount of pledged deposit and its currency type of an Senator. 
    lockbalance: specify the amount of pledged deposit and its currency type of a Senator. 
6.update_asset_private_keys account symbol true

    it is used to create a pair of private keys of specific assets, and broadcast corresponding public keys on the chain. HX will create a pair of new multi-signature addresses (cold and hot wallets) according to received public keys. 
    account:transaction initiator 
    symbol：assets type
7.account_change_for_crosschain proposer symbol hot cold  expiration_time true

    initiate a proposal，in order to validate hot address(wallet) and cold address(wallet) on chain 
    symbol：asset type
    hot：hot wallet address
    cold:cold wallet address 
8.get_proposal_for_voter account
    
    acquire all necessary proposals for the signature of this account 
    account：current account name 
9.approve_proposal account proposal_id delta true
    
    account: voter 
    proposal_id: proposal ID 
    delta: see voting content as below{"key_approvals_to_add":[addr]，“key_approvals_to_remove”：[addr]}    
10.get_crosschain_transaction type

    type：状态 0,1,2,3,4Status 
      0： withdrawal request status 
      1,2： waiting for signature or in the process of signing 
      3： transaction signed and broadcast 
      4： package this transaction on corresponding chain  

11.guard_sign_crosschain_transaction trxid senator

    sign withdrawal transaction 
    trxid: under status 1, withdrawal transaction ID 
    senator：Senator account name



---