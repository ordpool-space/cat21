# CAT-21 Protocol Specification

![Orange Banner](assets/cat21-banner.svg)

## Overview

CAT-21 is a new protocol developed to operate on top of the Bitcoin blockchain and leverages the Ordinals concept.
It introduces a unique way of representing and transacting digital assets, specifically pixelated cat images, in a decentralized manner.
CAT-21 transactions are identified using the `nLockTime` field in a Bitcoin transaction, with a specific focus on the value `21`.

## Protocol Rules

In this document, the terms "shall" and "should" are used to convey different levels of requirement:
- "Shall" is used to indicate requirements strictly to be followed in order to conform to the document and from which no deviation is permitted.
- "Should" is used to indicate that among several possibilities one is recommended as particularly suitable, without mentioning or excluding others, or that a certain course of action is preferred but not necessarily required.

### Identification of a CAT-21 Mint Transaction

1. **nLockTime Value**: A transaction is recognized as a CAT-21 mint if its [`nLockTime`](https://en.bitcoin.it/wiki/NLockTime) value is set to `21`. This is a hard requirement, meaning it **shall** be followed for the transaction to be acknowledged as a CAT-21 mint.
2. **Transaction Type**: A CAT-21 mint transaction should be a payment to a pay-to-taproot (P2TR) address (which starts with `bc1p`). This recommendation is made to ensure consistency within the protocol and to ensure the best compatibility with existing Ordinals-aware wallets. However, this is not a strict requirement. Other types of addresses may be used, but P2TR is preferred.
3. **First Output Matters**: For a mint transaction, only the first output is important. It defines the recipient of the CAT-21 mint. All other inputs and outputs are ignored. Therefore, every Bitcoin transaction can create exactly one cat.
4. **Ownership**: The ownership of a CAT-21 ordinal is determined by the entity controlling the first Satoshi in the transaction output, in line with the [Ordinal Theory](https://docs.ordinals.com/overview.html).
5. **Image Association**: Each CAT-21 ordinal is intrinsically linked to an image.
  This image is generated based on the transaction ID of the mint transaction, creating a unique pixelated cat image.

### Transferring CAT-21 ordinals

1. CAT-21 can be transferred using standard Bitcoin transactions.
2. The new owner of a CAT-21 ordinal is the entity controlling the first Satoshi of the mint transaction output.
   This is the same concept that applies to Ordinals and Inscriptions – but for digital cat artifacts!

### Immutability

1. Digital CAT-21 ordinals can't be destroyed, they are immutable on the Bitcoin blockchain.
2. If a CAT-21 ordinal is sent to a "burner" address, the cat still exists but no longer has an owner. (The cat is free!)


## Library and Tools

<img src="assets/genesis-cat.svg" title="Genesis cat" width="25%" align="right">

### Image Representation

Each CAT-21 ordinal is intrinsically linked to a generated image. 
The creation of generative cat art is a fundamental part of this protocol.
The pixelated cat images are inspired by the famous [Mooncat Algorithm](https://github.com/ponderware/mooncatparser/), adapted to meet new requirements.

* **Seed**: The seed for generating the image and traits is retrieved from the concatenated `transactionId` and `blockId`, hashed using the SHA-256 algorithm. 
  By using this method, the characteristics of each CAT-21 ordinal will only be determinable after the transaction is included in a block, 
  thus preventing anyone from generating transactions until they get a desirable outcome.
  This approach ensures fairness and unpredictability in the distribution of rare traits.
* **Format**: The images should be generated in a web-friendly, scalable format, with SVG being preferred.
* **Traits**: The existing traits from the original Ethereum Mooncats are utilized, with additional new traits such as red, green, and blue laser eyes and an orange background. 
* **Dimensions**: The dimensions of the generated images shall be squares.
* **Storage**: Images and Traits are not stored on the blockchain but are generated on-demand using the concatenated `transactionId` and `blockId` as a seed.
* **Reference Implementation**: The artwork is defined by the reference implementation in the [ordpool-parser repository](https://github.com/haushoppe/ordpool-parser) (the engine that parses digital artifacts on ordpool.space). 
  All other implementations should result in the exact same visual appearance to maintain consistency across the protocol.

### Locating CAT-21 Mint Transactions

Existing CAT-21 Mint Transactions can be discovered using Blockchair's search functionality.
The following links provide pre-configured queries according to CAT-21 protocol rules:

1. [Query for Mainnet](https://blockchair.com/bitcoin/transactions?q=lock_time(21)#f=hash,block_id,input_count,output_count,time,lock_time)
2. [Query for Testnet](https://blockchair.com/bitcoin/testnet/transactions?q=lock_time(21)#f=hash,block_id,input_count,output_count,time,lock_time) 

Existing CAT-21 Mint Transactions can also be located via the [Bitquery Grapqhl API](https://ide.bitquery.io/):

```
query txns {
  bitcoin {
    transactions(txLocktime: {is: 21}) {
      hash
      txLocktime
      block {
        height
      }
    }
  }
}
``` 

These queries are designed to filter transactions based the `nLockTime` set to `21`.

The official indexer at https://backend.cat21.spaces uses the Blockchair API as a source of truth and
enriches this information with sat ranges from the Ord API.

### CAT-21 Ecosystem

* The official website is https://cat21.space
* CAT-21 Mint Transactions in the Mempool are displayed on https://ordpool.space  _(at launch date)_
* Confirmed CAT-21 Mint Transactions are displayed on https://ordimint.com  _(at launch date)_
* MORE LINKS WITH COMPATIBLE SERVICES HERE (PRs welcome!)


## Future Development

### Open Discussion

The protocol may be expanded to include additional features based on community feedback and technological advancements.
Please make a pull request to the [cat-21 repository](https://github.com/haushoppe/cat-21) to participate in the open development.

The CAT-21 protocol introduces a novel way of digital asset representation and transaction on the Bitcoin blockchain, inviting marketplaces, wallets, and indexers to adopt and integrate this disruptive protocol in the broader ecosystem!

### Roadmap

1. ✅ Development of a sound Protocol Specification (this document)
2. ✅ Reference implementation in the [ordpool-parser repository](https://github.com/haushoppe/ordpool-parser)
3. ✅ Open-Source Indexer for CAT-21 ordinals in [cat-21-indexer repository](https://github.com/haushoppe/cat-21-indexer)
4. Development of a simple script (TypeScript preferred) that creates a PSBT to mint a CAT-21 ordinal
6. Open invitation of the Ordinals ecosystem to adapt the protocol in their products!


## Credits

* [@1440000bytes](https://twitter.com/1440000bytes) had the initial idea to use the `nLockTime` field for data storage. See this this [twitter conversation](https://twitter.com/HausHoppe/status/1741789980551213207).
* [@HausHoppe](https://twitter.com/HausHoppe) adapted the idea and created this repository to engage collaboration and discussions on the protocol. He also developed the parser, the indexer and the official website.
* [@ethspresso](https://twitter.com/ethspresso) designed the laser eyes and gave very valuable feedback.
* [@LightRider5](https://twitter.com/LightRider5) created the PSBT script and gave very valuable feedback.
