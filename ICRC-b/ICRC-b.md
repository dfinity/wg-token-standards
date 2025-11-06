|ICRC|Title|Author|Discussions|Status|Type|Category|Created|
|:----:|:----:|:----:|:----:|:----:|:----:|:----:|:----:|
|FIX a|ICP Network Identifiers|Quint Daenen (@q-uint), Dieter Sommer (@dietersommer), Thomas Gladdines (@sea-snake), Austin Fatheree (@skilesare)||[]()|Issue|Standards Track|2023-05-17|


# ICP Network Identifiers

This standard defines a normative way of specifying the identifier of ICP-based blockchain networks, compatible with the corresponding CAIP-2-specification [CAIP-2]. Such a network identifier has a wide field of applications, such as referring to tokens ledgers, account addresses, or other assets such as individual tokens on an ICP network in a way compatible with the goals of the CAIP group of chain agnosticity.

## Rationale

This standard defines the namespace for the Internet Computer Protocol (ICP) provides a standardized system for identifying any blockchain network based on the ICP protocol stack. It promotes interoperability, efficient querying, and clarity in asset identification, benefitting developers and users working with decentralized applications and assets on the Internet Computer.

## Terminology

We first define terminology that is slightly different to other ecosystems for reasons given below. In most (or all) other blockchain ecosystems, what we are discussing in this ICRC is referred to as *chain identifier* or *chain id*. This clashes with the efforts of this ICRC standard:

* In the ICP ecosystem, a network, such as ICP mainnet, can be, and typically is, comprised of multiple (or many) subnetworks, each of which is technically speaking its own blockchain. However, we want to refer to a whole network, not only a subnet, with the names defined in this ICRC. Thus, the term *chain* does not well capture our intentions. For this reason, we use the term *network*.

## Syntax

We define two basic ways of referring to icp blockchain networks.
1 **Option 1: Registry**: Through a network name registered in a registry.
1 **Option 2: Derivation** Through a network name derived from the root public key of the network, where the root public key is the public key through which the whole network can be identified (e.g., NNS public key for ICP mainnet).


The `chain_id` is a case-sensitive string in the form according to [CAIP-2]:

```
chain_id:    namespace + ":" + reference
namespace:   [\-a-z0-9]{3,8}
reference:   [\-_a-zA-Z0-9]{1,32}
```

Using the `icp` namespace, we define the CAIP-2-compliant syntax for ICP Network Identifiers:

// FIX unify the grammar to EBNF, ABNF or some other widely-used system.
```
network_id =    namespace + ":" + reference
namespace =    "icp"
reference =    registry_reference / derivation_reference
registry_reference = 1-9 [0-9]{0,30}
derivation_reference = [a-f0-9]{1,32}
```

The ICP *namespace* is always `icp` (see [ICP namespace]) and the *reference* (or *network name*) is either (1) an identifier registered in the registry defined by ICRC-?? [ICRC-a] or (2) the first 32 characters of hexadecimal representation of the SHA-256 hash of the root key of the ICP network.

The namespace identifier in the Registry Option (1) must have a length of at most 31 digits in order to differentiate it from the Derivation Option (2) which uses exactly a 32-character representation of the network reference.

Not every network has a name defined through a registry as of Option (1), but every network has a derived name as specified through Option (2).

It is recommended to use a registered reference for networks that have one for the reason of the shorter and human-interpretable string. This is particularly true for ICP mainnet as it is expected to be the most used identifier and `icp:1` is a substantially simpler and easier-to-read identifier than `icp:737ba355e855bd4b61279056603e0550`.

## Identifier Resolution

Resolution for the Registry Option is a straightforward lookup in the registry document.

When using the Derivation Option for identifying an ICP network, you can resolve the root key of the network by querying the status endpoint of the ICP API. The response is CBOR encoded and contains the root key.

```shell
curl "https://icp0.io/api/v2/status" --output - | hexdump -C
```

For private ICP networks referred to as UTOPIA, we refer the reader to the UTOPIA documentation for the definition of the root key of a UTOPIA instance as well as how to obtain the root key from the network to compute the hash. The computation is performed exactly as described above for ICP mainnet.

Once the root key has been obtained, the reference can be calculated by taking the first 32 characters of the hexadecimal representation of the SHA-256 hash of the root key.

Hexadecimal key characters are always presented with lowercase letters. Uppercase is not permitted as it would lead to multiple valid identifiers for the same network.

```shell
rootKey=$(echo "308182301d060d2b0601040182dc7c0503010201060c2b0601040182dc7c05030201036100814c0e6ec71fab583b08bd81373c255c3c371b2e84863c98a4f1e08b74235d14fb5d9c0cd546d9685f913a0c0b2cc5341583bf4b4392e467db96d65b9bb4cb717112f8472e0d5a4d14505ffd7484b01291091c5f87b98883463f98091a0baaae" | xxd -r -p)
hash=$(echo -n "$rootKey" | sha256sum | cut -d ' ' -f 1 | cut -c 1-32)
echo "icp:$hash"
```

## Examples for ICP Mainnet

ICP mainnet reference through the ICP Network Registry [ICRC-a]:
```text
1
```

This results in the following chain id for ICP mainnet:
```text
icp:1
```

ICP mainnet reference through its NNS public key hash:
```text
737ba355e855bd4b61279056603e0550
```

This results in the following chain id for ICP mainnet:
```text
icp:737ba355e855bd4b61279056603e0550
```

## Code Examples For Resolution Through Option 2

We next present source code in various common programming languages for computing the 32-character string used to identify the network when using Option 2.

### JavaScript

```js
const {createHash} = require('crypto');

const rootKey = Buffer.from(
    '308182301d060d2b0601040182dc7c0503010201060c2b0601040182dc7c05030201036100814' +
    'c0e6ec71fab583b08bd81373c255c3c371b2e84863c98a4f1e08b74235d14fb5d9c0cd546d968' +
    '5f913a0c0b2cc5341583bf4b4392e467db96d65b9bb4cb717112f8472e0d5a4d14505ffd7484' +
    'b01291091c5f87b98883463f98091a0baaae', "hex"
);

(async () => {
    const hash = await createHash('sha256').update(rootKey).digest('hex');
    console.log("icp:" + hash.slice(0, 32))
})()
```

### Golang

```go
package main

import (
	"crypto/sha256"
	"encoding/hex"
	"fmt"
	"net/url"

	"github.com/aviate-labs/agent-go"
)

var icp0, _ = url.Parse("https://icp0.io/")

func main() {
	c := agent.NewClient(agent.ClientConfig{Host: icp0})
	status, _ := c.Status()
	hash := sha256.Sum256(status.RootKey)
	hashHexString := hex.EncodeToString(hash[:])
	fmt.Printf("icp:%s", hashHexString[:32])
}
```

## Test Cases

```text
# icp0.io (root_key = "308182301d060d2b0601040182dc7c0503010201060c2b0601040182dc7c05030201036100814c0e6ec71fab583b08bd81373c255c3c371b2e84863c98a4f1e08b74235d14fb5d9c0cd546d9685f913a0c0b2cc5341583bf4b4392e467db96d65b9bb4cb717112f8472e0d5a4d14505ffd7484b01291091c5f87b98883463f98091a0baaae")
icp:737ba355e855bd4b61279056603e0550
```

## Considerations

### Evolving Network Structure

While there is currently one "mainnet" running the Internet Computer, it is important to acknowledge that the network's
structure may change in the future. To accommodate potential network variations, this specification defines, besides the registry-based option, the hash of the root key as the reference. This approach allows for flexibility and adaptation as the Internet Computer continues to evolve and potentially introduces new network configurations, even without registering all of them in the public ICP Network Registry. The option of using a registry has been introduced to simplify the reference for the most-used networks.

## References

- [ICP namespace] FIX
- [CAIP-2](https://github.com/ChainAgnostic/CAIPs/blob/master/CAIPs/caip-2.md)
- [ICRC-a] ICRC-a: ICP Network Registry, 2025. FIX
- [ICP API Status](https://internetcomputer.org/docs/current/references/ic-interface-spec#api-status)
- [ICP Namespace - Reference Implementations](https://github.com/icvc/icp-namespace)

## Rights

Copyright and related rights waived via CC0.
