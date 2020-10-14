---
title: "4.2.1 Account Rules"
slug: "421-membership"
hidden: false
createdAt: "2019-06-24T10:08:56.048Z"
updatedAt: "2020-03-03T08:38:30.604Z"
---
The account models in the blockchain world can be roughly divided into two categories:
1. Public key string. Similar to bitcoin / Ethereum / Tron, a public-private key pair represents an account and encodes the public key into a string in some form. Although the privacy is good, the readability is poor.
2. Registration string. Common in Bitshares / EOS / Iost, users can register a certain length of string, and the public and private keys are hung on the account as permissions. The advantage of this is that the account is readable and user-friendly.

Cocos BCX takes a second approach. Users can register account names with better readability according to their preference. The naming rules of the account are as follows:
  * Account name length min 5, max 63
  * It must start with a lowercase letter, end with a lowercase letter or a number of 0-9, and the middle character can use a lowercase letter or a 0-9 number or a '-' symbol (note that it is not an underscore). Uppercase letters are not supported.  
In addition, according to the naming rules of account names, we divide account names into two categories
  * Basic Name
  * Premium Name 

When the account name meets one of the following conditions, it is Basic Name
  * Contains numbers 0-9
  * Contains special characters-
  * Without a, e, i, o, u, y

There are two kinds of naming which have different charges. The specific fees are as follows:
  Basic name: 0.1 cocos
  Premium Name: 5 cocos,
Charging 0.01 cocos/k base on transaction amount.