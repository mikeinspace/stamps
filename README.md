# STAMPS Protocol: Trading Immutable Art on the Blockchain

Storing "Art on the Blockchain" as a method of achieving "permanance" is often a misnomer in the NFT world. Most NFTs are merely image pointers to centralized hosting or stored in prunable witness data.

We propose a method of embedding base64-formatted image data using unspendable outputs in a novel fashion.

The means by which this is achieved is by first HEX-encoding an image's base64 string (HEX-encoding acts to preserve the data string from unintended truncation/conversion by wallet software.) and then broadcasting it using the Counterparty protocol. The length of the string will necessitate that Counterparty defaults to P2SH thereby chunking the data into outputs rather than using the limited (and prunable) OP_RETURN.  By doing so, the data is preserved in such a manner that makes pruning a full-node impossible. The data is preserved immutably forever.

# Formatting

Given the cost of preserving data in this manner we suggest the following guidance: 24x24 pixel, 8-colour-depth PNG. The constraints of this "canvas" are ideal for pixel art. In particular, the CryptoPunks use a native resolution of 24x24 pixels. While the technical specifications are open to interpretation and reinvention, inclusion within the STAMPS directory will rely on a number of consensus "rules" on STAMPS which is distinct from any other cases of using P2SH to encode data in this manner.

# How does trading work?

Once a compliant broadcast is completed, a user will need to create a Counterparty asset from the same address, preferably within the next few blocks. The asset name, supply and divisibility is entirely at the discretion of the user, however the transaction hash of the broadcast transaction must be included within the Description field prefaced by stamp:. The following method is recommended as a means by which "legacy" compatibility can be maintained with the popular xchain.io, but in terms of STAMPS consensus, only the broadcast transaction hash is required.

Recommended format: imgur/2lPpwj6.png; stamp:efc9ad4ef56d45811777b29fe370900e5de1dd71746448d067e5d92e7361fae8
Minimum required format: stamp:efc9ad4ef56d45811777b29fe370900e5de1dd71746448d067e5d92e7361fae8


