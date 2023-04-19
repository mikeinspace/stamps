
# Bitcoin Stamps Key Burn Methodology #

Key Burn is a new technique introduced to address concerns with the spendable outputs that encode the art of a #Bitcoin Stamp.

Based on 'NFiniTy' by B0B Smith, Key Burn assigns the spending key of the 'fake multisig' to a burn address when a #Bitcoin Stamp is minted, making the spendable outputs, effectively, unspendable.

Presently, the STAMPCHAIN.IO minting service does this by default by cycling through a series of known burn addresses which can easily be scrutinized to validate that no private key can practically exist. In the future, this library of burn addresses may grow to address adversarial action.

The very first example of the Key Burn method in use (coined 'NFiniTy') is here: https://xchain.io/asset/SPENDME. By analyzing its scriptPubKey, you will notice that the spendable multisig key address is: '<code>022222222222222222222222222222222222222222222222222222222222222222</code>' which does not have a known Private Key based on the improbable pattern.

The second example of the Key Burn method in use (a valid #Bitcoin Stamp) is here: https://xchain.io/asset/A808022222222222222. Once again, you can examine the scriptPubKey here: https://blockstream.info/tx/f2ac4cf5230e3033968c25d0a4e3f05ea7ba36429dec7e560ae770a732fd7ae8?expand to verify that the spendable multisig key address is: '<code>022222222222222222222222222222222222222222222222222222222222222222</code>'

# Library of current Key Burn addresses: #

<code>022222222222222222222222222222222222222222222222222222222222222222</code>
<code>033333333333333333333333333333333333333333333333333333333333333333</code>
<code>020202020202020202020202020202020202020202020202020202020202020202</code>
<code>030303030303030303030303030303030303030303030303030303030303030303</code>

Special Thanks to B0B Smith, 
