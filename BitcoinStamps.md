
# Bitcoin Stamps

Storing "Art on the Blockchain" as a method of achieving permanence is often a misnomer in the NFT world. Most NFTs are merely image pointers to centralized hosting or stored on-chain in prunable witness data. We propose a method of embedding base64-formatted image data using transaction outputs in a novel fashion.

The means by which this is achieved is encoding an image's binary content to a base64 string, placing this string as a suffix to `STAMP:` in a transaction's description key, and then broadcasting it using the Counterparty protocol onto the Bitcoin ledger. The length of the string means that Counterparty defaults to bare multisig, thereby chunking the data into outputs rather than using the limited (and prunable) OP_RETURN. By doing so, the data is preserved in such a manner that is impossible to prune from a fullnode, preserving the data immutably forever.

Given the cost of preserving data in this manner, we suggest the following guidance: 24x24 pixel, 8-colour-depth PNG or GIF. The constraints of this "canvas" are ideal for pixel art. In particular, the CryptoPunks use a native resolution of 24x24 pixels. While the technical specifications are open to interpretation and reinvention, inclusion within the Bitcoin Stamps directory will rely on a number of consensus rules on Bitcoin Stamps which are distinct from any other cases of using P2SH to encode data in this manner.

Bitcoin Stamps will be numbered based on the transaction timestamp. This is to ensure that the Bitcoin Stamps directory is ordered chronologically. The first Bitcoin Stamp will be the first transaction to include the `STAMP:` string with a valid base64 string appended in the description key, and so on. A transaction with an invalid or indecipherable base64 string will not be considered a Bitcoin Stamp. The Bitcoin Stamp number will begin at zero and continue indefinitely.

## What Makes a Bitcoin Stamp?

A Bitcoin Stamp is a Counterparty transaction which contains a valid `STAMP:base64` string in the description key. STAMPS can be decoded directly from the original Bitcoin transaction. In order for speed of processing and to eliminate needs for indexing, we are utilizing Counterparty API to decode the original Bitcoin transactions. Once the decoding is complete, we upload the images to stampchain.io for consumption via web applications as a convenience. It is intended that anyone may decode these transactions and interpret the underlying image data for rendering on any application. 

## Bitcoin Stamps abide by the following rules:


- A Bitcoin Stamp must be a numerical asset, for example: [A1997663462583877600]
- A Bitcoin Stamp can be created from a previously existing numerical asset which was not previously a STAMP. This is accomplished by updating the asset to include the `stamp:base64` string in a new transaction.
- Bitcoin Stamps cannot be duplicated on the same asset. For example, if one asset is a STAMP, then by simply changing the description field to a new base64 string, it will not become a new STAMP. However, the new `STAMP:` transaction will be created on the blockchain. The new transaction will just not be indexed by the official STAMPS project. This is intended to keep them in a one-to-one relationship to the first created STAMP.
- The image data must be in either jpg, png, gif or webP format and encoded in base64.

**Recommended Format:**

- `STAMP:<base64 data>`

Example:

- `STAMP:iVBORw0KGgoAAAANSU...`

## Potential Future State formatting:

Warning: Do not try this until its actually approved. Doing so may result in an invalid STAMP as plans may change.

- `STAMP:data:image/png;base64,iVBORw0KGgoAAAANSU...`

## Decoding a Bitcoin Stamp

A raw bitcoin transaction may be decoded using tools such as:

https://jpja.github.io/Electrum-Counterparty/decode_tx.htm

This will reveal the description field of the STAMP transaction. The description field will contain the base64 string. This string can be decoded using any base64 decoder. 

## Absence of MIME-type and encoding

Our rationale for excluding both the MIME-type and encoding goes as follows:

- The fewer the bytes the better.
- Given the limited scope of acceptable file formats, we are confident that decoding them accurately based on the base64 string alone is trivial.
- We are only interested in decoding base64, so if the string does not conform to valid base64 it is rejected. Therefore, specification of the encoding is unnecessary.

This all pertains to current state. The future-state proposal would require a MIME-type like 'text/plain' for the auxilary content to be decoded.

## XCHAIN-specific markup

While no specific markup should be required, STAMPS are purposely designed to be very small in the range of 24x24 pixels. While they can be presented at this size or even scaled-up using the traditional method, the user experience would be sub-optimal. Using a few simple CSS rules will optimize the rendering. Eg: image-rendering: pixelated;

Visual example of pixel art scaling without image degradation: https://i.imgur.com/CGLqw11.jpg

## Bitcoin Stamps Indexing Reference

The official stamp indexing reference is here: https://stampchain.io/stamp.json This may be generated and hosted by anyone using the sample code in this project. 

## Trading

Users are able to trade the token on the Counterparty DEX, Dispensers or OTC or any other method as traditional Counterparty assets.

## The Ecosystem

- Main Directory: [https://STAMPCHAIN.IO](https://stampchain.io/)
- 3rd Party Directory: https://kaleidoscopexcp.com/stamps/
- Marketplace: https://scarce.city/marketplace/digital?refinementList%5Bset%5D%5B0%5D=stampchain

## Future Partnerships

There have been ongoing discussions with Emblem, Hiro Wallet and Token.Art dev teams. All expressed enthusiasm about the potential for integration.

