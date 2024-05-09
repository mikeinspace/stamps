<h1>STAMP VAULT</h1>
<p><strong>A method of permanently securing Ordinal Sats within a Bitcoin Stamp vault</strong></p>

<p>Introduction: Ordinals introduced a novel method of instantiating individual "Satoshis" when viewed through the lens of "Ordinal theory". However, these atomized "Sats" have proven to be quite fragile in that they can easily be spent by mistake. This is due to their very nature of being tied to specific UTXOs which the Bitcoin protocol has no awareness of. Ordinal theory is an overlay "metaprotocol" that operates by its own rules, but relies on lower-level transfer of UTXOs at the base layer. In contrast, Counterparty assets utilize an account-balance model wherby the ruleset operates independantly of specific UTXOs.</p>

<p>Bitcoin Stamps added a novel twist to the traditonal Counterparty approach by adopting the account-balance model but opting to store data within transaction outputs rather than OP_RETURN messages. What this means is that Ordinal theory utilizes UTXOs to determine ownership while Bitcoin Stamps utilizes UTXOs for data storage. It also presents a unique opportunity to leverage aspects of both protocols in order to provide a robust method of permanently storing Ordinals within Bitcoin Stamp vaults.</p>

<p>Bitcoin Stamps (OLGA-encoding) places the Counterparty  OP_RETURN 

jpja olga stamp tool puts the op return in position 2 (vout:1) so the counterparty 'ownership' is 'burnt' during the issuance which is a nice trick .. but as I understand ordinal theory it's the first output that is important  

in counterparty as I understand it  the position of the op return is used to control a transfer of ownership 

so if you want to retain a counterparty ownership of a olga stamp you put the op return in position 1 (vout:0) 

I am aware counterparty 'ownership' can be a contentious issue
