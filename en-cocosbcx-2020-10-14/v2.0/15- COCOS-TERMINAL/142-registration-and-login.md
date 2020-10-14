---
title: "15.2 Registration and Login"
slug: "142-registration-and-login"
hidden: false
createdAt: "2019-06-24T06:46:12.149Z"
updatedAt: "2020-03-02T09:33:11.744Z"
---
[block:api-header]
{
  "title": "Account"
}
[/block]

## Create an Account
There are two modes for account creating: wallet mode and account mode.

* In account mode, an account shall be created by entering a valid username and password(as shown below). 
The account name usually contains letters and numbers within 5 to 63 bits and start with lowercase letters.
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/d3e8cbe-f0539f0-_2019-06-05_7.04.25.png",
        "f0539f0-_2019-06-05_7.04.25.png",
        1398,
        603,
        "#3d4046"
      ]
    }
  ]
}
[/block]
* In wallet mode, an account shall be created by entering a username and wallet password(as shown below). Note: The password in this mode is used to encrypt the wallet, which contains the private key of the account. Please remember to back up your wallet after registration!
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/8d4d3c2-b64100f-_2019-06-05_7.06.03.png",
        "b64100f-_2019-06-05_7.06.03.png",
        750,
        580,
        "#47494c"
      ]
    }
  ]
}
[/block]
## Login 

There are four login modes: username (account mode), import private key (account mode), import private key (wallet mode), key file (wallet mode).

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/f5f87a2-ca5db53-_2019-06-05_7.06.51.png",
        "ca5db53-_2019-06-05_7.06.51.png",
        707,
        483,
        "#66686b"
      ]
    }
  ]
}
[/block]
    * Username Login(Account Mode) 
    Enter the username and password, and click confirm.
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/5d4d846-4087a69-_2019-06-05_7.08.17.png",
        "4087a69-_2019-06-05_7.08.17.png",
        1336,
        616,
        "#3d4146"
      ]
    }
  ]
}
[/block]
  * Import Private Key Login(Account Mode)
    Enter the private key and password of the temporary wallet, and click submit.
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/4b173fa-bc83df9-_2019-06-05_7.09.08.png",
        "bc83df9-_2019-06-05_7.09.08.png",
        1326,
        613,
        "#3e4146"
      ]
    }
  ]
}
[/block]
  * Import Private Key Login(Wallet Mode)
    Enter the private key and password of the temporary wallet, and click submit.

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/cd37246-5c3d8a1-_2019-06-05_7.09.08.png",
        "5c3d8a1-_2019-06-05_7.09.08.png",
        1326,
        613,
        "#3e4146"
      ]
    }
  ]
}
[/block]
    * Key file Login(Wallet Mode)
    Click import the backup key.file.

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/1f18079-3bace09-_2019-06-05_7.10.05.png",
        "3bace09-_2019-06-05_7.10.05.png",
        1322,
        604,
        "#34373d"
      ]
    }
  ]
}
[/block]
Below is the page when logged in:

* The top left side is the menu for the profile, username, and the bottom is the navigation.

* The right side is corresponding contents.

* The search box above is available for data query like "transaction hash/ account/contract/block.NH", etc.

* Right to the search box are the general function setting like statistics, messages, API node selection, languages, interface lock, and exit button.

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/6685f98-34f6c54-_2019-06-05_7.12.02.png",
        "34f6c54-_2019-06-05_7.12.02.png",
        1425,
        425,
        "#353941"
      ]
    }
  ]
}
[/block]