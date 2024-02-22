# SRC-20 Token Specification on Bitcoin Stamps

The SRC-20 protocol is a cutting-edge specification modeled after BRC-20 utilizing the immutability of Bitcoin Stamps. Earlier versions of SRC-20, in their initial state, were built on top of Counterparty transactions and had specific requirements for an issuance transaction. As of block 796,000, the current specification encodes SRC-20 transactions directly onto BTC, bypassing the use of Counterparty. Consequently, any SRC-20 transactions created on Counterparty after block 796,000 will be considered invalid. Counterparty was initially used as a proof of concept while we developed a direct-to-BTC method, which optimizes transaction size and reduces the cost of SRC-20 transactions.

# Additional SRC-20 Specifications

https://github.com/hydren-crypto/stampchain/blob/main/docs/src20.md


## SRC-20 Indexing Reference

The Official Bitcoin Stamps Indexing reference API: https://stampchain.io/docs 