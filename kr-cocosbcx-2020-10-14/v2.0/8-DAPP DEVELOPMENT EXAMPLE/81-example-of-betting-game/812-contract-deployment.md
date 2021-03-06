---
title: "8.1.2 Contract Deployment"
slug: "812-contract-deployment"
hidden: false
createdAt: "2019-06-26T06:10:36.022Z"
updatedAt: "2019-08-13T08:06:39.305Z"
---
Cocos-BCX's contract deployment is easier than that of EOS and Ethereum. By pushing the code directly to the chain through the operation interface, it can be updated freely. There are transaction records when creating and updating a contract.

In addition, it must be emphasized that Cocos-BCX will directly deploy the source code to the chain without an intermediate code.

Once the contract is deployed on the chain, the source code can be viewed in the explorer. The data that has been written in public_data is open and transparent.

Below is the detailed deployment process:

##step1: Register

The account system of Cocos-BCX is similar to that of BitShares, which can be registered directly with a username and password. Therefore, it’s important to keep in mind that the password cannot be retrieve once you forget it.

There are currently three ways to register a Cocos-BCX test account:
1. Use js-sdk to open the sample registration on index.html as shown in the following picture:


[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/3cc628a-d613f64-image.png",
        "d613f64-image.png",
        2948,
        1608,
        "#f8f6f8"
      ]
    }
  ]
}
[/block]
Cocos-BCX's js-sdk demo is extremely powerful and easy to use. It contains almost all the functions of the blockchain for users to experience.

Js-sdk demo is a page program, you can use the developer tools of chrome to observe the output of the program through the console. It is easy to find errors in the execution process, which is very helpful to solve problems.

2. You can register at http://www.easywallet.pro, the terminal of Cocos-BCX, which contains a lot of features including the core function of wallet and explorer. 

3. Use the command line to send the command. See [cli_wallet](https://cn-dev.cocosbcx.io/v2.0/docs/22-cli_wallet) for details.



##step2: Deploy to the blockchain

So far, we have created a developer account to deploy the contract, which is shown as follows according to the input box of the js-sdk demo:

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/265ba88-10e1251-_1.png",
        "10e1251-_1.png",
        864,
        637,
        "#fcfcfc"
      ]
    }
  ]
}
[/block]
The deployment of the contract requires these parameters. The public-private key pair is very simple by clicking a button for generating a public-private key pair on the contract deployment function. Then enter the appropriate contract name and code. Click OK to create a contract.

if there is an error, it may be caused by the following reasons:
1	You forgot to log in to the account before deploying the contract (login directly in the js-sdk demo).
2	The logged in account is not registered as a developer.
3	COCOS in the account is insufficient to cover the fee.
4	There is an error in the code of contract deployment. You need to correct the error and redeploy the contract.

The specific error can be found in the js console output in the js-sdk demo with the developer tools under the chrome.

So far, we have successfully deployed the contract to the chain. We can enter the deployed contract name in the terminal to view the contract information, including the basic information of the contract, code, interfaces, data zones (public_data), call statistics, etc., as shown below:

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/6ab6211-d23ba3c-_1.png",
        "d23ba3c-_1.png",
        865,
        249,
        "#383c42"
      ]
    }
  ]
}
[/block]

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/17d014a-ee059c6-_1.png",
        "ee059c6-_1.png",
        865,
        526,
        "#363a3f"
      ]
    }
  ]
}
[/block]
Among them, the function of contract statistics is very powerful and convenient to see the statistics of various operations related to the contract.