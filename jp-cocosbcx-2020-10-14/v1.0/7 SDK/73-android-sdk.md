---
title: "7.4 Android-SDK"
slug: "73-android-sdk"
hidden: false
createdAt: "2019-09-18T05:08:16.797Z"
updatedAt: "2019-09-18T05:48:00.323Z"
---
[block:api-header]
{
  "title": "説明"
}
[/block]
このドキュメントはAndroid　cocosウォレットの開発用です。
SDKはAndroid4.0（API　Level　14）以降に対応できます。現在のテスト版はv.27を使用しています。

備考：Android　P（v.27以降）はhttpサーバーにアクセス制限をかけていますが、SDKにはhttpリクエストが備えています。
[block:api-header]
{
  "title": "クラスライブラリのリファレンスについて"
}
[/block]
1．bcx_sdk.aarをプロジェクトディレクトリにコピーし、Project StructureでNew Mouduleを選択し（Module dependencyを追加しないでください）、Import JAR/aar Packageを選択してください。そしてNextをクリックし、aarの所在パスを選択してから、Finishをクリックし、Module dependency選択してbcx_sdkMouduleをプロジェクトに追加してください。
備考：サードパーティ依存関係がarrファイルに追加されないので、下記コードで追加してください。
[block:code]
{
  "codes": [
    {
      "code": "// implenment websocket\n    implementation 'com.neovisionaries:nv-websocket-client:1.30'\n    // implenment bitcoinj\n    implementation 'org.bitcoinj:bitcoinj-core:0.14.7'\n    implementation group: 'com.google.code.gson', name: 'gson', version: '2.8.5'\n    implementation group: \"org.tukaani\", name: \"xz\", version: \"1.6\"\n    implementation 'com.squareup.okhttp3:okhttp:3.12.1'\n    // spongycastle\n    implementation 'com.madgag.spongycastle:core:1.58.0.0'\n    implementation 'com.madgag.spongycastle:prov:1.58.0.0'\n    implementation 'com.madgag.spongycastle:pkix:1.54.0.0'\n    implementation 'com.madgag.spongycastle:pg:1.54.0.0'\n    // fasterxml\n    implementation 'com.fasterxml.jackson.core:jackson-databind:2.9.7'",
      "language": "java"
    }
  ]
}
[/block]
2．Mavenモード（今後対応する予定）
[block:code]
{
  "codes": [
    {
      "code": "//通常依存\nimplementation 'com.cocos.android:cocos-sdk:1.0.0'\n\n//すべての依存トランシットを切ります―方法1\nimplementation 'com.cocos.android:cocos-sdk:1.0.0@aar'\n\n//すべての依存トランシットを切ります―方法2\nimplementation('com.cocos.android:cocos-sdk:1.0.0') {\n        transitive = false\n}",
      "language": "java"
    }
  ]
}
[/block]
**注意：**
1．同じ名称のデータベースを作成しないでください：cocos_bcx_android_sdk.db;
2．ERROR：INSTALL_FAILED_NO_MATCHING_ABIS

**解決案**
appモジュールのbuild.guard androidに下記コードを追加します：
[block:code]
{
  "codes": [
    {
      "code": "packagingOptions {\n        exclude 'lib/x86_64/darwin/libscrypt.dylib'\n        exclude 'lib/x86_64/freebsd/libscrypt.so'\n        exclude 'lib/x86_64/linux/libscrypt.so'\n    }",
      "language": "java"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "SDKの初期化"
}
[/block]
他のインターフェイスをコールする前に必ず初期化してください。でなければ、ヌルポインタエラー（null pointer error）が発生することがあります。
[block:code]
{
  "codes": [
    {
      "code": "List<String> mListNode = Arrays.asList(\"ws://47.93.62.96:8050\", \"ws://39.96.33.61:8080\", \"ws://39.96.29.40:8050\", \"ws://39.106.126.54:8050\");\n       String[] faucetUrl = {\"http://47.93.62.96:3000/api/v1/accounts\"};\n       String chainId = \"53b98adf376459cc29e5672075ed0c0b1672ea7dce42b0b1fe5e021c02bda640\";\n       String coreAsset = \"COCOS\";\n       boolean isOpenLog = true;\n       CocosBcxApiWrapper.getBcxInstance().init(this, chainId, mListNode, faucetUrl, coreAsset, isOpenLog,\n               new IBcxCallBack() {\n                   @Override\n                   public void onReceiveValue(String value) {\n                       Log.i(\"initBcxSdk\", value);\n                 }\n               });",
      "language": "java"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "SDK　APIについて"
}
[/block]
リターン値は全部string型のデータです。
APIのコールオブジェクトはシングルトンオブジェクトです。
例：
[block:code]
{
  "codes": [
    {
      "code": "/**\n    * account model  create account\n    *\n    * @param strAccountName accountName\n    * @param strPassword    Password\n    * @param isAutoLogin    true :   log in， false:just register\n    * @param callBack\n    */           \nCocosBcxApiWrapper.getBcxInstance().create_password_account(\"*****\", \"*****\", true, new IBcxCallBack() {\n               @Override\n               public void onReceiveValue(String value) {\n                   Log.i(\"createaccwithpassword\", value);\n                   ToastUtils.showShort(value);\n               }\n           });",
      "language": "java"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "ステータスコード"
}
[/block]
**一覧と説明** 
[block:parameters]
{
  "data": {
    "h-0": "code",
    "h-1": "Message",
    "h-2": "Description",
    "0-0": "300",
    "0-1": "Chain sync error, please check your system clock",
    "1-0": "301",
    "1-1": "RPC connection failed. Please check your network",
    "2-0": "1",
    "2-1": "None",
    "3-0": "0",
    "2-2": "Operation succeeded",
    "3-1": "failed",
    "3-2": "The operation failed, and the error status description is not fixed. You can directly prompt res.message or to prompt the operation failure.",
    "4-0": "101",
    "4-1": "Parameter is missing",
    "5-0": "1011",
    "5-1": "Parameter error",
    "6-0": "102",
    "6-1": "The network is busy, please check your network connection",
    "7-1": "Please enter the correct account name(/^a-z{4,63}/$)",
    "7-0": "103",
    "8-1": "XX not found",
    "8-0": "104",
    "9-0": "105",
    "9-1": "wrong password",
    "10-0": "106",
    "10-1": "The account is already unlocked",
    "11-0": "107",
    "11-1": "Please import the private key",
    "12-0": "108",
    "12-1": "User name or password error (please confirm that your account is registered in account mode, and the account registered in wallet mode cannot be logged in using account mode)",
    "13-0": "109",
    "13-1": "Please enter the correct private key",
    "14-0": "110",
    "14-1": "The private key has no account information",
    "15-0": "111",
    "15-1": "Please login first",
    "16-0": "112",
    "16-1": "Must have owner permission to change the password, please confirm that you imported the ownerPrivateKey",
    "17-0": "113",
    "17-1": "Please enter the correct original/temporary password",
    "18-0": "114",
    "18-1": "Account is locked or not logged in.",
    "19-0": "115",
    "19-1": "There is no asset XX on block chain",
    "20-0": "116",
    "20-1": "Account receivable does not exist",
    "21-0": "117",
    "21-1": "The current asset precision is configured as X, and the decimal cannot exceed X",
    "22-0": "118",
    "22-1": "Encrypt memo failed",
    "23-0": "119",
    "23-1": "Expiry of the transaction",
    "24-0": "120",
    "24-1": "Error fetching account record",
    "25-0": "121",
    "25-1": "block and transaction information cannot be found",
    "26-0": "122",
    "26-1": "Parameter blockOrTXID is incorrect",
    "27-0": "123",
    "27-1": "Parameter account can not be empty",
    "28-0": "124",
    "28-1": "Receivables account name can not be empty",
    "29-0": "125",
    "29-1": "Users do not own XX assets",
    "30-0": "127",
    "30-1": "No reward available",
    "31-0": "129",
    "31-1": "Parameter ‘memo’ can not be empty",
    "32-0": "130",
    "32-1": "Please enter the correct contract name(/^a-z{4,63}$/)",
    "33-0": "131",
    "33-1": "Parameter ‘worldView’ can not be empty",
    "34-0": "133",
    "34-1": "Parameter ‘toAccount’ can not be empty",
    "35-0": "135",
    "35-1": "Please check parameter data type",
    "36-0": "136",
    "36-1": "Parameter ‘orderId’ can not be empty",
    "37-0": "137",
    "37-1": "Parameter ‘NHAssetHashOrIds’ can not be empty",
    "38-0": "138",
    "38-1": "Parameter ‘url’ can not be empty",
    "39-0": "139",
    "39-1": "Node address must start with ws:// or wss://",
    "40-0": "140",
    "40-1": "API server node address already exists",
    "41-0": "141",
    "41-1": "Please check the data in parameter NHAssets",
    "42-0": "142",
    "42-1": "Please check the data type of parameter NHAssets",
    "43-0": "144",
    "43-2": "",
    "43-1": "Your current batch creation / deletion / transfer number is X , and batch operations can not exceed X",
    "44-0": "145",
    "44-1": "XX contract not found",
    "45-0": "146",
    "45-1": "The account does not contain information about the contract",
    "46-0": "147",
    "46-1": "NHAsset do not exist",
    "47-0": "148",
    "47-1": "Request timeout, please try to unlock the account or login the account",
    "48-0": "149",
    "48-1": "This wallet has already been imported",
    "49-0": "150",
    "49-1": "Key import error",
    "50-0": "151",
    "50-1": "File saving is not supported",
    "50-2": "",
    "51-0": "152",
    "51-1": "Invalid backup to download conversion",
    "52-0": "153",
    "52-1": "Please unlock your wallet first",
    "53-0": "154",
    "53-1": "Please restore your wallet first",
    "54-0": "155",
    "54-1": "Your browser may not support wallet file recovery",
    "55-0": "156",
    "55-1": "The wallet has been imported. Do not repeat import",
    "56-0": "157",
    "56-1": "Can’t delete wallet, does not exist in index",
    "57-0": "158",
    "57-1": "Imported Wallet core assets can not be XX , and it should be XX",
    "58-0": "159",
    "58-1": "Account exists",
    "59-0": "160",
    "59-1": "You are not the creator of the Asset XX .",
    "60-0": "161",
    "60-1": "Orders do not exist",
    "61-0": "162",
    "61-1": "The asset already exists",
    "62-0": "163",
    "62-1": "The wallet already exists. Please try importing the private key",
    "63-0": "164",
    "63-1": "worldViews do not exist",
    "64-0": "165",
    "64-1": "There is no wallet account information on the chain",
    "65-0": "166",
    "65-1": "The Wallet Chain ID does not match the current chain configuration information. The chain ID of the wallet is: XX",
    "66-0": "167",
    "66-2": "",
    "66-1": "The current contract version ID was not found",
    "67-0": "168",
    "67-1": "This subscription does not exist",
    "68-0": "169",
    "68-1": "MethodMethod does not exist does not exist"
  },
  "cols": 3,
  "rows": 69
}
[/block]

[block:api-header]
{
  "title": "APIの使用例"
}
[/block]
1．ウォレットモードでのアカウント作成
[block:code]
{
  "codes": [
    {
      "code": "/**\n     * wallet model  create account\n     *\n     * @param strAccountName accountName\n     * @param strPassword    Password\n     * @param isAutoLogin    true :   log in， false:just register\n     * @param callBack\n     */\n  CocosBcxApiWrapper.getBcxInstance().create_wallet_account(\"testtest3\", \"111111\", true, new IBcxCallBack() {\n                @Override\n                public void onReceiveValue(String value) {\n                    Log.i(\"create_wallet_account\", value);\n                }\n            });",
      "language": "java"
    }
  ]
}
[/block]

[block:code]
{
  "codes": [
    {
      "code": "データ1をリターンします：{\"code\":1,\"data\":{\"account\":{\"active_key\":\"COCOS6BGnotPV3232ZJBvp5FgZuZ5cGPqNgqaSHnbSoaJLjaKmV8LLE\",\"name\":\"testtest3\",\"owner_key\":\"COCOS8F9BeMjVqBVakgJhTm2pQoMido4ZBksfHL6oQb1ZWXtpmpBJF5\"}}}",
      "language": "java"
    }
  ]
}
[/block]

[block:code]
{
  "codes": [
    {
      "code": "データ2をリターンします：{\"code\":159,\"message\":account exist}",
      "language": "java"
    }
  ]
}
[/block]

[block:code]
{
  "codes": [
    {
      "code": "データ3をリターンします：{\"code\":102,\"message\":It doesn't connect to the server.}",
      "language": "java"
    }
  ]
}
[/block]
2．取引
[block:code]
{
  "codes": [
    {
      "code": "/**\n     * transfer\n     * @param password パスワード（仮パスワード/アカウントパスワード）\n     * @param strFrom 送り手アカウント\n     * @param strTo 受け手アカウント\n     * @param strAmount 金額\n     * @param strAssetSymbol トークンシンボル\n     * @param strMemo メモ\n     */\n CocosBcxApiWrapper.getBcxInstance().transfer(\"111111\", \"testtest3\", \"gnkhandsome1\", \"10\", \"COCOS\", \"testting\", new IBcxCallBack() {\n                @Override\n                public void onReceiveValue(String value) {\n                    Log.i(\"transfer\", value);\n                }\n            });",
      "language": "java"
    }
  ]
}
[/block]

[block:code]
{
  "codes": [
    {
      "code": "###データ1をリターンします：{\"code\":1,\"message\":bf3c058914399136d384de714a3c57d2966e1513}",
      "language": "java"
    }
  ]
}
[/block]
注： hash : bf3c058914399136d384de714a3c57d2966e1513
[block:code]
{
  "codes": [
    {
      "code": "データ2をリターンします：{\"code\":105,\"message\":wrong password}",
      "language": "java"
    }
  ]
}
[/block]
3．秘密鍵のエクスポート（秘密鍵でインポートされたアカウントは登録した際にインポートした秘密鍵だけエクスポートできます）
[block:code]
{
  "codes": [
    {
      "code": "CocosBcxApiWrapper.getBcxInstance().export_private_key(\"gnkhandsome1\", \"123456\", new IBcxCallBack() {\n                            @Override\n                            public void onReceiveValue(final String value) {\n                                   Log.i(\"export_private_key\", value);\n                                \n                            }\n                        });",
      "language": "java"
    }
  ]
}
[/block]
データ（公開鍵（Key）、秘密鍵（Value））をリターンします：
[block:code]
{
  "codes": [
    {
      "code": "{\"code\":1,\"data\":{\"COCOS6G55VgR94GZmELS4UHEf2eVggmhPRnWLTWgGiEmzuBKdvEwoAB\":\"5Hy7aVcZFyHa7UKURN22m9gB7xp4KS7Bo1dibWSVZZYAg6Br1bu\",\"COCOS8Dw7QjWVFggYCvp9c8XbsXssqizN1MqkwPfSAVTQppQLhUcTC2\":\"5JgPmrWHevyH4ZzLkgZL3yAaddXE6phrKJYCfKyAJmhhjbmZyF7\"},\"message\":\"\"}",
      "language": "java"
    }
  ]
}
[/block]
4．残高情報の照会（パラメーター1：ユーザーID；パラメーター2：照会するアセットID、空に設定する場合はすべてのアセット情報を照会します）
[block:code]
{
  "codes": [
    {
      "code": "List<Object> assetSymbolOrId = new ArrayList<>();\n      // todo デフォルトトークン\nassetSymbolOrId.add(\"1.3.0\");\nCocosBcxApiWrapper.getBcxInstance().get_account_balances(\"1.2.76\", unit, new IBcxCallBack() {\n          @Override\n          public void onReceiveValue(final String value) {\n                  Log.i(\"get_account_balances\", value);\n          }\n      });",
      "language": "java"
    }
  ]
}
[/block]
データをリターンします：
[block:code]
{
  "codes": [
    {
      "code": "{\"id\":1,\"data\":[{\"amount\":55362897,\"asset_id\":\"1.3.0\"}]}",
      "language": "text"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "GitHub"
}
[/block]
[AndroidSDK](https://github.com/Cocos-BCX/AndroidSdk)