# Bitcoin Stamps Improvement Proposal:<br/>Octet Linked Graphics & Artifacts (OLGA)

Based on "File Storage in P2WSH Outputs" by JP Janssen<br/><br/>Source: <a href="https://github.com/CounterpartyXCP/cips/blob/master/cip-0033.md">https://github.com/CounterpartyXCP/cips/blob/master/cip-0033.md</a>

# Abstract
Encode a supported Bitcoin Stamp, which is stored in the form of binary octets, in the transaction outputs of non-obvious burn-addresses, along with a Counterparty issuance transaction.

# Supported File-types
Image formats such as PNG, JPG, GIF, and SVG are the focus of the protocol for images and art. Currently, the excluded file formats for Bitcoin Stamps include ['plain', 'octet-stream', 'js', 'css', 'x-empty', 'json'].

# Motivation
Store files immutably on Bitcoin and link them to tokens in a manner that is cheaper than storing them in multisig Bitcoin transactions, as done with Classic Bitcoin Stamps.

# Rationale
The Classic Bitcoin Stamp method stores files as Base64 strings, achieving an efficiency of 6 bits per byte. Base64 encoding converts binary data into an ASCII string format by representing it with 64 different ASCII characters, including A-Z, a-z, 0-9, '+', and '/'. In this encoding, 24 bits (or 3 bytes) of binary data are encoded into 4 Base64 characters, which amounts to 32 bits. Consequently, the total size of 24 bits of binary data, when encoded in Base64, becomes 4 bytes. Since 24 bits of original data are represented by 32 bits (4 bytes), the efficiency is 24/32, which simplifies to 6/8, or 6 bits per original byte. Therefore, in the context of Bitcoin transactions, 3 bytes of binary data consume 4 bytes. Additionally, the Classic Bitcoin Stamp method employs multisig transaction encoding, where only two out of three outputs are utilized for storage.

This Bitcoin Stamps Improvement Proposal (BSIP) introduces a method for storing a file in conjunction with a Counterparty issuance transaction. This is achieved by dividing the file into chunks, which then constitute multiple P2WSH outputs. This approach creates (effectively) permanent UTXOs, wherein a small amount of bitcoin dust is burnt.

Comparing the encoding methods for files of about the same size; a [Stamp of 2853 bytes](https://stampchain.io/asset.html?tx_hash=e6ed0accb29285858217826b2116609ae297e8eaea71fdffd9b87a7934a948b0) and a [OLGA of 2474 bytes](https://jpja.github.io/Electrum-Counterparty/decode_tx?tx=549a5cc4bc189c800f0f9ea01068e8a7fd987c7dadb40c0b6a224d489ed070cc):

| Encoding         | File | Tx    | Tx x  | Dust   | SATS/Byte  |
|------------------|------|-------|-------|--------|------------|  
| Classic Stamp    | 2853 | 8579  | 3.0   | 73,000 | 26         |
| OLGA Stamp       | 2474 | 3613  | 1.5   | 27,306 | 11         |

In a Classic Bitcoin Stamp, the Bitcoin transaction is three times larger than the file, and for each byte of the file, 26 satoshis are burnt. With the OLGA Stamp method, the transaction is only 50% larger than the OLGA-encoded file, and just 11 satoshis are burnt per byte. This makes the OLGA Stamp method more than 50% cheaper than Classic Bitcoin Stamps.

# Definitions
- `STAMP:` - Case insensitive prefix of the Counterparty `asset description` signaling that a file is encoded in the transaction.
- `P2WSH output` - 32 byte script data of a Pay-To-Witness-Script-Hash address output.

# Specification

## File Encoding
- Prepend the file's blob with a two-byte integer signaling the file size.
- Split the blob into 32 byte chunks.
- Append empty bytes to last chunk to make it exactly 32 bytes.
- Convert these to P2WSH addresses and add these as tx outputs.

## Link Token to OLGA-encoded file via Counterparty Issuance
- In the same transaction, insert a valid `op_return` or `multisig` Counterparty issuance transaction.
- Asset description must begin with `STAMP:` (case insensitive).
- Characters after `STAMP:` are currently ignored (reserved for future use). 
- To avoid conflict with Classic Stamps, any base64 data following STAMP: may invalidate the transaction for inclusion in Bitcoin Stamps.
- Asset must be numeric not named or sub-asset of named.

## Block Height Activation
OLGA-encoded Bitcoin Stamps will be considered valid only on, or after, Bitcoin block height 832,000.

## Limitations 
Since a standard node accepts a maximum of 200 outputs, and one is used for an op_return and another for change, the file must fit within 198 P2WSH outputs. This implies a maximum file size of 198 * 32 - 2 = 6334 bytes. The theoretical maximum file size, which can be mined by a node ignoring standard rules, is 256^2 - 2 = 65,536 bytes, limited only by the two-byte size prefix.

# Implementation

PENDING

With the "Counterparty Decoder" you can look up OLGA Stamps and Counterparty CIP33 transactions on [mainnet](https://jpja.github.io/Electrum-Counterparty/decode_tx?tx=549a5cc4bc189c800f0f9ea01068e8a7fd987c7dadb40c0b6a224d489ed070cc) and [testnet](https://jpja.github.io/Electrum-Counterparty/decode_tx?tx=83fc87b4fffd78c8ffd55469206f0f90c0dbbb620b32e8d4adfb7d46148a07f5&network=testnet).

# Copyright
This document is placed in the public domain.
