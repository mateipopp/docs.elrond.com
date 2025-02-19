---
id: embed
title: Embedding Mandos code in Go
---

# **Embedding in Go**

Mandos steps can be embedded in Go, in order to program for more flexible behavior. One can even save dynamically generated Mandos scenarios. For a comprehensive example on how to do that, check out the [delegation contract fuzzer in Elrond VM](https://github.com/ElrondNetwork/wasm-vm/tree/master/fuzz/delegation) or the [DNS contract deployment scenario test generator](https://github.com/ElrondNetwork/wasm-vm/tree/master/cmd/testgen/dns). Just a snippet from the fuzzer:

```
_, err = pfe.executeTxStep(fmt.Sprintf(`
	{
		"step": "scDeploy",
		"txId": "-deploy-",
		"tx": {
			"from": "''%s",
			"value": "0",
			"contractCode": "file:delegation.wasm",
			"arguments": [
				"''%s",
				"%d",
				"%d",
				"%d"
			],
			"gasLimit": "100,000",
			"gasPrice": "0"
		},
		"expect": {
			"out": [],
			"status": "",
			"logs": [],
			"gas": "*",
			"refund": "*"
		}
	}`,
		string(pfe.ownerAddress),
		string(pfe.auctionMockAddress),
		args.serviceFee,
		args.numBlocksBeforeForceUnstake,
		args.numBlocksBeforeUnbond,
	))
```
