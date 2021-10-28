

## TransparentUpgradeableProxy

### 1. Find the original source code. 

For easy way, just get the source from another network which already verified: 
https://rinkeby.etherscan.io/address/0xC642ef7021597DfAcD125BB87AE1D1b91F2dB5eB#code

### 2. Prepare Standard-Json-Input format

- Template
```
{
  "language": "Solidity",
  "sources": {
    "TransparentUpgradeableProxy.sol": {
      "content": "// SPDX-License-Identifier: MIT\r\n\r\npragma solidity ^0.8.0;\r\n\r\nimport \"../ERC1967/ERC1967Proxy.sol\";......"
    },
    "ERC1967/ERC1967Proxy.sol": {
      "content": "......"
    }
  },
  "settings": {
    "optimizer": {
      "enabled": true,
      "runs": 200
    },
    "outputSelection": {
      "*": {
        "*": [
          "evm.bytecode",
          "evm.deployedBytecode",
          "abi"
        ]
      }
    },
    "libraries": {}
  }
}

```

- Prepare source content:
	+ Access this: https://testnet.bscscan.com/json-serialize
	+ Copy and paste original source and Convert to get "Serialized Json String"
	+ Copy "Serialized Json String" to "content"

### 3. Get Constructor Arguments ABI-encoded

- Way1: using https://abi.nhancv.com to find Arguments if you know constructor input value correctly
- Way2: If you dont know input value clearly, and the tx just show a long hex in "Input Data", you can try my way. :3 
	- For example deployment tx: https://testnet.bscscan.com/tx/0x45c2ccdf44113ca3a28ff16b4f64e36ac0feb5f1b78e989ab0f5eacb5f123870
	- Input Data:
```
0x608060405260405162000f4............076cc3735a920a3ca505d382bbc416464726573733a206c6f772d6c6576656c2064656c65676174652063616c6c206661696c65640000000000000000000000004de65e961a8a19c2edb057c3ce5dd3bd3fe915d4000000000000000000000000da808402153b8d4a839322312e512caf0ddb6ec7000000000000000000000000000000000000000000000000000000000000006000000000000000000000000000000000000000000000000000000000000000249ab6074e000000000000000000000000000000000000000000000000000000000000002a00000000000000000000000000000000000000000000000000000000
```
	- Look at the end of "Input Data", you can see some value with prefix long '0'. It's param. Because the address cannot fullfil 256 bytes. :), it will show as '0'. So the param of this example is
```
0000000000000000000000004de65e961a8a19c2edb057c3ce5dd3bd3fe915d4000000000000000000000000da808402153b8d4a839322312e512caf0ddb6ec7000000000000000000000000000000000000000000000000000000000000006000000000000000000000000000000000000000000000000000000000000000249ab6074e000000000000000000000000000000000000000000000000000000000000002a00000000000000000000000000000000000000000000000000000000
```

### 4. Verify contract

- Access: https://testnet.bscscan.com/verifyContract?a=0x4031B139faFfD14119F142A75c2d04aDB15C5c81
- Compiler Type: Solidity (Standard-Json-Input)
- Compiler Version: v0.8.2+commit.661d1103
- License Type: MIT
- Agree -> Continue
- Select Standard-Json-Input.json file which created above -> Upload
- Fill "Constructor Arguments ABI-encoded" if needed, leave a bank as default
- Verify and Publish











