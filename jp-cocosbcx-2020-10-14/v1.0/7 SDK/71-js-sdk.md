---
title: "7.2 JS-SDK"
slug: "71-js-sdk"
excerpt: "JavaScript APIの目的は、Cocos-BCX　RPC　APIを使用してCocos-BCXのチェーンシステムとのインテグレーションです。"
hidden: false
createdAt: "2019-09-18T02:18:01.374Z"
updatedAt: "2019-09-18T05:07:30.359Z"
---
[block:api-header]
{
  "title": "クラスライブラリについて"
}
[/block]
**APIファイルを導入** 
[block:code]
{
  "codes": [
    {
      "code": "<script type=\"text/javascript\" src=\"bcx.min.js\"></script>",
      "language": "javascript"
    }
  ]
}
[/block]
**クラスライブラリオブジェクトをインスタンス化** 
[block:code]
{
  "codes": [
    {
      "code": "var bcx=new BCX({\n            default_ws_node:”ws://XXXXXXXXX” //ノードrpcアドレス、任意項目。空欄の場合、ws_node_listから速度が最も早いノードへ自動接続します\n            ws_node_list:[{url:\"ws://xxxxxxx\",name:\"xxxxx\"}]//APIサーバノードリスト、必須項目\n            faucet_url:\"http://xxx.xxx.xxx.xxx:xxxx\", //登録\n            networks:[{\n                core_asset:\"xxx\",//コアアセットシンボル\n                chain_id:\"xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx\"//チェーン链id   \n            }], \n            auto_reconnect:false,//RPCの接続が切断した場合、自動接続するかどうか、デフォルトはtrue\n            app_keys:[\"xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx\"]//コントラクトの授権。授権しない場合はスキップしてください\n\t })",
      "language": "javascript"
    }
  ]
}
[/block]
**コール例―振込** 
[block:code]
{
  "codes": [
    {
      "code": "bcx.transferAsset({\n     to:\"test\",\n     amount:1\n     assetId:\"COCOS\",\n     memo:\"\"\n}).then(res=>{\n     console.log('transferAsset res',res);\n})",
      "language": "javascript"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "APIについての説明"
}
[/block]
1．特別な説明以外、callback関数は必ず選べられます。callbackがリターンしたresultは{code:0,message:””}構造のObject対象です。code=1の場合は成功であり、message説明がありません。code!=1の場合は失敗であり、messageは失敗状態の説明になります。
2．特別な説明以外、関数は全部一つだけあります。関数はObjectであり、すべての関連関数（callbackも）を含んでいます。

コール例：
[block:code]
{
  "codes": [
    {
      "code": "bcl.getPrivateKey({\n     callback:res=>{}\n})",
      "language": "javascript"
    }
  ]
}
[/block]
3．購読以外のインターフェイスはcallback関数をコールしない場合すべてpromise対象をリターンします。
4．インターフェイスの関数はすべて文字列です（特別な説明がない限り）。
5．インターフェイスの関数は空に設定してならなりません（特別な説明がない限り）。callbackは任意項目です。
6．クエリインタフェースのリターン例：:{code:1,data:[]}
7．クエリ以外のインターフェイスのリターン値はObjectであるtryDataがあります。
例：
[block:code]
{
  "codes": [
    {
      "code": "trx_data:{\n block_num:*****,//ブロックの高さ\n trx_id:\"************************\"//取引 ID\n}",
      "language": "javascript"
    }
  ]
}
[/block]
8．クエリ以外のインターフェイスはIDビジネスと関わる場合（例えば、NHアセットを作成した時発生したID）、data対象を含むデータをリターンします。
例：
[block:code]
{
  "codes": [
    {
      "code": "data:{\n  real_running_time: 387//実行時間\n  result: \"4.2.288\"//ビジネス id\n}",
      "language": "javascript"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "ステータスコード"
}
[/block]

[block:parameters]
{
  "data": {
    "h-0": "Code",
    "h-1": "Message",
    "h-2": "Description",
    "0-0": "300",
    "0-1": "Chain sync error, please check your system clock",
    "0-2": "",
    "1-0": "301",
    "1-1": "RPC connection failed. Please check your network",
    "2-0": "1",
    "2-1": "None",
    "2-2": "Operation succeeded",
    "3-0": "0",
    "3-1": "failed",
    "3-2": "The operation failed, and the error status description is not fixed. You can directly prompt res.message or to prompt the operation failure.",
    "4-0": "101",
    "4-1": "Parameter is missing",
    "5-0": "1011",
    "5-1": "Parameter error",
    "6-0": "102",
    "6-1": "The network is busy, please check your network connection",
    "7-0": "103",
    "7-1": "Please enter the correct account name(/^a-z{4,63}/$)",
    "8-0": "104",
    "8-1": "XX not found",
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
    "14-2": "",
    "15-0": "111",
    "15-1": "Please login first",
    "16-0": "112",
    "16-1": "Must have owner permission to change the password, please confirm that you imported the ownerPrivateKey",
    "17-0": "113",
    "17-1": "Please enter the correct original/temporary password",
    "18-0": "114",
    "18-1": "Account is locked or not logged in",
    "19-0": "115",
    "19-1": "There is no asset XX on block chain",
    "20-0": "116",
    "20-1": "Account receivable does not exist",
    "21-0": "117",
    "21-1": "The current asset precision is configured as X ,and the decimal cannot exceed X",
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
    "31-1": "Parameter ‘memo’ can not be empty memo",
    "32-0": "130",
    "32-1": "Please enter the correct contract name(/^a-z{4,63}$/)",
    "33-0": "131",
    "33-1": "Parameter ‘worldView’ can not be empty",
    "34-0": "133",
    "34-1": "Parameter ‘toAccount’ can not be empty toAccount",
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
    "66-1": "The current contract version ID was not found",
    "67-0": "168",
    "67-1": "This subscription does not exist",
    "68-0": "169",
    "68-1": "Method does not exist"
  },
  "cols": 3,
  "rows": 69
}
[/block]

[block:api-header]
{
  "title": "チェーンシステムとインタラクションするAPI"
}
[/block]

[block:api-header]
{
  "title": "ウォレットモード"
}
[/block]
**アカウント作成**
関数：createAccountWithWallet
機能：ウォレットモードでアカウントを作成します。このモデルで作成したアカウントは、ID＆パスワードを持ってログインできません。作成する時すでにアカウントを所持している場合は子アカウントの作成になりますが、終身会員のみ操作できます。
パラメーター：
account：アカウント名、/^[a-z][a-z0-9.-]{4,63}$/、小文字アルファベット＋数字/小文字アルファベット/点/ハイフンから成っていて、長さは4～63以内です。
password：パスワード
callback：コールバック関数

**ウォレットのバックアップ**
関数：backupDownload
機能：ウォレットデータをバックアップします。このAPIをコールすると、ウォレットファイルが自動的に作成され、データをダウンロードします。
パラメーター：
callback：コールバック関数

**バックアップしたウォレットデータをロード**
関数：loadWalletFile
機能：webにとって、file inputがchangeイベントと連携した時、ウォレットファイルをロードします。
パラメーター：
file：ホスティング環境はweb => file inputのchangeイベントで作動した場合、イベント対象event.target,files[0]をリターンします。
callback：コールバック関数

**ウォレットのバックアップを復元**
関数：restoreWallet
機能：ウォレットをバックアップする時に、ウォレットファイルが自動作成され、ダウンロードします。このAPIをコールした後、ウォレットがロック状態に入ります。
パラメーター：
password：バックアップのパスワード
callback：コールバック関数

**秘密鍵のインポート**
関数：importPrivateKey
機能：秘密鍵をウォレットにインポートします
パラメーター：
privateKey：復号化された秘密鍵
password：ウォレットを持っているまたは復元された場合、パスワードはユーザーが設定したパスワードとなり、そうでない場合は修正できる仮パスワードです。
callback：コールバック関数

**ウォレットの削除**
関数：deleteWallet
機能：ウォレット情報を削除します。アカウントモードの場合、まずウォレットを削除することを推奨します。
パラメーター：
callback：コールバック関数

**ウォレットアカウントの入手**
関数：getAccount
機能：ウォレットアカウント情報を取得します
パラメーター：
そのままデータをリターンします。
例：
[block:code]
{
  "codes": [
    {
      "code": "{  \n\t\t\"accounts\": [\"tom0002\"],  \n\t\t\"currentAccount\": {  \n\t\t\t\"account_id\": \"1.2.20\",  \n\t\t\t\"locked\": true,  \n\t\t\t\"account_name\": \"tom0002\"  \n\t\t}\n  }",
      "language": "javascript"
    }
  ]
}
[/block]
**複数アカウントの切り替え**
関数：setCurrentAccount
機能：ウォレットモードで使用中のアカウントを切り替えます
パラメーター：
account：切り替えのアカウント
callback：コールバック関数

**アカウントのアンロック**
関数：unlockAccount
機能：秘密鍵のインポートまたはウォレットモードで、アカウントをアンロックします
パラメーター：
password：秘密鍵をインポートする際に設定した仮パスワード
callback：コールバック関数

**アカウントのロック**
関数：lockAccount
機能：アカウントをロックします
パラメーター：
callback：コールバック関数
[block:api-header]
{
  "title": "アカウントモード"
}
[/block]
**アカウントの作成**
関数：creatAccountWithPassword
機能：アカウントを新規作成します。すでにログイン状態だと、子アカウントが作成されます。ただし、終身会員になる必要があります。
パラメーター：
account：アカウント名は/^[a-z][a-z0-9.-]{4,63}$/で、小文字アルファベット＋数字/アルファベット/点/ハイフンから成っていて、長さは4～63です。
password：パスワード
autoLogin：boolean型、自動ログインを設定します。デフォルトはfalse。
callback：コールバック関数

**パスワードでログイン**
関数：passwordLogin
機能：アカウントへログインします
パラメーター：
account：アカウント名
password：パスワード
callback：コールバック関数

**秘密鍵でログイン**
関数：privateKeyLogin
機能：実際の秘密鍵はウォレットモードだけ存在しますが、互換性を考えて、このAPIを保留しました。
パラメーター：
privateKey：秘密鍵
password：設定した仮パスワード
callback：コールバック関数

**ログアウト**
関数：logout
機能：暗号化されたkeyを含み、キャッシュメモリーをクリアします。
パラメーター：
callback：コールバック関数

**パスワードの変更**
関数：changePassword
機能：アカウントモードだけパスワードを変更できます；変更完了後、APIは自動コールされ、ログアウトになります。
パラメーター：
oldPassword：元のパスワード
newPassword：新しいパスワード
callback：コールバック関数

**ログイン中のアカウント情報を入手**
関数：getAccountInfo
機能：アカウントがアンロック状態の場合、アカウント名nameを含むデータをリターンします
パラメーター：
無
[block:api-header]
{
  "title": "アカウントOP"
}
[/block]
**終身会員へアップグレード**
関数：upgradeAccount
機能：終身会員に切り替えた後、手数料を支払い、子アカウントを作成できます
パラメーター：
onlyGetFee：手数料情報だけ入手します
callback：コールバック関数

**秘密鍵の入手**
関数：getPrivateKey
機能：ユーザーのactive_private_keyを取得します。この秘密鍵はアカウントですべての取引（手数料も含む）のサインになります。リターン値のowner_private_keyは、アカウント関連のすべての設定を変更することができます
パラメーター：
callback：秘密鍵が設定完了後のコールバック関数

**操作履歴を照会**
関数：queryAccountOperations
機能：アカウントの操作履歴を照会します
パラメーター：
account：アカウント名
limit：最大履歴数
staetId：初めの履歴id。すべての履歴を照会する場合、初めてのアカウント履歴はstartIdとなります
endId：終わりの履歴id。すべての履歴を照会する場合、終わりのアカウント履歴はendIdとなります
callback：APIパラメーターの説明

**アカウント操作変更履歴の描述**
関数：subscribeToAccountOperations
機能：アカウント操作変更履歴を記録します
パラメーター：
account：アカウント名
callback：操作履歴が変更になる度にcallback関数をコールします

**アカウント情報の照会**
関数：queryAccountInfo
機能：アカウントidを含み、アカウント情報を表示します
パラメーター：
account：アカウント名
callback：APIパラメーターの説明
[block:api-header]
{
  "title": "トークン操作のインターフェイス"
}
[/block]
**トークンの取引**
関数：transferAsset
機能：受け手にトークンを振り込みます
パラメーター：
fromAccount：送り手アカウント名（提議をするのではない）
toAccount：受け手アカウント名
amount：振り込む金額
assetId：アセットID、あるいはアセットシンボル
memo：メモ
feeAssetId：手数料となるアセットID
isPropose：提議します
onlyGetFee（boolean）：手数料情報だけ入手します
callback：振り込み後のコールバック関数を設定します

**アセットの作成**
関数：creatAsset
機能：トークンを作成します
パラメーター：
assetId：アセットID、^[.A-Z]+$
precision：精度（小数点以下の桁数）
maxSupply：最大アセット量
description：アセット説明、空に設定できます
onlyGetFee：手数料情報だけ入手します
callback：APIパラメーター説明
coreExchangeRate（Object）：
[block:code]
{
  "codes": [
    {
      "code": "{  \n\t\t\tquoteAmount:見積アセット(即ち作成したトークン、デフォルトは1),  \n\t\t\tbaseAmount: ベースアセット(即ちコアアセット、デフォルトは1)  \n\t\t}",
      "language": "javascript"
    }
  ]
}
[/block]
**アセットのアップデート**
関数：updateAsset
機能：トークンをアップデートします
パラメーター：
assetId：アセットID、^[.A-Z]+$
maxSupply：最大アセット量
newIssuer：新しい発行者
description：アセット説明、空に設定できます
onlyGetFee：手数料情報だけ入手します
callback：APIパラメーター説明
coreExchangeRate（Object）：手数料レート
[block:code]
{
  "codes": [
    {
      "code": "{   \n\t\tquoteAmount:見積アセット\n\t\tbaseAmount: ベースアセット\n\t}",
      "language": "javascript"
    }
  ]
}
[/block]
**アセットの削除**
関数：reserveAsset
機能：トークンを削除します
パラメーター：
assetId：アセットID
amount：削除する量
onlyGetFee：手数料情報だけ入手します
callback：コールバック関数

**アセットの発行**
関数：issueAsset
機能：トークンを発行します
パラメーター：
toAccount：発行者アカウント
amount：発行量
assetId：アセットID
memo：メモ、空に設定できます
onlyGetFee：手数料情報だけ入手します
callback：コールバック関数

**アセット手数料プールへトークンを注入**
関数：assetFundFeePool
機能：コアアセットはすべての手数料の支払い手段となります。手数料プールはTier II アセットからコアアセットへ交換する時の手数料の役割を担います。プールの残高が0になると、TierⅡアセットで手数料を支払うのも不可能になります。現在、TierⅡアセットで支払える手数料のAPIは振込、投票、終身会員への切り替え、アセットの発行で、これから追加する予定です。
パラメーター：
assetId：トークンを注入するTierⅡアセットID
amount：注入するコアアセット量
onlyGetFee：手数料情報だけ入手します
callback：コールバック関数

**アセット手数料の受取**
関数：assetClaimFees
機能：アセット発行者はここでアセット手数料を受け取ることができます
パラメーター：
assetId：受け取るTierⅡアセットID
amount：TierⅡアセット量
onlyGetFee：手数料情報だけ入手します
callback：コールバック関数

**オンチェーンアセットの照会**
関数：queryAsset：
機能：チェーンシステムに実装したアセット情報の照会
パラメーター：
assetId：アセットID。空に設定する場合、オンチェーン上すべてのアセットを照会することになります
callback：コールバック関数

**アカウントの指定アセット残高の照会**
関数：queryAccountBalance
機能：アカウント内指定アセット残高を照会します。assetIdを空に設定する場合、すべてのアセット残高を照会することになります。
パラメーター：
assetId：アセットID、あるいはアセットシンボル。
account：アカウント名
callback：コールバック関数

**アカウント内すべてのアセット残高をリスティング**
関数：queryAccountAllBalances
機能：ユーザーが所有しているすべてのアセット残高をリスティングします。リストでは、アセットとユニットのレート値も含んでいます。アセット残高が0の場合、0と表示しているコアアセットをリターンします。
パラメーター：
unit：ユニット、手数料レートまたは相場価格によって、アセットの価値を換算します
account：アカウント名
callback：コールバック関数
[block:api-header]
{
  "title": "NHアセットOP"
}
[/block]
**開発者として登録**
関数：registerCreator
機能：開発者として登録します

**世界観の作成**
関数：creatNHAsset
機能：唯一性を持つNHアセットを作成します。このインターフェイスはNHアセットの作成者（鍛冶屋）だけ利用できます。
パラメーター：
assetId：現在のNHアセット取引に適用するアセットID
worldView：世界観
baseDescribe：作成者が定義したNHアセットの説明
ownerAccount：指定したNHアセットの所有者（NHアセットの帰属するアカウント、デフォルトは作成者）
NHAssetCount(Number)：作成したNHアセット量、デフォルトは1。typeだけを0に設定したとき、単一種類のNHアセット作成ができます
type：作成したNHアセットの種類、デフォルトは0。デフォルト設定の時、単一種類のNHアセットを作成し、1に設定すると、異なる種類のNHアセットを作成します
NHAsset(Array)例：
[block:code]
{
  "codes": [
    {
      "code": "[{  \n\t \"assetId\": \"X.X.X\",  \n\t \"worldView\": \"TEST\",  \n\t \"baseDescribe\": \"{name:\\\"占い師\\\"}\",  \n\t \"ownerAccount\": \"test2\"  \n\t}, {  \n\t \"assetId\": \"X.X.X\",  \n\t \"worldView\": \"TEST\",  \n\t \"baseDescribe\": \"{name:\\\"魔女\\\"}\",  \n\t \"ownerAccount\": \"test2\"  \n\t}, {  \n\t \"assetId\": \"X.X.X\",  \n\t \"worldView\": \"TEST\",  \n\t \"baseDescribe\": \"{name:\\\"狩人\\\"}\",  \n\t \"ownerAccount\": \"test2\"  \n\t}]",
      "language": "javascript"
    }
  ]
}
[/block]
**NHアセットの削除**
関数：deleteNHAsset
機能：NHアセットデータをすべて削除します（ユーザー自身だけが授権し処理できます）。
パラメーター：
NHAssetId（Array）：NHアセット実例の唯一ID；例[X.X.X, X.X.X]

**NHアセットの取引**
関数：transferNHAsset
機能：ユーザーのNHアセットを他人に移転します
パラメーター：
toAccount：NHアセットの受け手アカウント
NHAssetIds(Array)：いくつかNHアセットidの配列、例[X.X.X, X.X.X]

**世界観と関係付ける提議を承認**
関数：approvalProposal
機能：他人が自分の世界観と関係付ける提議を承認します
パラメーター：
proposalId：提議のID

**現在対応中の提議情報を入手**
関数：getAccountProposal
機能：現在操作中のユーザーが対応している提議情報を取得します
[block:api-header]
{
  "title": "NHアセットの取引インターフェイス"
}
[/block]
**NHアセットのpending orderを作成**
関数：creatNHAssetOrder
機能：NHアセットを売出します（取引する前にqueryAccountGameItemsをコールし、アカウント内のNHアセットをリスティングできます）
パラメーター：
otcAccount：OTC取引所アカウント、pending orderの手数料を徴収します（OTCプラットフォームが記入します）
orderFee：ユーザーがOTCプラットフォームに支払うpending orderの手数料（OTCプラットフォームが記入します）
NHAssetId：NHアセットの唯一ID（ユーザーが記入します）
price：注文が実行される価格（ユーザーが記入します）
priceAssetId：注文価格が使用するトークンID（ユーザーが記入します）
expiration：有効時間、例えば3600（s）、つまり1時間
memoe：メモ
callback：注文が実行された時のコールバック関数

**NHアセットの購入**
関数：fillNHAssetOrder
機能：NHアセットを購入し、ゲームアイテムの購入代金を支払い、アイテムデータをアップデートします。これはアトミック操作であり、すべてのステップが同時に完了します。支払いあるいはデータ更新がメインチェーンに承認されない場合、異常取引を防止するため、全操作をロールバックします。
パラメーター：
orderId：注文ID
callback：コールバック関数

**NHアセットのpending orderをキャンセル**
関数：cancelNHAssetOrder
機能：NHアセットのpending orderを取消します
パラメーター：
orderId：注文ID
callback：コールバック関数
[block:api-header]
{
  "title": "NHアセットをクエリするインターフェイス"
}
[/block]
**オンチェーンすべてのNHアセットの取引注文情報を照会**
関数：queryNHAssetOrders
機能：オンチェーンすべてのNHアセットの注文情報を照会します
パラメーター：
assetIds(Array)：アセットIDまたはIDのスクリーニング条件
worldViews(Array)：世界観バージョン名またはバージョンIDのスクリーニング条件
pageSize：1ページ当たりのデータサイズ
page：ページ数

**指定アカウント内NHアセットの取引情報の照会**
関数：queryAccountNHAssetOrders
機能：指定アカウント内のNHアセットの取引情報を照会します
パラメーター：
account：照会するアカウント名またはID
pageSize：1ページ当たりのデータサイズ
page：ページ数
callback：コールバック関数

**アカウント内のNHアセットの照会**
関数：queryAccountNHAsset
機能：現在操作中のアカウント内のゲームアイテムと対応するNHアセット情報を照会します
パラメーター：
account：アカウント名またはID
worldViews(Array)：世界観の配列
page：ページ数
pageSize：1ページ当たりのデータサイズ
callback：リターン値
例：{status:1,data:[],total:0}

**開発者が関係付けた世界観の照会**
関数：queryNHCreator
機能：開発者が関係付けた世界観情報を照会します
パラメーター：
account：アカウント名またはID
callback：コールバック関数

**開発者が作成したNHアセットの照会**
関数：queryNHCreator
機能：開発者が作成した世界観情報を照会します
パラメーター：
account：アカウント名またはID
callback：コールバック関数

**NHアセットの情報詳細の照会**
関数：queryNHAsset
機能：NHアセットの情報詳細を照会します
パラメーター：
NHAssetIds：NHアセットIDまたはhash
callback：コールバック関数

**世界観の情報詳細の照会**
関数：lookupWorldViews
機能：世界観の情報詳細を照会します
パラメーター：
worldVeiws(Array)：世界観名またはID
callback：コールバック関数
[block:api-header]
{
  "title": "投票について"
}
[/block]
**ユーザーの投票データの照会**
機能：ユーザーの投票に関するデータを照会します
パラメーター：
callback：コールバック関数

**投票情報の送信**
関数：publishVotes
機能：情報を保存する際に代理人アカウント（プロキシ）を設定したため、ユーザーの投票情報は代理人と同期します
パラメーター：
witnessesIds（Array）：証人アカウントの配列、すべてのユーザーアカウントIDは投票データから確認できます
proxyAccount：代理人アカウント名
callback：コールバック関数
[block:api-header]
{
  "title": "ブロックチェーンブラウザインターフェイス"
}
[/block]
**ブロック情報の照会**
関数：queryBlock
機能：ブロックの高さでブロック情報を照会します
パラメーター：
block：ブロックの高さ

**取引情報の照会**
関数：queryTransaction
機能：取引ID（即ち取引hash）で取引情報を照会します
パラメーター：
transactionId：取引ID

**IDでデータを照会**
関数：queryDateByIds
機能：IDで関連するデータを照会します
パラメーター：
ids(Array)：IDの配列

**オンチェーン取引のサブスクリプション**
関数：subscribeToChainTransaction
機能：オンチェーンで発生した取引情報をサブスクリプションします
パラメーター：
callback：コールバック関数

**ブロック生成情報の照会**
関数：lookupWinessesForExplorer
機能：Demoを参考して、ブロック生成データを解析します
パラメーター：
callback：コールバック関数

**ブロック生成リワード情報の照会**
関数：lookupBlockRewards
機能：Demoを参考して、リワードデータを解析します
パラメーター：
callback：コールバック関数

**ブロック生成リワードの受取**
関数：claimVestingBalance
機能：ブロック生成リワードを受け取ります
パラメーター：
id：リワードID、ブロック生成リワード情報に含まれています。
callback：コールバック関数
[block:api-header]
{
  "title": "APIサーバーに関連するインターフェイス"
}
[/block]
**bcxの初期化**
関数：init
機能：bcxを初期化します（RPC接続、Indexedbデータのリロードなど）
パラメーター：
refresh：任意項目。次回から初めてinit後のキャッシュメモリーを使用します。refreshがtrueの場合だけデータをリロードし、RPCモジュールを再度初期化します。
autoReconnect：任意項目。RPCが切断になった場合自動接続します
subscribeToRpcConnectionStatusCallback：任意項目。RPCの接続状態をサブスクリプションし、値：status=>closed：rpc切断,error：エラー,realopen：接続中をリターンします。
callback：任意項目。コールバック関数

**APIサーバーリストの照会**
関数：lookupWSNodeList
機能：APIサーバーのノードリスト情報を照会します
パラメーター：
refresh：pingをリフレッシュします。この関数は現在切断中のノード情報だけをリフレッシュします。すべてのノードをリフレッシュする場合はinit({refresh:true})をコールしてください。
callback：コールバック関数

**APIサーバーノードへアクセス**
関数：switchAPINode
機能：ノードの切り替え
パラメーター：
url：APIサーバーノードアドレス。APIサーバーノードリストのwebsoketアドレスに限られます
callback：コールバック関数

**新しいAPIサーバーノードを追加**
関数：addAPINode
機能：新しいノードを追加します
パラメーター：
name：新しいノード名
url：APIサーバーノードのwebsoketアドレス
callback：コールバック関数

**APIサーバーノードの削除**
関数：deleteAPINode
機能：ノードを削除します
パラメーター：
url：APIサーバーノードのwebsoketアドレス
callback：コールバック関数

**APIサーバーノードの接続状態をサブスクリプション**
関数：subscribeToRpcConnectionStatus
機能：rpcの接続状態をサブスクリプションします
パラメーター：
callback：コールするとRPCの接続状態statusをリターンします。
リターン値は：
closed：切断
error：エラー
realopen：接続中
[block:api-header]
{
  "title": "コントラクト"
}
[/block]
**秘密鍵/公開鍵のワンクリック作成（ランダム作成）**
関数：generateKeys
機能：公開鍵と秘密鍵ペアをランダムに作成します。権限付きのコントラクトを作成する際に利用されます。作成した秘密鍵はAPIを初期化し、コントラクトを授権するのに用いて、コールバックせずにリターンします。

**コントラクトの作成**
関数：createContract
機能：スマートコントラクトを作成します。コントラクトに権限機能を追加する場合、特定のLuaコードを書き込んで、関数set_permissions_flag =>をコールしてください。権限コード：function my_change_contract_authority( publickey) assert(is_owner()) change_contract_authority( publickey) end function set_permissions_flag(flag) assert(is_owner()) set_permissions_flag(flag) end
パラメーター：
authority：コントラクト権限（公開鍵と秘密鍵ペアのPublicKey）。APIで初期化する時、開発者は秘密鍵を設定することができます。ペアとなる秘密鍵が設定完了してから初めてコントラクトをコールできます。
パラメーター：
name：コントラクト名、/^[a-z][a-z0-9.-]{4,63}$/、小文字アルファベット＋アルファベット/数字/点/ハイフンから成っていて、長さは4～63です。
data：コントラクトのLuaコード
onlyGetFee：手数料情報だけ入手します
callback：APIパラメーターの説明

**コントラクトのアップデート**
関数：updateContract
機能：コントラクトデータをアップデートします
パラメーター：
nameOrId：コントラクト名またはID。例：contract.test02
data：コントラクトのLuaコード
onlyGetFee：手数料情報だけ入手します

**コントラクトのコール**
関数：callContractFunction
機能：コントラクト関数のインターフェイスをコールします
パラメーター：
nameOrId：コントラクト名またはID。例：contract.test02
functionName：コントラクトの関数名、my_nht_describe_change（アイテムの属性を変更します）
valueList(Array)：コールする関数のパラメーター配列。例：[4.2.0,{"size":"large"}]。パラメーターのデータ型がjsonの場合だけ、cisonで解析する必要があります。
runtime：コントラクト関数の実行時間（単位：㎳）、デフォルトは5。
onlyGetFee：手数料情報だけ入手します。デフォルトはfalse。
callback：コールバック関数

**コントラクトデータの照会**
関数：queryContract
機能：コントラクト情報を照会します
パラメーター：
nameOrId：コントラクト名またはID
callback：コールバック関数

**アカウント内コントラクトデータの照会**
関数：queryAccountContractData
機能：アカウント内のコントラクトをコールすることで発生したデータを照会します
パラメーター：
account：アカウント名またはID
contractNameOrId：コントラクト名またはID
callback：コールバック関数
[block:api-header]
{
  "title": "その他"
}
[/block]
**サブスクリプションの停止**
関数：unsubscribe
機能：サブスクリプションを停止します
パラメーター：
method(Array)：停止するサブスクリプション方法。例えば、ブロック情報や取引情報のサブスクリプションを停止する場合は['subscribeToBlocks','subscribeToBlocks']に設定します。空に設定するとすべてのサブスクリプションを停止します。この方法ではcallbackを機能しないとpromiseをリターンします。
備考：特定ユーザーのサブスクリプションを停止する場合、パラメーターを['subscribeToAccountOperation|account']に設定してください。
callback：コールバック関数

**取引メモの暗号化**
関数：decodeMemo
機能：コールバックしなく、結果のみリターンします。リターンした結果は、メモのtext付きのオブジェクトです。
例：bcl.decodeMemo(raw_data.memo)、raw_dataは取引のソースデータです。

**取引のベース手数料を照会**
関数：queryTransactionBaseFee
機能：取引のベース手数料情報を照会します
パラメーター：
transactionType：取引タイプ、例えばtransfer
feeAssetId：手数料を支払うトークンのシンボルまたはID
callback：APIパラメーターの説明
[block:api-header]
{
  "title": "transaction Type一覧"
}
[/block]

[block:parameters]
{
  "data": {
    "h-0": "transactionType",
    "h-1": "API",
    "0-0": "transfer",
    "0-1": "transferAsset",
    "1-0": "account_create",
    "1-1": "createAccountWithPassword",
    "2-0": "account_update",
    "2-1": "changePassword",
    "3-0": "account_upgrade",
    "3-1": "upgradeAccount",
    "4-0": "asset_create",
    "4-1": "createAsset",
    "5-0": "asset_issue",
    "5-1": "issueAsset",
    "6-0": "proposal_update",
    "6-1": "submitProposal",
    "7-0": "vesting_balance_withdraw",
    "7-1": "claimVestingBalance",
    "8-0": "contract_create",
    "8-1": "createContract",
    "9-0": "call_contract_function",
    "9-1": "callContractFunction",
    "10-0": "call_contract_function",
    "10-1": "callContractFunction",
    "11-0": "register_creator",
    "11-1": "registerCreator",
    "12-0": "creat_world_view",
    "12-1": "creatWorldView",
    "13-0": "propose_relate_world_view",
    "13-1": "proposeRelateWorldView",
    "14-0": "creat_nh_asset",
    "14-1": "creatNHAsset",
    "15-0": "delete_nh_asset",
    "15-1": "delete_nh_asset",
    "16-0": "transfer_nh_asset",
    "16-1": "transferNHAsset",
    "17-0": "transfer_nh_asset",
    "17-1": "transferNHAsset",
    "18-0": "transfer_nh_asset",
    "18-1": "transferNHAsset",
    "19-0": "creat_nh_asset_order",
    "19-1": "creatNHAssetOrder",
    "20-0": "cancel_nh_asset_order",
    "20-1": "cancelNHAssetOrder",
    "21-0": "fill_nh_asset_order",
    "22-0": "limit_order_create",
    "21-1": "fillNHAssetOrder",
    "22-1": "createLimitOrder",
    "23-0": "limit_order_cancel",
    "23-1": "cancelLimitOrder"
  },
  "cols": 2,
  "rows": 24
}
[/block]

[block:api-header]
{
  "title": "GitHub"
}
[/block]
[JSSDK](https://github.com/Cocos-BCX/JSSDK)