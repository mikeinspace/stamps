
# STAMPS: A Protocol for Storing Images On-Chain in Spendable Outputs Immutably on Bitcoin

Storing "Art on the Blockchain" as a method of achieving permanence is often a misnomer in the NFT world. Most NFTs are merely image pointers to centralized hosting or stored on-chain in prunable witness data. We propose a method of embedding base64-formatted image data using unspendable outputs in a novel fashion.

The means by which this is achieved is by encoding an image's binary content to a base64 string, placing this string as a suffix to `stamp:` in a transaction's description key, and then broadcasting it using the Counterparty protocol onto the Bitcoin ledger. The length of the string means that Counterparty defaults to P2SH, thereby chunking the data into outputs rather than using the limited (and prunable) OP_RETURN. By doing so, the data is preserved in such a manner that is impossible to prune from a fullnode, preserving the data immutably forever.

Given the cost of preserving data in this manner, we suggest the following guidance: 24x24 pixel, 8-colour-depth PNG. The constraints of this "canvas" are ideal for pixel art. In particular, the CryptoPunks use a native resolution of 24x24 pixels. While the technical specifications are open to interpretation and reinvention, inclusion within the STAMPS directory will rely on a number of consensus rules on STAMPS which are distinct from any other cases of using P2SH to encode data in this manner.

STAMPS will be numbered based on the transaction timestamp. This is to ensure that the STAMPS directory is ordered chronologically. The first STAMP will be the first transaction to include the `stamp:` string with a valid base64 string appended in the description key, and so on. A transaction with an invalid or indecipherable base64 string will not be considered a stamp. The STAMP number will begin at zero and continue indefinitely.


## What Makes a Stamp?

A STAMP is an immutable broadcast transaction which contains a valid `stamp:base64` string in the description key. STAMPS can be decoded directly from the original Bitcoin transaction. In order for speed of processing and to eliminate needs for indexing, we are utilizing Counterparty API to decode the original Bitcoin transactions. Once the decoding is complete, we upload the images to stampchain.io for consumption via web applications as a convenience. It is intended that anyone may decode these transactions and interpret the underlying image data for rendering on any application. 

Stamps abide by the following rules:

- A STAMP must be a numerical asset, for example: [A1997663462583877600]
- A STAMP can be created from a previously existing numerical asset which was not previously a stamp. This is accomplished by updating the asset to include the `stamp:base64` string in a new broadcast transaction.
- STAMPS cannot be duplicated on the same asset. For example, if one asset is a stamp, then by simply changing the description field to a new base64 string, it will not become a new stamp. However, the new `stamp:` transaction will be created on the blockchain. The new transaction will just not be indexed by the official stamp project. This is intended to keep them in a one-to-one relationship to the first created stamp.
- The image must be encoded in base64.
  - "stamp:iVBORw0KGgoAAAANSUhEUgAAAAwAAAAMBAMAAACkW0HUAAAAElBMVEUAAACui2EAAAC7s6akloG2n4LfldcbAAAAAXRSTlMAQObYZgAAAClJREFUCNdjQAdKCiCSMVAQTAmCKSYnE5CooqExRFARLoeghCD6BIAEAG00AqOK03PuAAAAAElFTkSuQmCC"

- Stamps can be a subasset to an existing Counterparty asset given that it follows the above formatting.

## Decoding a STAMP

A raw bitcoin transaction may be decoded using tools such as:

https://jpja.github.io/Electrum-Counterparty/decode_tx.htm

This will reveal the description field of the STAMP transaction. The description field will contain the base64 string. This string can be decoded using any base64 decoder. 

## Example

**This broadcast**: https://xchain.io/tx/2262968 includes a properly formated stamp:base64 string and is considered stamp #0. Its transaction hash: [17686488353b65b128d19031240478ba50f1387d0ea7e5f188ea7fda78ea06f4](https://blockstream.info/tx/17686488353b65b128d19031240478ba50f1387d0ea7e5f188ea7fda78ea06f4) 

The official stamp indexing reference is here: https://stampchain.io/stamp.json This may be generated and hosted by anyone using the sample code in this project. 
## Trading

Users are able to trade the token on the Counterparty DEX, Dispensers or OTC or any other method as traditional Counterparty assets.

