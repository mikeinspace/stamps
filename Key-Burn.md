
# Bitcoin Stamps Key Burn Methodology #

Key Burn is a new technique introduced to address concerns with the spendable outputs that encode the art of a #Bitcoin Stamp.

Based on 'NFiniTy' by B0B Smith, Key Burn assigns the spending key of the 'fake multisig' to a burn address when a #Bitcoin Stamp is minted, making the spendable outputs, effectively, unspendable.

Presently, the STAMPCHAIN.IO minting service does this by default by cycling through a series of known burn addresses which can easily be scrutinized to validate that no private key can practically exist. In the future, this library of burn addresses may grow to address adversarial action.

