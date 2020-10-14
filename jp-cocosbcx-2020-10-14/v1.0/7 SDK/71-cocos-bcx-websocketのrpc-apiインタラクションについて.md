---
title: "7.1 Cocos-BCX websocketのRPC APIインタラクションについて"
slug: "71-cocos-bcx-websocketのrpc-apiインタラクションについて"
excerpt: "Cocos-BCXチェーンはogin_api、database_api、network_broadcast_apiとhistory_apiを提供しています"
hidden: false
createdAt: "2019-11-20T11:29:38.881Z"
updatedAt: "2019-11-20T12:14:21.893Z"
---
[block:api-header]
{
  "title": "一、基本データ構造"
}
[/block]
**1．データ構造の送信**

**例** 
[block:code]
{
  "codes": [
    {
      "code": "{\"method\": \"call\", \"params\": [api_id, \"関数名\", [パラメーター]], \"id\": 2}",
      "language": "json"
    }
  ]
}
[/block]
**パラメーター説明：**
 method：call
params：api_id：関数が所属するapiと対応するid；関数名：RPC関数名；パラメーター：RPC関数と対応するパラメーター
id：カスタマイズメッセージid、アプリ内でメンテナンスを行います。用途：アプリ開発者が区別しやすいため、オンチェーンのメッセージレスポンスはこのidを返送します。

**2．データ構造のリターン**

**例** 
[block:code]
{
  "codes": [
    {
      "code": "{\"id\":2,\"jsonrpc\":\"2.0\",\"result\":\"\"}",
      "language": "json"
    }
  ]
}
[/block]
**パラメーター説明：**
id：送信idと対応します；
jaonrpc：apiと対応するRPCバージョン
result：リターンしたデータセット（任意データ構造）
[block:api-header]
{
  "title": "二、login_api"
}
[/block]
説明：ノードが配置したパスワードを確認してからloginします。apiに使用権限を設けず、database_api、history_api、network_broadcast_apiのコールが可能です。

**1．login**

**説明**
apiのコール権限をアクセスします。デフォルト設定として、すべての人はdatabase_api、network_broadcast_api、history_api、block_api、asset_apiをコールできます。
**パラメーター**
api_id：デフォルト設定は1；
関数名：login；
パラメーター：ユーザー名、パスワードのデフォルト設定は空；
**例：**
[block:code]
{
  "codes": [
    {
      "code": "{\"method\":\"call\",\"params\":[1,\"login\",[\"\",\"\"]],\"id\":1}",
      "language": "json"
    }
  ]
}
[/block]
**2．database**

**説明**
database_api_idを入手します。
**パラメーター**
api_id：デフォルト設定は1；
関数名：database；
パラメーター：無；
**例**
[block:code]
{
  "codes": [
    {
      "code": "{\"method\":\"call\",\"params\":[1,\"database\",[]],\"id\":2}",
      "language": "json"
    }
  ]
}
[/block]
**3．network_broadcast**

**説明**
network_broadcast_api_idを入手します。
**パラメーター：**
api_id：デフォルト設定は1；
パラメーター：network_broadcast；
パラメーター：無；
**例** 
[block:code]
{
  "codes": [
    {
      "code": "{\"method\":\"call\",\"params\":[1,\"network_broadcast\",[]],\"id\":3}",
      "language": "json"
    }
  ]
}
[/block]
**4．history**

**説明**
history_api_idを入手します。
**パラメーター：**
api_id：デフォルト設定は1；
関数名：history；
パラメーター：無；
**例**
[block:code]
{
  "codes": [
    {
      "code": "{\"method\":\"call\",\"params\":[1,\"history\",[]],\"id\":4}",
      "language": "json"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "三、database_api"
}
[/block]
説明：database_apiは主にログインなしの照会リクエストに使用します。

**1．get_chain_id**

**説明**
チェーンIDを照会します。
**パラメーター：**
api_id：database_api_id（databaseから確認できます）；
関数名：get_chain_id；
パラメーター：無；
**例**
[block:code]
{
  "codes": [
    {
      "code": "{\"method\":\"call\",\"params\":[2,\"get_chain_id\",[]],\"id\":5}",
      "language": "json"
    }
  ]
}
[/block]
**2．lookup_account_names**

**説明**
アカウントでアカウント情報を照会します。
**パラメーター**
api_id：database_api_id（databaseから確認できます）；
関数名：lookup_account_names；
パラメーター：アカウント名；
**例**
[block:code]
{
  "codes": [
    {
      "code": "{\"id\":7,\"method\":\"call\",\"params\":[2,\"lookup_account_names\",[[\"test1\"]]]}",
      "language": "json"
    }
  ]
}
[/block]
**3．get_accounts**

**説明**
アカウントidでアカウント情報を照会します。
**パラメーター
**api_id：database_api_id（databaseから確認できます）；
関数名：get_accounts；
パラメーター：アカウントID；
**例** 
[block:code]
{
  "codes": [
    {
      "code": "{\"id\":9,\"method\":\"call\",\"params\":[2,\"get_accounts\",[[\"1.2.19\"]]]}",
      "language": "json"
    }
  ]
}
[/block]
**4．get_full_accounts**

**説明**
アカウントidからアカウント情報を照会します
**パラメーター**
api_id：database_api_id（databaseから確認できます）；
関数名：get_full_accounts；
パラメーター：アカウント名またはidからアカウント情報を照会します；
**例** 
[block:code]
{
  "codes": [
    {
      "code": "{\"id\":30,\"method\":\"call\",\"params\":[2,\"get_full_accounts\",[[\"gnkhandsome1\"],false]]}",
      "language": "json"
    }
  ]
}
[/block]
**5．get_objects**

**説明**
idからidと対応するデータを照会します。（アカウントidはアカウント情報と対応し、アセットidはアセットデータと対応します）
**パラメーター**
api_id：database_api_id（databaseから確認できます）；
関数名：get_objects；
パラメーター：照会する項目id；
**例**
[block:code]
{
  "codes": [
    {
      "code": "{\"id\":10,\"method\":\"call\",\"params\":[2,\"get_objects\",[[\"1.2.19\"]]]}",
      "language": "json"
    }
  ]
}
[/block]
**6．get_key_references**

**説明**
idからidと対応するデータを照会します。（アカウントidはアカウント情報と対応し、アセットidはアセットデータと対応します）**
パラメーター**
api_id：database_api_id（databaseから確認できます）；
関数名：get_key_references；
パラメーター：keyと対応するアカウントid；
**例**
[block:code]
{
  "codes": [
    {
      "code": "{\"id\":14,\"method\":\"call\",\"params\":[2,\"get_key_references\",[[\"COCOS5jY5exmyKNPXU8WsTPekoFbL5vQXkHuRdbudG2144AmoYWGxGo\",\"COCOS7MCzNJ3q3d4p2ie7rw1EcZBhdCg4g9ty6BcqZirNtDBENvJSws\"]]]}",
      "language": "json"
    }
  ]
}
[/block]
**7．lookup_asset_symbols**

**説明**
アセットIDまたはアセットシンボルからアセット情報を照会します。
**パラメーター**
api_id：database_api_id（databaseから確認できます）；
関数名：lookup_asset_symbols；
パラメーター：アセットIDまたはアセットシンボル
**例** 
[block:code]
{
  "codes": [
    {
      "code": "{\"id\":19,\"method\":\"call\",\"params\":[2,\"lookup_asset_symbols\",[[\"COCOS\"]]]}",
      "language": "json"
    }
  ]
}
[/block]
**8．get_assets**

**説明**
アセットIDからアセット情報を照会します。
**パラメーター**
api_id：database_api_id（databaseから確認できます）；
関数名：get_assets；
パラメーター：アセットID
**例** 
[block:code]
{
  "codes": [
    {
      "code": "{\"id\": 22,\"method\":\"call\",\"params\":[0,\"get_assets\",[[\"1.3.0\"]]]}",
      "language": "json"
    }
  ]
}
[/block]
**9．list_assets**

**説明**
アルファベット順でオンチェーンアセット情報をリスティングします。
**パラメーター**
api_id：database_api_id（databaseから確認できます）；
関数名：list_assets；
パラメーター："A"：Aからリスティングします；100：数量；
**例** 
[block:code]
{
  "codes": [
    {
      "code": "{\"method\":\"call\",\"params\":[2,\"list_assets\",[\"A\",100]],\"id\":42}",
      "language": "json"
    }
  ]
}
[/block]
**10．get_dynamic_global_properties**

**説明**
チェーンのダイナミックなグローバルプロパティを確認します。ヘッドブロック番号、次の証人などブロック間隔情報の変更も含みます。
**パラメーター**
api_id：database_api_id（databaseから確認できます）；
関数名：get_dynamic_global_properties；
パラメーター：無；
**例** 
[block:code]
{
  "codes": [
    {
      "code": "{\"id\":26,\"method\":\"call\",\"params\":[2,\"get_dynamic_global_properties\",[]]}",
      "language": "json"
    }
  ]
}
[/block]
**11．get_global_properties**

**説明**
チェーンのグローバルプロパティを確認します。アクティブ証人リスト、委員会メンバー、間隔の阻止など変更されたチェーン属性やメンテナンス期間（一日に一回）で一回だけ変更された属性も含みます。
**パラメーター**
api_id：database_api_id（databaseから確認できます）；
関数名：get_global_properties；
パラメーター：無；
**例** 
[block:code]
{
  "codes": [
    {
      "code": "{\"id\":10,\"method\":\"call\",\"params\":[2,\"get_objects\",[[\"1.2.19\"]]]}",
      "language": "json"
    }
  ]
}
[/block]
**12．get_block_header**

**説明**
ヘッドブロック情報を照会します。
**パラメーター**
api_id：database_api_id（databaseから確認できます）；
関数名：get_block_header；
パラメーター：ブロック番号
**例** 
[block:code]
{
  "codes": [
    {
      "code": "{\"method\":\"call\",\"params\":[2,\"get_block_header\",[\"537581\"]],\"id\":43}",
      "language": "json"
    }
  ]
}
[/block]
**13．get_block**

**説明**
ブロック情報を照会します。
**パラメーター**
api_id：database_api_id（databaseから確認できます）；
関数名：get_block；
パラメーター：ブロック番号；
**例** 
[block:code]
{
  "codes": [
    {
      "code": "{\n  \"id\": 21,\n  \"method\": \"call\",\n  \"params\": [\n      0,\n      \"get_block\",\n      [\n          \"390096\"\n      ]\n  ]\n}",
      "language": "json"
    }
  ]
}
[/block]
**14．get_contract**

**説明**
コントラクト名またはIDからコントラクト情報を照会します。
**パラメーター**
api_id：database_api_id（databaseから確認できます）；
関数名：get_contract；
関数：コントラクト名またはID；
**例** 
[block:code]
{
  "codes": [
    {
      "code": "{\"method\":\"call\",\"params\":[2,\"get_contract\",[\"contract.hahaha\"]],\"id\":22}",
      "language": "json"
    }
  ]
}
[/block]
**15．get_account_balances**

**説明**
アカウント内すべてのアセットまたは指定アセットの残高を照会します。
**パラメーター**
api_id：database_api_id（databaseから確認できます）；
関数名：get_account_balances；
パラメーター：1.2.19：アカウントID；[“1.3.0”]：アセットid。（空に設定すると、すべてのアセット残高を照会します）；
**例** 
[block:code]
{
  "codes": [
    {
      "code": "Check all assets balance of the account.\n{\"id\":10,\"method\":\"call\",\"params\":[2,\"get_account_balances\",[\"1.2.19\",[]]]}\nCheckdesignated assets balance of the account.\n{\"id\":8,\"method\":\"call\",\"params\":[2,\"get_account_balances\",[\"1.2.19\",[\"1.3.0\"]]]}",
      "language": "json"
    }
  ]
}
[/block]
**16．lookup_nh_asset**

**説明**
NHアセットIDまたはhashからアセット情報を照会します。
**パラメーター**
api_id：database_api_id（databaseから確認できます）；
関数名：lookup_nh_asset；
パラメーター：NHアセットIDまたはhash；
**例** 
[block:code]
{
  "codes": [
    {
      "code": "{\"method\":\"call\",\"params\":[2,\"lookup_nh_asset\",[[\"4.2.0\"]]],\"id\":97}",
      "language": "json"
    }
  ]
}
[/block]
**17．list_account_nh_asset**

**説明**
アカウント内すべてのNHアセットをリスティングします。
**パラメーター**
api_id：database_api_id（databaseから確認できます）；
関数名：list_account_nh_asset；
パラメーター
WORLD_VIEW：世界観名（任意項目）；
10：pageSize
1：page
4：クエリタイプ（使用権と所有権によって、5つのタイプがあります。enum class nh_asset_list_type {only_active = 0, //レンタルアセットのみリスティングしますonly_owner = 1, //リースアセットのみリスティングします all_active = 2, //すべての利用可能なアセットall_owner = 3, //所有しているすべてのアセットowner_and_active = 4 //所有権と使用権両方を持っています}；
**例**
[block:code]
{
  "codes": [
    {
      "code": "Check account NH assets of which its universe is world-view\n{\"method\":\"call\",\"params\":[2,\"list_account_nh_asset\",[\"1.2.19\",[\"WORLD_VIEW\"],\"10\",\"1\",4]],\"id\":105}\nCheck the NH assets of the account\n{\"method\":\"call\",\"params\":[2,\"list_account_nh_asset\",[\"1.2.19\",[],\"10\",\"1\",4]],\"id\":107}",
      "language": "json"
    }
  ]
}
[/block]
**18．list_account_nh_asset_order**

**説明**
アカウント内NHアセットのオーダーをリスティングします。
**関数名**
api_id：database_api_id（databaseから確認できます）；
関数名：list_account_nh_asset_order；
パラメーター：
1.2.19：アカウントid；
10：pageSize；
1：page
**例** 
[block:code]
{
  "codes": [
    {
      "code": "{\"method\":\"call\",\"params\":[2,\"list_account_nh_asset_order\",[\"1.2.19\",10,1]],\"id\":128}",
      "language": "json"
    }
  ]
}
[/block]
**19．list_nh_asset_order**

**説明**
NHアセットのオーダーをリスティングします。
**パラメーター**
api_id：database_api_id（databaseから確認できます）；
関数名：list_nh_asset_order；
パラメーター
COCOS（任意項目）：通貨；
GNK（任意項目）：世界観；
“{\”name\”:\”gnkhandsome\”}（任意項目）”：基本データ；
10 ： pageSize;
1 : page ;
true：昇順であるかどうか、trueは昇順で、falseは降順です。
**例** 
[block:code]
{
  "codes": [
    {
      "code": "{\"method\":\"call\",\"params\":[2,\"list_nh_asset_order\",  [\"\",\"\",\"\",10,1,true]],\"id\":168}\n\n{\"method\":\"call\",\"params\":[2,\"list_nh_asset_order\",[\"COCOS\",\"GNK\",\"      {\\\"name\\\":\\\"gnkhandsome\\\"}\",10,1,true]],\"id\":176}",
      "language": "json"
    }
  ]
}
[/block]
**20．lookup_world_view**

**説明**
世界観名またはIDから世界観情報を照会します。
**パラメーター**
api_id：database_api_id（databaseから確認できます）；
関数名：lookup_world_view；
パラメーター：“GNK”：世界観；
**例** 
[block:code]
{
  "codes": [
    {
      "code": "{\"method\":\"call\",\"params\":[2,\"lookup_world_view\",[[\"GNK\"]]],\"id\":189}",
      "language": "json"
    }
  ]
}
[/block]
**21．get_nh_creator**

**説明**
アカウント名またはIDから開発者に関係付けた世界観を確認します。
**パラメーター**
api_id：database_api_id（databaseから確認できます）；
関数名：get_nh_creator；
パラメーター：“1.2.19”：アカウントid；
**例** 
[block:code]
{
  "codes": [
    {
      "code": "{\"method\":\"call\",\"params\":[2,\"get_nh_creator\",[\"1.2.19\"]],\"id\":434}",
      "language": "json"
    }
  ]
}
[/block]
**22．list_nh_asset_by_creator**

**説明**
開発者が作成したNHアセットをリスティングします。
**パラメーター**
api_id：database_api_id（databaseから確認できます）；
関数名：list_nh_asset_by_creator；
パラメーター
“1.2.19” :アカウントid；
“WORLD_VIEW”：世界観
10：pageSize；
1：page；
**例** 
[block:code]
{
  "codes": [
    {
      "code": "{\"method\":\"call\",\"params\":[2,\"list_nh_asset_by_creator\",[\"1.2.19\",\"WORLD_VIEW\",\"10\",\"1\"]],\"id\":17}",
      "language": "json"
    }
  ]
}
[/block]
**23．get_transaction_by_id**

**説明**
取引hashから取引情報を入手します。
**パラメーター**
api_id：database_api_id（databaseから確認できます）；
関数名：get_transaction_by_id；
パラメーター：get_transaction_by_id；
パラメーター：取引hash
**例** 
[block:code]
{
  "codes": [
    {
      "code": "{\"method\":\"call\",\"params\":[2,\"get_transaction_by_id\",[\"a5507f83a825d262217ca8006bbf5de1332184d3d80df51880984580609f06fb\"]],\"id\":516}",
      "language": "json"
    }
  ]
}
[/block]
**24．get_transaction_in_block_info**

**説明**
取引が発生したブロックの位置情報を入手します。
**パラメーター**
api_id：database_api_id（databaseから確認できます）；
関数名：get_transaction_in_block_info；
パラメーター：取引hash
**例** 
[block:code]
{
  "codes": [
    {
      "code": "{\"method\":\"call\",\"params\":[2,\"get_transaction_by_id\",[\"a5507f83a825d262217ca8006bbf5de1332184d3d80df51880984580609f06fb\"]],\"id\":516}",
      "language": "json"
    }
  ]
}
[/block]
**25．get_limit_orders**

**説明**
取引所の指値注文の取引ペア情報を入手します。
**パラメーター**
api_id：database_api_id（databaseから確認できます）；
関数名：get_limit_orders；
パラメーター：TEST_COCOS（COCOSトークンを取引するためのテストトークン）
1.3.0：1.3.0トークン取引所；
1.3.1：1.3.0トークン取引所の1.3.1トークン；
500：指値注文数
**例** 
[block:code]
{
  "codes": [
    {
      "code": "{\"method\":\"call\",\"params\":[2,\"get_limit_orders\",[\"1.3.0\",\"1.3.1\",500]],\"id\":547}",
      "language": "json"
    }
  ]
}
[/block]
**26．estimation_gas**

**説明**
推定GAS代を確認します。
**パラメーター**
api_id：database_api_id（databaseから確認できます）；
関数名：estimation_gas；
パラメーター：
amount：抵当量
asset_id：抵当アセットid
**例** 
[block:code]
{
  "codes": [
    {
      "code": "{\"method\":\"call\",\"params\":[2,\"estimation_gas\",   [{\"amount\":1000000,\"asset_id\":\"1.3.0\"}]],\"id\":575}",
      "language": "json"
    }
  ]
}
[/block]

[block:code]
{
  "codes": [
    {
      "code": "",
      "language": "text"
    }
  ]
}
[/block]
**27．get_vesting_balances**

**説明**
受取待ちのGAS代またはブロック生成インセンティブを確認します。
**パラメーター**
api_id：database_api_id（databaseから確認できます）；
関数名：get_vesting_balances；
パラメーター：
1.2.19：アカウントid；
**例** 
[block:code]
{
  "codes": [
    {
      "code": "{\"method\":\"call\",\"params\":[2,\"get_vesting_balances\",[\"1.2.19\"]],\"id\":581}",
      "language": "json"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "四、history_api"
}
[/block]
説明：history_apiは操作履歴を照会するためのインタフェースです。

**1．get_account_history**

**説明**
指定アカウントに対する直近操作履歴を照会します。
**パラメーター**
api_id：database_api_id（databaseから確認できます）；
関数名：get_account_history；
パラメーター：
1.2.19：アカウントid；
**例** 
[block:code]
{
  "codes": [
    {
      "code": "{\"method\":\"call\",\"params\":[4,\"get_account_history\",[\"1.2.19\",\"1.11.0\",100,\"1.11.0\"]],\"id\":549}",
      "language": "json"
    }
  ]
}
[/block]
**2．get_fill_order_history**

**説明**
取引所の指値注文の取引履歴を照会します。
**パラメーター**
api_id：database_api_id（databaseから確認できます）；
関数名：get_fill_order_history；
パラメーター：
1.3.0：1.3.0トークン取引所；
1.3.1：1.3.0トークン取引所の1.3.1トークン；
200：指値注文数
**例** 
[block:code]
{
  "codes": [
    {
      "code": "{\"method\":\"call\",\"params\":[4,\"get_fill_order_history\",[\"1.3.0\",\"1.3.1\",200]],\"id\":548}",
      "language": "json"
    }
  ]
}
[/block]

[block:code]
{
  "codes": [
    {
      "code": "",
      "language": "text"
    }
  ]
}
[/block]
**3．get_market_history**

**説明**
取引所の一定期間内の市況情報を確認します。
**パラメーター**
api_id：database_api_id（databaseから確認できます）；
関数名：get_market_history；
パラメーター：
1.3.0：1.3.0トークン取引所；
1.3.1：1.3.0トークン取引所の1.3.1トークン；
84600：期間
2019-10-10T06:56:11 :開始時間
2019-10-12T06:56:11 ：終了時間
**例** 
[block:code]
{
  "codes": [
    {
      "code": "{\"method\":\"call\",\"params\":[4,\"get_market_history\",[\"1.3.0\",\"1.3.1\",86400,\"2019-10-10T06:56:11\",\"2019-10-12T06:56:11\"]],\"id\":661}",
      "language": "json"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "五、network_broadcast_api"
}
[/block]
説明：network_broadcast_apiはユーザー署名が必要なすべてのオンチェーン操作を対応します。

**1．broadcast_transaction_with_callback**

**説明**
操作のソースデータやデータ署名を送信する関数です
**パラメーター**
api_id：network_broadcast_api（network_broadcastから確認できます）；
関数名：broadcast_transaction_with_callback；
パラメーター：（操作によって異なりますので、操作例をご確認ください）；

**基本データ例及びパラメーター説明** 
[block:code]
{
  "codes": [
    {
      "code": "{\n    \"method\":\"call\",\n    \"params\":[\n        3(network_broadcast_api is obtained by checking network_broadcast),\n        \"broadcast_transaction_with_callback\"(Function name:),\n        [\n            48 （this id is a custom message id）,\n            {\n                \"ref_block_num\":25492,\n                \"ref_block_prefix\":2286421322,\n                \"expiration\":\"2019-10-12T09:04:26\",\n                （ref_block_num, ref_block_prefix, expiration is obtained by checking get_dynamic_global_properties）\n                \"operations\":[\n                    [\n                        7（opertaion ID，used to identify the operation, different operations correspond to different operation IDs）,\n                        {\n                            \"account_to_upgrade\":\"1.2.19\",\n                            \"upgrade_to_lifetime_member\":true,\n                            \"extensions\":[\n                            ]\n                           （operation data，different data needs different operation）\n                         }\n                     ]\n                ],\n                \"extensions\":[\n                ],\n                \"signatures\":[ \"1f3630fe1a044bc2afbb0c684e737481c87b638e143ef66e8e1346d03451ce158932a54a32990264f236e5e0452bcecc52e43f67438237905acfaeda4bbba4aebf\"\n                ] （signatures: generated from the user's private key to data summary）\n            }\n        ]\n    ]，\n        \"id\":48\n}",
      "language": "json"
    }
  ]
}
[/block]
**2．終身会員にアップグレードします**

**例** 
[block:code]
{
  "codes": [
    {
      "code": "{\n  \"method\":\"call\",\n  \"params\":[\n      3,\n      \"broadcast_transaction_with_callback\",\n      [\n          48,\n          {\n              \"ref_block_num\":25492,\n              \"ref_block_prefix\":2286421322,\n              \"expiration\":\"2019-10-12T09:04:26\",\n              \"operations\":[\n                  [\n                      7,\n                      {\n                          \"account_to_upgrade\":\"1.2.19\",\n                          \"upgrade_to_lifetime_member\":true,\n                          \"extensions\":[\n\n                          ]\n                      }\n                  ]\n              ],\n              \"extensions\":[\n\n              ],\n              \"signatures\":[                \"1f3630fe1a044bc2afbb0c684e737481c87b638e143ef66e8e1346d03451ce158932a54a32990264f236e5e0452bcecc52e43f67438237905acfaeda4bbba4aebf\"\n              ]\n          }\n      ]\n  ],\n  \"id\":48\n}",
      "language": "json"
    }
  ]
}
[/block]
**3．振込**

**例** 
[block:code]
{
  "codes": [
    {
      "code": "{\n    \"id\":13,\n    \"method\":\"call\",\n    \"params\":[\n        4,\n        \"broadcast_transaction\",\n        [\n            {\n                \"signatures\":[\n                    \"1b1a84246c6360719f4411cfeeb678a686e489982f82d1e797ad60060e618a6e305172d6788cf9dd877ba087a5f547c846656f4bd0dd38fe3cc42ee8c7a5956d8a\"\n                ],\n                \"expiration\":\"2019-10-16T05:08:08\",\n                \"extensions\":[\n\n                ],\n                \"operations\":[\n                    [\n                        0,\n                        {\n                            \"amount\":{\n                                \"amount\":200000,\n                                \"asset_id\":\"1.3.0\"\n                            },\n                            \"extensions\":[\n\n                            ],\n                            \"from\":\"1.2.19\",\n                            \"memo\":{\n                                \"from\":\"COCOS7MCzNJ3q3d4p2ie7rw1EcZBhdCg4g9ty6BcqZirNtDBENvJSws\",\n                                \"message\":\"6a77d9bfed718aff95ae7f6f503fa564\",\n                                \"nonce\":13763002032446693210,\n                                \"to\":\"COCOS4wkoXsipL5dXNy85TFUaJqJydMzcaMvbYNR8a5EXnc5KLQZz3w\"\n                            },\n                            \"to\":\"1.2.20\"\n                        }\n                    ]\n                ],\n                \"ref_block_num\":59572,\n                \"ref_block_prefix\":1114595117\n            }\n        ]\n    ]\n}\n",
      "language": "json"
    }
  ]
}
[/block]
**4．デジタルアセットを作成します**

**例** 
[block:code]
{
  "codes": [
    {
      "code": "{\n    \"method\":\"call\",\n    \"params\":[\n        3,\n        \"broadcast_transaction_with_callback\",\n        [\n            94,\n            {\n                \"ref_block_num\":25826,\n                \"ref_block_prefix\":2156015147,\n                \"expiration\":\"2019-10-12T09:15:35\",\n                \"operations\":[\n                    [\n                        8,\n                        {\n                            \"issuer\":\"1.2.19\",\n                            \"symbol\":\"GNK\",\n                            \"precision\":5,\n                            \"common_options\":{\n                                \"max_supply\":\"1000000000\",\n                                \"market_fee_percent\":0,\n                                \"max_market_fee\":\"0\",\n                                \"issuer_permissions\":15,\n                                \"flags\":0,\n                                \"description\":\"{\"main\":\"\",\"short_name\":\"\",\"market\":\"\"}\",\n                                \"extensions\":[\n\n                                ]\n                            },\n                            \"extensions\":[\n\n                            ]\n                        }\n                    ]\n                ],\n                \"extensions\":[\n\n                ],\n                \"signatures\":[\n                    \"1f6b450f1db977fed6409bb2452daca03a67bfe942772223b3e1a43fdc1200de1e3f903fd05882bc88053dfd9860cbbc96a29e9ea1f61411b8c7c404f079b6189d\"\n                ]\n            }\n        ]\n    ],\n    \"id\":94\n}",
      "language": "json"
    }
  ]
}
[/block]
**5．アセットをリリースします**

**例** 
[block:code]
{
  "codes": [
    {
      "code": "{\n    \"method\":\"call\",\n    \"params\":[\n        3,\n        \"broadcast_transaction_with_callback\",\n        [\n            28,\n            {\n                \"ref_block_num\":35359,\n                \"ref_block_prefix\":2246203291,\n                \"expiration\":\"2019-10-14T03:06:16\",\n                \"operations\":[\n                    [\n                        13,\n                        {\n                            \"issuer\":\"1.2.19\",\n                            \"asset_to_issue\":{\n                                \"amount\":\"1000000000\",\n                                \"asset_id\":\"1.3.6\"\n                            },\n                            \"issue_to_account\":\"1.2.19\",\n                            \"extensions\":[\n\n                            ]\n                        }\n                    ]\n                ],\n                \"extensions\":[\n\n                ],\n                \"signatures\":[\n                    \"20595dc07b4ed0ede052754e9ca22d63ec6196da325cb97524ce460d90e71dad8948c737bf1bfaa389fb1aad217109d41cc5637c4afaa550061caf1d08d5136143\"\n                ]\n            }\n        ]\n    ],\n    \"id\":28\n}",
      "language": "json"
    }
  ]
}
[/block]
**6．アセットを削除します**

**例** 
[block:code]
{
  "codes": [
    {
      "code": "{\n    \"method\":\"call\",\n    \"params\":[\n        3,\n        \"broadcast_transaction_with_callback\",\n        [\n            42,\n            {\n                \"ref_block_num\":35414,\n                \"ref_block_prefix\":2161905183,\n                \"expiration\":\"2019-10-14T03:08:07\",\n                \"operations\":[\n                    [\n                        14,\n                        {\n                            \"payer\":\"1.2.19\",\n                            \"amount_to_reserve\":{\n                                \"amount\":\"100000\",\n                                \"asset_id\":\"1.3.6\"\n                            },\n                            \"extensions\":[\n\n                            ]\n                        }\n                    ]\n                ],\n                \"extensions\":[\n\n                ],\n                \"signatures\":[\n                    \"1f70bdccc124bf90ed014af83684a033a678cd1998695c7cfb040e98133da0cc8142f2e01bbdbbd0b6bff8cf6551acc06453d6fd9d2cc9f3de8ace746c476342c6\"\n                ]\n            }\n        ]\n    ],\n    \"id\":42\n}",
      "language": "json"
    }
  ]
}
[/block]
**7．ステークgas**

**例** 
[block:code]
{
  "codes": [
    {
      "code": "{\n    \"method\":\"call\",\n    \"params\":[\n        3,\n        \"broadcast_transaction_with_callback\",\n        [\n            106,\n            {\n                \"ref_block_num\":35970,\n                \"ref_block_prefix\":1563481302,\n                \"expiration\":\"2019-10-14T03:26:38\",\n                \"operations\":[\n                    [\n                        54,\n                        {\n                            \"mortgager\":\"1.2.19\",\n                            \"beneficiary\":\"1.2.19\",\n                            \"collateral\":\"1000000\"\n                        }\n                    ]\n                ],\n                \"extensions\":[\n\n                ],\n                \"signatures\":[\n                    \"1f5beabcb0ae6a495ca1d2bbe9fe99b79dbf3ae95694d90738a9a620b9c3fbd486640a5f65b2378308dad63e2817d9d96772648a65444b6e4bd3521ac7940e593c\"\n                ]\n            }\n        ]\n    ],\n    \"id\":106\n}",
      "language": "json"
    }
  ]
}
[/block]
**8．開発者として登録します**

**例** 
[block:code]
{
  "codes": [
    {
      "code": "{\n    \"method\":\"call\",\n    \"params\":[\n        3,\n        \"broadcast_transaction_with_callback\",\n        [\n            173,\n            {\n                \"ref_block_num\":36710,\n                \"ref_block_prefix\":1117181228,\n                \"expiration\":\"2019-10-14T03:51:25\",\n                \"operations\":[\n                    [\n                        37,\n                        {\n                            \"fee_paying_account\":\"1.2.19\"\n                        }\n                    ]\n                ],\n                \"extensions\":[\n\n                ],\n                \"signatures\":[\n                    \"20251b5d09a70a5202795d01b9fdc402dbed4022a9c34ae9f432456a7ca834fa8e14d6ca44b1f7454bb694cfd0856c2083be203b7b3c4aee23a68398ff3c58e3bc\"\n                ]\n            }\n        ]\n    ],\n    \"id\":173\n}",
      "language": "json"
    }
  ]
}
[/block]
**9．世界観を作成します**

**例** 
[block:code]
{
  "codes": [
    {
      "code": "{\n    \"method\":\"call\",\n    \"params\":[\n        3,\n        \"broadcast_transaction_with_callback\",\n        [\n            182,\n            {\n                \"ref_block_num\":36728,\n                \"ref_block_prefix\":2052004780,\n                \"expiration\":\"2019-10-14T03:52:00\",\n                \"operations\":[\n                    [\n                        38,\n                        {\n                            \"fee_paying_account\":\"1.2.19\",\n                            \"world_view\":\"GNK\"\n                        }\n                    ]\n                ],\n                \"extensions\":[\n\n                ],\n                \"signatures\":[\n                    \"20623e8670ba63425f7f21140f59611791c3961591649e75a353b0aa47c1f6d9ad22bb5a0f5da69df4a23a6fd400bbf5e6df6cf79d7abadcacdc179a0e3744c70b\"\n                ]\n            }\n        ]\n    ],\n    \"id\":182\n}",
      "language": "json"
    }
  ]
}
[/block]
**10．世界観提議と関係付けします**

**例** 
[block:code]
{
  "codes": [
    {
      "code": "{\n    \"method\":\"call\",\n    \"params\":[\n        3,\n        \"broadcast_transaction_with_callback\",\n        [\n            197,\n            {\n                \"ref_block_num\":36743,\n                \"ref_block_prefix\":909075952,\n                \"expiration\":\"2019-10-14T03:52:31\",\n                \"operations\":[\n                    [\n                        20,\n                        {\n                            \"fee_paying_account\":\"1.2.19\",\n                            \"expiration_time\":\"2019-10-15T03:52:16\",\n                            \"proposed_ops\":[\n                                {\n                                    \"op\":[\n                                        39,\n                                        {\n                                            \"related_account\":\"1.2.26\",\n                                            \"world_view\":\"SYLING\",\n                                            \"view_owner\":\"1.2.21\"\n                                        }\n                                    ]\n                                }\n                            ],\n                            \"extensions\":[\n\n                            ]\n                        }\n                    ]\n                ],\n                \"extensions\":[\n\n                ],\n                \"signatures\":[\n                    \"207080641c762d168dce4ab4ee03906276a071ae181a28f2e2e2b6294824776a9d3373982dd68826e7655796ad80a1d7d3927e9353cb414271a1c817f555cfa33c\"\n                ]\n            }\n        ]\n    ],\n    \"id\":197\n}",
      "language": "json"
    }
  ]
}
[/block]
**11．NHアセットを作成します**

**例** 
[block:code]
{
  "codes": [
    {
      "code": "{\n    \"method\":\"call\",\n    \"params\":[\n        3,\n        \"broadcast_transaction_with_callback\",\n        [\n            227,\n            {\n                \"ref_block_num\":36837,\n                \"ref_block_prefix\":1896194324,\n                \"expiration\":\"2019-10-14T03:55:39\",\n                \"operations\":[\n                    [\n                        40,\n                        {\n                            \"fee_paying_account\":\"1.2.19\",\n                            \"owner\":\"1.2.19\",\n                            \"asset_id\":\"COCOS\",\n                            \"world_view\":\"GNK\",\n                            \"base_describe\":\"{\"name\":\"hahah\"}\"\n                        }\n                    ],\n                    [\n                        40,\n                        {\n                            \"fee_paying_account\":\"1.2.19\",\n                            \"owner\":\"1.2.19\",\n                            \"asset_id\":\"COCOS\",\n                            \"world_view\":\"GNK\",\n                            \"base_describe\":\"{\"name\":\"hahah\"}\"\n                        }\n                    ],\n                    [\n                        40,\n                        {\n                            \"fee_paying_account\":\"1.2.19\",\n                            \"owner\":\"1.2.19\",\n                            \"asset_id\":\"COCOS\",\n                            \"world_view\":\"GNK\",\n                            \"base_describe\":\"{\"name\":\"hahah\"}\"\n                        }\n                    ],\n                    [\n                        40,\n                        {\n                            \"fee_paying_account\":\"1.2.19\",\n                            \"owner\":\"1.2.19\",\n                            \"asset_id\":\"COCOS\",\n                            \"world_view\":\"GNK\",\n                            \"base_describe\":\"{\"name\":\"hahah\"}\"\n                        }\n                    ],\n                    [\n                        40,\n                        {\n                            \"fee_paying_account\":\"1.2.19\",\n                            \"owner\":\"1.2.19\",\n                            \"asset_id\":\"COCOS\",\n                            \"world_view\":\"GNK\",\n                            \"base_describe\":\"{\"name\":\"hahah\"}\"\n                        }\n                    ]\n                ],\n                \"extensions\":[\n\n                ],\n                \"signatures\":[\n                    \"1f1f715903b6cc5e3de8fcc898c22f2306af49cba7de52a951ddb459f9ac943c8f09218ea9dbbba4a7f9d22404ba827c12de352b20e600394635058ecc77a19b51\"\n                ]\n            }\n        ]\n    ],\n    \"id\":227\n}",
      "language": "json"
    }
  ]
}
[/block]
**12．NHアセットを削除します**

**例** 
[block:code]
{
  "codes": [
    {
      "code": "{\n    \"method\":\"call\",\n    \"params\":[\n        3,\n        \"broadcast_transaction_with_callback\",\n        [\n            240,\n            {\n                \"ref_block_num\":36879,\n                \"ref_block_prefix\":513082099,\n                \"expiration\":\"2019-10-14T03:57:03\",\n                \"operations\":[\n                    [\n                        41,\n                        {\n                            \"fee_paying_account\":\"1.2.19\",\n                            \"nh_asset\":\"4.2.0\"\n                        }\n                    ]\n                ],\n                \"extensions\":[\n\n                ],\n                \"signatures\":[\n                    \"1f4334ace92bdeb744113dd827849c81a1e9918d4472774e298acb4896d7face896fdc32db8c144429fc8cc144794163767f346ad1cbc03a677423bda6d576c610\"\n                ]\n            }\n        ]\n    ],\n    \"id\":240\n}",
      "language": "json"
    }
  ]
}
[/block]
**13．NHアセットを移転します**

**例** 
[block:code]
{
  "codes": [
    {
      "code": "{\n    \"method\":\"call\",\n    \"params\":[\n        3,\n        \"broadcast_transaction_with_callback\",\n        [\n            251,\n            {\n                \"ref_block_num\":36900,\n                \"ref_block_prefix\":2662692825,\n                \"expiration\":\"2019-10-14T03:57:45\",\n                \"operations\":[\n                    [\n                        42,\n                        {\n                            \"from\":\"1.2.19\",\n                            \"to\":\"1.2.20\",\n                            \"nh_asset\":\"4.2.1\"\n                        }\n                    ]\n                ],\n                \"extensions\":[\n\n                ],\n                \"signatures\":[\n                    \"2043d2ed8e23174628d73036297be2874010ac7c6ddee2adf50f5baf665ff4fd4d3eab5ce885453d2a6e533d5bcc5ec6be6c4d1e8261468d55387ee5f5b9fb6f77\"\n                ]\n            }\n        ]\n    ],\n    \"id\":251\n}",
      "language": "json"
    }
  ]
}
[/block]
**14．NHアセットオーダーを作成します**

**例** 
[block:code]
{
  "codes": [
    {
      "code": "{\n    \"method\":\"call\",\n    \"params\":[\n        3,\n        \"broadcast_transaction_with_callback\",\n        [\n            274,\n            {\n                \"ref_block_num\":36944,\n                \"ref_block_prefix\":1093032956,\n                \"expiration\":\"2019-10-14T03:59:13\",\n                \"operations\":[\n                    [\n                        43,\n                        {\n                            \"seller\":\"1.2.19\",\n                            \"otcaccount\":\"1.2.20\",\n                            \"pending_orders_fee\":{\n                                \"amount\":\"0\",\n                                \"asset_id\":\"1.3.0\"\n                            },\n                            \"nh_asset\":\"4.2.2\",\n                            \"memo\":\"NHアセットをpending orderに \",\n                            \"price\":{\n                                \"amount\":\"200000\",\n                                \"asset_id\":\"1.3.0\"\n                            },\n                            \"expiration\":\"2019-10-14T04:58:57\"\n                        }\n                    ]\n                ],\n                \"extensions\":[\n\n                ],\n                \"signatures\":[\n                    \"2076f7f91700c92201e6fd2c382d3ce3ef7ec50afb858f4d3749020010928edbe66c585dec666b763686dcf7a6549c5ba68f9eb20132812f2b417b313e8dc61977\"\n                ]\n            }\n        ]\n    ],\n    \"id\":274\n}",
      "language": "json"
    }
  ]
}
[/block]
**15．NHアセットオーダーを購入します**

**例** 
[block:code]
{
  "codes": [
    {
      "code": "{\n    \"method\":\"call\",\n    \"params\":[\n        3,\n        \"broadcast_transaction_with_callback\",\n        [\n            290,\n            {\n                \"ref_block_num\":36982,\n                \"ref_block_prefix\":977787249,\n                \"expiration\":\"2019-10-14T04:00:35\",\n                \"operations\":[\n                    [\n                        45,\n                        {\n                            \"order\":\"4.3.1\",\n                            \"fee_paying_account\":\"1.2.19\",\n                            \"seller\":\"1.2.19\",\n                            \"nh_asset\":\"4.2.2\",\n                            \"price_amount\":\"2\",\n                            \"price_asset_id\":\"1.3.0\",\n                            \"price_asset_symbol\":\"COCOS\",\n                            \"extensions\":[\n\n                            ]\n                        }\n                    ]\n                ],\n                \"extensions\":[\n\n                ],\n                \"signatures\":[\n                    \"1f4c3bc2c3548efa96abbd1990b236cc27d2abdd24431353d1ef4c33192901147467e6124d547fc51c4aedd3b74b923d8722db7b9e7e49459a05edcae7c91318ff\"\n                ]\n            }\n        ]\n    ],\n    \"id\":290\n}",
      "language": "json"
    }
  ]
}
[/block]
**16．NHアセットオーダーをキャンセルします**

**例** 
[block:code]
{
  "codes": [
    {
      "code": "{\n    \"id\":11,\n    \"method\":\"call\",\n    \"params\":[\n        4,\n        \"broadcast_transaction\",\n        [\n            {\n                \"signatures\":[\n                    \"1b1a84246c6360719f4411cfeeb678a686e489982f82d1e797ad60060e618a6e30376a67bd56eba98d36ac8c410a94406b7bb1b49ac1d9580449a376ef7d712dd4\"\n                ],\n                \"expiration\":\"2019-10-14T06:09:56\",\n                \"extensions\":[\n\n                ],\n                \"operations\":[\n                    [\n                        44,\n                        {\n                            \"extensions\":[\n\n                            ],\n                            \"fee_paying_account\":\"1.2.19\",\n                            \"order\":\"4.3.5\"\n                        }\n                    ]\n                ],\n                \"ref_block_num\":40844,\n                \"ref_block_prefix\":2763196414\n            }\n        ]\n    ]\n}",
      "language": "json"
    }
  ]
}
[/block]
**17．GASまたはブロック生成インセンティブを受け取ります**

**例** 
[block:code]
{
  "codes": [
    {
      "code": "{\n    \"method\":\"call\",\n    \"params\":[\n        3,\n        \"broadcast_transaction_with_callback\",\n        [\n            626,\n            {\n                \"ref_block_num\":40661,\n                \"ref_block_prefix\":1759545378,\n                \"expiration\":\"2019-10-14T06:03:37\",\n                \"operations\":[\n                    [\n                        27,\n                        {\n                            \"vesting_balance\":\"1.13.11\",\n                            \"owner\":\"1.2.19\",\n                            \"amount\":{\n                                \"amount\":\"9622\",\n                                \"asset_id\":\"1.3.1\"\n                            }\n                        }\n                    ]\n                ],\n                \"extensions\":[\n\n                ],\n                \"signatures\":[\n                    \"2039e91f96c54d042258ff1711465a9954f1fa0daba941c9c07462f0dadc1a8ef17c02544b1fd069843ac98db59a9ff7072b1e8353de79b9a6f1856e11a73dfdf2\"\n                ]\n            }\n        ]\n    ],\n    \"id\":626\n}",
      "language": "json"
    }
  ]
}
[/block]