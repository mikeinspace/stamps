# Bitcoin Stamps Improvement Proposal:<br/>Octet Linked Graphics & Artifacts

Based on "File Storage in P2WSH Outputs" by JP Janssen<br/><br/>Source: <a href="https://github.com/CounterpartyXCP/cips/blob/master/cip-0033.md">https://github.com/CounterpartyXCP/cips/blob/master/cip-0033.md</a>

# Abstract
Encode a supported `file-type` saved in binary octets in tx outputs of non-obvious burn-addresses along an `issuance` transaction.

# Supported File-types

Presently, most image formats (PNG,JPG,GIF,SVG) are supported. Executables are not supported.

# Motivation
Store files onchain and link these to tokens in a way which

1. is cheaper than traditional Bitcoin Stamps,
2. is less of a burden on node operators

# Rationale
The "Stamp" method involves storing the file as a base64 string with an efficiency of only 6 bits per byte. Moreover, multisig encoding is used, where only two out of three outputs are used for storage. For the node operator, stamps cause redundant file storage, where the file first is stored in the bitcoin data and then multiple times in the Counterparty database.

This CIP introduces a method for storing a file along an `issuance` transaction. This is achieved by breaking the file into chunks that make up multiple P2WSH outputs. This makes (effectively) permanent UTXOs where some bitcoin dust is burnt.

Comparing the encoding methods for files of about the same size; a [Stamp of 2853 bytes](https://stampchain.io/asset.html?tx_hash=e6ed0accb29285858217826b2116609ae297e8eaea71fdffd9b87a7934a948b0) and a [CIP33 of 2474 bytes](https://jpja.github.io/Electrum-Counterparty/decode_tx?tx=549a5cc4bc189c800f0f9ea01068e8a7fd987c7dadb40c0b6a224d489ed070cc):

| Encoding       | File | Tx    | Tx x  | Dust   | Dust x |
|----------------|------|-------|-------|--------|--------|  
| STAMP (CIP26)  | 2853 | 8579  | 3.0   | 73,000 | 26     |
| P2WSH (CIP33)  | 2474 | 3613  | 1.5   | 27,306 | 11     |

With Bitcoin Stamps the Bitcoin transaction is three times larger than the OLGA-encoded file, and for each byte of the file 26 satoshis are burnt. With this method the tx is just 50% larger than the OLGA-encoded file, and only 11 sats are burnt per byte. This makes this method more than 50% cheaper than traditional Bitcoin Stamps.

# Definitions
- `STAMP:` - Case insensitive prefix of `asset description` signaling that a file is encoded in the transaction.
- `filename` - Unicode filename including file extension.
- `P2WSH output` - 32 byte script data of a Pay-To-Witness-Script-Hash address output.

# Specification

## File Encoding
- prepend the file's blob with a two-byte integer signaling the file size.
- split the blob into 32 byte chunks.
- append empty bytes to last chunk to make it exactly 32 bytes.
- convert these to P2WSH addresses and add these as tx outputs.

## Link Token to File via Issuance
- in the same transaction, insert a valid `op_return` Counterparty issuance.
- asset description must begin with `STAMP:` (case insensitive) followed by filename.
- asset must be numeric not named or sub-asset of named.

## Block Height Activation
- OLGA-encoded Bitcoin Stamps will only be considered valid on, or after, block height: 832,000

## Limitations 
Since a standard node accepts maximum 200 outputs, and one is used for op_return and one for change, the file must fit 198 P2WSH outputs. This implies a max file size of `198*32 - 2 =` 6334 bytes. The theoretical max filesize (that can be mined by a node ignoring standard rules) is `256^2 - 2 =` 65,536 bytes, only limited by the two-byte size prefix.

# Implementation

The "XCP Opreturn Builder for Electrum" has [CIP33 Token Issuance](https://jpja.github.io/Electrum-Counterparty/cip33_issuance.html) and [CIP33 Broadcast](https://jpja.github.io/Electrum-Counterparty/cip33_broadcast.html) forms. They work with Bitcoin mainnet and testnet. Read instructions.

With the "Counterparty Decoder" you can look up CIP33 transactions on [mainnet](https://jpja.github.io/Electrum-Counterparty/decode_tx?tx=549a5cc4bc189c800f0f9ea01068e8a7fd987c7dadb40c0b6a224d489ed070cc) and [testnet](https://jpja.github.io/Electrum-Counterparty/decode_tx?tx=83fc87b4fffd78c8ffd55469206f0f90c0dbbb620b32e8d4adfb7d46148a07f5&network=testnet).

# Copyright
This document is placed in the public domain.
