---
title: "4.2 Account"
slug: "42-account"
hidden: false
createdAt: "2019-06-24T10:07:13.509Z"
updatedAt: "2019-06-24T10:07:13.509Z"
---
The account modes on blockchain are classified into:
1.	Public key string. It is similar to the public-private key pair on the Bitcoin/Ethereum/TRON blockchain, of which the public key is encoded into a string in certain form. It is highly private but poorly readable.
2.	Registration string. It is common in BitShares/EOS/IOST, where users can register a string of a certain length. The public and private keys are attached to the account. This kind of account is more readable and user friendly.

Cocos-BCX takes the second approach, allowing users to register accounts according to their preferences with the cli_wallet tool or other wallets.