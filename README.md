# CAT-21 Protocol Specification

![CAT-21 Banner](assets/cat21-banner.svg)

## Overview

CAT-21 is a protocol that associates unique cat art with individual satoshis on Bitcoin.

## Terminology

The following terms are used throughout this specification:

1. **Sat**: The smallest unit of Bitcoin. Due to the Bitcoin halving schedule, there will only ever be exactly 2,099,999,997,690,000 satoshis.
2. **Ordinal**: A sat with a unique sequential number. If counted, every sat is an ordinal.
3. **CAT-21 ordinal**: An ordinal that received one or more cats through a CAT-21 mint transaction (`nLockTime` set to `21`). Once an ordinal receives a cat, it is referred to as a CAT-21 ordinal from that point on.
4. **Cat**: The digital artifact defined by the CAT-21 protocol. Each cat is revealed through a CAT-21 mint transaction and intrinsically linked to a unique deterministic image derived from the transaction hash and block hash. A single CAT-21 ordinal can carry multiple cats.

## The Protocol

Collecting, gifting, and trading form social connections. Art makes every satoshi more valuable. CAT-21 gives owners something to cherish and build communities around.
The CAT-21 protocol is founded on a genesis act, validated by consensus, and manifested through proof of work.

### Genesis

For a long time, no one had ever set `nLockTime` to `21` in all of Bitcoin's history. The creator of this protocol performed the first such transaction to secure the right to give it meaning. The protocol was then developed through this specification and an initial mint phase. First is first.

### Consensus

Bitcoin is consensus. Ordinal Theory is consensus. If we agree to count sats, they become ordinals. If we agree that `nLockTime=21` reveals cats, it does. By setting `nLockTime` to `21`, the minting entity enters this reality. No authority enforces this. The protocol exists because its participants choose to follow it. This is the same mechanism that gives Bitcoin its value.

### Proof of Cat Work

Bitcoin's value and security are based on accumulated proof of work. Every new block strengthens the network. The same principle applies to CAT-21. Every mint transaction strengthens the protocol by proving that entities accept and care about it. This proof can only grow. It can never get weaker, even during times of no activity. The Proof of Cat Work is calculated by accumulating all fees spent to miners across all CAT-21 mint transactions.

### Minting

A CAT-21 mint transaction has its `nLockTime` set to `21`. No exceptions.

The mint transaction should be a payment to a pay-to-taproot (P2TR) address (which starts with `bc1p`) to ensure the best compatibility with existing Ordinals-aware wallets. However, this is not a strict requirement. Other types of addresses may be used, but P2TR is preferred.

For a mint transaction, only the first output is important. It defines the first owner of the cat. All other inputs and outputs are ignored. Every CAT-21 mint transaction reveals exactly one cat.

### Ownership

A CAT-21 mint assigns a new cat to the first sat of the first output of the mint transaction, making it a CAT-21 ordinal. The entity that controls it owns the cat. Ownership of a cat shall be determined solely by control of its CAT-21 ordinal. As the CAT-21 ordinal moves through transactions, ownership follows.

Control is proven by the ability to spend the output containing the CAT-21 ordinal. CAT-21 ordinals move through transactions on a first-in, first-out basis. All tracking rules of Ordinal Theory apply to the CAT-21 protocol. CAT-21 ordinals and therefore cats shall only be transferred on-chain. No other form of agreement is recognized by this protocol. The ledger is the sole arbiter of ownership.

### Cat Identity

Each cat has a unique identity, secured by proof of work. Its identity is determined by `SHA256(transactionHash + blockHash)`, where the block hash is unpredictable. Unpredictability is in the nature of every cat. No entity can choose their cat. The cat was always there, waiting in the math. It can only be revealed. Every Bitcoin transaction that does not set `nLockTime` to `21` is a cat that will never be revealed. The choice to mint is the choice to reveal.

This seed formula is immutable. Changing it would alter the identity of every existing cat. The art style is defined by the genesis cat holder (see Governance).

### Scarcity and Supply

There is no artificial supply cap. The supply of cats is unlimited. A single CAT-21 ordinal can carry multiple cats through repeated minting. The number of CAT-21 ordinals is bounded by the total supply of spendable satoshis. Any entity can mint a cat at any time. No permission is required. This property is enforced by the Bitcoin network itself. A protocol cannot be capped. A protocol cannot be stopped.

Scarcity in CAT-21 is a product of time. Cat #0 can never be minted again. Earlier cats receive lower numbers, and lower numbers can never be assigned again. Categories such as sub1k, sub10k, and sub100k emerge naturally as more cats are minted. Every new mint makes all previous cats more scarce. You are never late. The CAT-21 protocol celebrates every newly revealed cat.

### Immutability

Bitcoin is the most durable ledger ever created. The CAT-21 protocol inherits this property. CAT-21 cats can't be destroyed. They are immutable on the Bitcoin blockchain. If a CAT-21 ordinal becomes unspendable, the cat still exists but no longer has an owner. (The cat is free!)


## Governance

<img src="assets/genesis-cat.svg" title="Genesis cat" width="25%" align="right">

Cat #0 is the Genesis Cat. Its mint transaction is the first Bitcoin transaction with `nLockTime` set to `21` in all of Bitcoin's long history. This event occurred at block height 824,205. In ancient Egypt, the Genesis Cat would have sat beside Bastet herself, adorned with gold, guarded by priests, worshipped as divine. The CAT-21 protocol was not written to summon her. It was written to capture a glimpse of her greatness. The most magnificent cat that will ever exist. All others are merely echoes of her perfection. Meow!

### Authority

The entity that controls sat 596964966600565 according to Ordinal Theory is the sole authority over protocol changes, future development, and the definition of the cat art. A future holder has full authority to adjust any governance decision. Governance updates shall be published as inscriptions on sat 596964966600565 and become effective after 21 confirmations.

### Why governance exists

The visual representation can never fully capture the true identity of a cat. Any image is an interpretation of the underlying seed. Future generations may find better ways to honor the cats. This is why the art is governable.

### Decisions by the current genesis cat holder

The following decisions are ossified by the first genesis cat holder. They can only be changed through a governance update on-chain (see above). The first holder considers the cats perfect as they are. Only the genesis cat holder decides when and to whom the genesis cat is transferred. One day, when the genesis cat finds a new guardian, these decisions may evolve.

**Art:** The first genesis cat holder has chosen pixelated cat images as the visual representation. The images are inspired by the famous [Mooncat Algorithm](https://github.com/ponderware/mooncatparser/), adapted to meet new requirements. The existing traits from the original Ethereum Mooncats are utilized, with additional new traits such as red, green, and blue laser eyes and an orange background. The fee rate of the mint transaction determines the color of the cat. Higher fee rates produce rarer colors. The images are generated in SVG format with square dimensions. The artwork is defined by the reference implementation in the [ordpool-parser repository](https://github.com/ordpool-space/ordpool-parser). All other implementations should result in the exact same visual appearance to maintain consistency across the protocol.

**Ecosystem:** The official website is https://cat21.space. CAT-21 mint transactions in the mempool are displayed on https://ordpool.space. The official indexer is [cat21-ord](https://github.com/ordpool-space/cat21-ord), a fork of the [ord client](https://github.com/ordinals/ord) that indexes `nLockTime=21` transactions and provides sat tracking, transfer tracking, and a REST API.


## Credits

* **1440000bytes** had the initial idea to use the `nLockTime` field for data storage. See [Inscriptionless Inscriptions](https://delvingbitcoin.org/t/inscriptionless-inscriptions/785) on Delving Bitcoin.
* **HausHoppe** created the protocol, the reference implementation, the indexer, and the official ecosystem. First ever genesis cat holder.
* **ethspresso** designed the laser eyes and crown traits and gave very valuable feedback.
* **LightRider5** created the initial PSBT minting script and gave very valuable feedback.
* The original [Mooncats](https://mooncatrescue.com/) (2017) paved the way for on-chain generative cat art. CAT-21 carries their legacy to Bitcoin.

## Appendix

In this document, the terms "shall" and "should" are used to convey different levels of requirement:
- "Shall" is used to indicate requirements strictly to be followed in order to conform to the document and from which no deviation is permitted.
- "Should" is used to indicate that among several possibilities one is recommended as particularly suitable, without mentioning or excluding others, or that a certain course of action is preferred but not necessarily required.
