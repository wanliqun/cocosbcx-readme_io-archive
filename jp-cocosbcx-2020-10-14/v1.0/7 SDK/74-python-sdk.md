---
title: "7.5 Python-SDK"
slug: "74-python-sdk"
hidden: false
createdAt: "2019-09-18T05:49:41.369Z"
updatedAt: "2019-09-18T06:07:56.314Z"
---
[block:api-header]
{
  "title": "はじめに"
}
[/block]
Ubuntu 16.04 LTS(64 bit)で構築することを推奨します。デフォルトはpython 3.5。

**手動インストール：**
Python
cd python-grapheneEnhance
python3 setup.py install –user

**チェーンパラメーターを変更：**
Python
vi python-grapheneEnhance/grapheneEnhancebase/chains.py # ブロックチェーンのパラメーターを設定します
[block:code]
{
  "codes": [
    {
      "code": "known_chains = {\n\"xxxxxx\": {\n    \"chain_id\": \"xxxxxx\",\n    \"core_symbol\": \"xxxxxx\",\n    \"prefix\": \"xxxxxx\"} # chains.pyで書いたコード\n```\n\npython3 setup.py install --user #pythonライブラリをリロードします",
      "language": "python"
    }
  ]
}
[/block]
**python スクリプトを構築します：** 
[block:code]
{
  "codes": [
    {
      "code": "from grapheneEnhance.graphene import Graphene\nfrom grapheneEnhance.instance import set_shared_graphene_instance\nfrom grapheneEnhance.storage import configStorage as config\nfrom pprint import pprint\n\nnodeAddress = \"ws://127.0.0.1:8000\" # The RPC node to be connected\ngph = Graphene(node=nodeAddress, blocking=True) # Instantiated object\nset_shared_graphene_instance(gph) # Set gph as a shared global instance\n\nif gph.wallet.created() is False: # Create a local wallet database, if not, create a new wallet database\n    gph.newWallet(\"xxxxxx\")\ngph.wallet.unlock(\"xxxxxx\") # Unlock the wallet, if you need to interact with the wallet in subsequent operations, you need to unlock the wallet.\n\nconfig[\"default_prefix\"] = gph.rpc.chain_params[\"prefix\"] # Add default information to the wallet database\ngph.wallet.addPrivateKey(privateKey) # Add a private key to the wallet\nconfig[\"default_account\"] = yourname # Add default information to the wallet database",
      "language": "text"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "APIについて"
}
[/block]
**アカウント関連**
関数：creat_account
機能：アカウントを作成し、秘密鍵をウォレットにインポートします
パラメーター：
account_name：アカウント名、/^[a-z][a-z0-9.-]{4,63}$/、小文字アルファベット＋数字/小文字アルファベット/点/ハイフンから成って、長さは4～63です。
password：パスワード
備考：アカウントを作成できるのは終身会員だけです。
例：
[block:code]
{
  "codes": [
    {
      "code": "pprint(gph.create_account(\"test3\", \"password\"))",
      "language": "python"
    }
  ]
}
[/block]
関数：upgrate_account
機能：終身会員にアップグレードします。切り替え手数料はかかりますが、アップグレード後、子アカウントの作成ができます。
パラメーター：
account：アップグレードするアカウント名
例：
[block:code]
{
  "codes": [
    {
      "code": "pprint(gph.upgrade_account(\"test1\"))",
      "language": "python"
    }
  ]
}
[/block]
**アセット関連**
関数：transfer
機能：目標アカウントにトークンを振込します。
パラメーター：
to：受け手アカウント名
amount(int)：金額
asset：アセットIDまたはトークンシンボル
memo：メモ
account：送り手アカウント
例：
[block:code]
{
  "codes": [
    {
      "code": "pprint(gph.transfer(\"test2\",100, \"1.3.0\", \" \", \"test1\"))",
      "language": "python"
    }
  ]
}
[/block]
関数：asset_creat
機能：トークンを作成します
パラメーター：
symbol：トークンシンボル、^[.A-Z]+$
precision(int)：精度（小数点以下の桁数）
amount(int)：ベースアセット量（即ち作成するトークン、デフォルトは1）
asset：ベースアセットID
_amount(int)：見積アセット（即ちコアアセット、デフォルトは1）
_asset：見積アセット
common_options(dict)：ビットトークンの選択項目（任意項目）。デフォルトパラメーターでビットトークンを作成する際、{}をパス（pass）します。
is_prediction_market(bool)：予測市場であるかどうか（ビットトークンの場合のみ）
account：トークンの作成者
commen_optionsパラメーター例：

[block:code]
{
  "codes": [
    {
      "code": "common_options = {\n    \"max_supply\": 10000000000000, # 最大発行量\n    \"market_fee_percent\": 0, # 市場取引の手数料％、デフォルト\n    \"max_market_fee\": 0, # 市場取引の最大手数料、デフォルト\n    \"issuer_permissions\": 79, # 発行者がアップデート可能な権限、デフォルト\n    \"flags\": 0, # 現在の権限\n    \"core_exchange_rate\": {\"base\": {}, \"quote\": {}}, # コアアセットとの交換レート、ベースアセットと見積アセットに決められます\n    \"whitelist_authorities\": [], # ホワイトリストアカウント\n    \"blacklist_authorities\": [], # ブラックリストアカウント\n    \"whitelist_markets\": [], # ホワイトリストアセット\n    \"blacklist_markets\": [], # ブラックリストアセット\n    \"description\": '{\"main\":\"\",\"short_name\":\"\",\"market\":\"\"}', #描述\n    \"extension\": {}",
      "language": "python"
    }
  ]
}
[/block]
例：
[block:code]
{
  "codes": [
    {
      "code": "pprint(gph.asset_create(\"TESTS\", 5, 1, \"1.3.0\", 1, \"1.3.1\", common_options=common_options, bitasset_opts={}, account=\"test1\"))",
      "language": "python"
    }
  ]
}
[/block]
関数：asset_issue
機能：トークンを発行します
パラメーター：
amount(int)：発行量
asset：発行するアセットシンボル
issue_to_account：発行者
memo：メモ（任意項目）
account：トークンの作成者
例：
[block:code]
{
  "codes": [
    {
      "code": "pprint(gph.asset_issue(10000, \"TESTS\", \"test1\", account=\"test1\"))",
      "language": "python"
    }
  ]
}
[/block]
**NHアセット関連**
関数：register_nh_asset_creator
機能：現在操作中のアカウントを開発者として登録します
パラメーター：
account：登録者アカウント名
例：
[block:code]
{
  "codes": [
    {
      "code": "pprint(gph.register_nh_asset_creator(\"test2\"))",
      "language": "python"
    }
  ]
}
[/block]
関数：creat_world_view
機能：NHアセットに適用する世界観を作成し、チェーンシステムで現在操作中のアカウント（一般はゲームアカウント）に適用するNHアセット世界観を登録します。
パラメーター：
world_view：世界観名
account：作成者アカウント名
例：
[block:code]
{
  "codes": [
    {
      "code": "pprint(gph.create_world_view(\"DRBALL\", \"test1\"))",
      "language": "python"
    }
  ]
}
[/block]
関数：creat_nh_asset
機能：唯一性のあるNHアセットを作成します
パラメーター：
owner：指定NHアセットの所有者（NHアセットの帰属アカウント、デフォルトは作成者）
assetId：本NHアセットで取引する時に使用しるアセットID
world_view：世界観
describe：本NHアセットの描述、作成者に定義されます
account：作成者
例：
[block:code]
{
  "codes": [
    {
      "code": "pprint(gph.create_nh_asset(\"test2\", \"XXX\", \"FLY\", '{\"name\":\"tom\"}', \"test1\"))",
      "language": "python"
    }
  ]
}
[/block]
関数：creat_nh_asset_order
機能：NHアセットを売出します
パラメーター：
otcaccount：OTC取引所アカウント、pending orderの手数料を徴収します。
pending_order_fee_amount：pending orderの手数料、ユーザーがOTC取引プラットフォームに支払います
nh_asset：NHアセットID
memo：メモ
price_amount：注文が実行される価格
price：注文価格が使用したアセットシンボルまたはID
account：注文の作成者
例：
[block:code]
{
  "codes": [
    {
      "code": "pprint(gph.create_nh_asset_order(\"official-account\", 1, \"1.3.0\", \"4.2.1\", \" \", 100, \"1.3.0\", \"test1\"))",
      "language": "python"
    }
  ]
}
[/block]
**コントラクト関連**
関数：creat_contract
機能：スマートコントラクトを作成します
パラメーター：
name:コントラクト名、/^[a-z][a-z0-9.-]{4,63}$/、小文字アルファベット＋小文字アルファベット/数字/点/ハイフンから成っていて、長さは4～63です。
data：コントラクトLuaコード
con_authority：コントラクト権限（公開鍵と秘密鍵ペアのpublicKey）
account：コントラクトの作成者
例：
[block:code]
{
  "codes": [
    {
      "code": "print(gph.create_contract(\"contract.test01\", data=data, con_authority=\"COCOS6esv8d6u2eqzKyiQvCYJa6XK74c7BrmzUqL4Z7zfhtvB4dbLh4\", account=\"developer\"))",
      "language": "python"
    }
  ]
}
[/block]
関数：call_contract_function
機能：コントラクト関数インターフェイスをコールします
パラメーター：
contract：コントラクト名またはID
function：コントラクト内関数名
value_list(list)：コントラクト関数をコールするパラメーターリスト
account：コール者アカウント名
value_listパラメーター例：
[block:code]
{
  "codes": [
    {
      "code": "pprint(gph.call_contract_function(\"1.16.1\", \"draw\", value_list=value_list, account=\"test1\"))",
      "language": "python"
    }
  ]
}
[/block]
**市場関連**
関数：limit_order_create
機能：所与の市場で注文を作成します
パラメーター：
amount（int）：売り出すトークン量
asset：売り出すアセットIDまたはトークンシンボル
min_amount(int)：必要な取得するトークンの最小量
min_amount_asset：必要な取得するアセットIDまたｈトークンシンボル
fill(bool)：デフォルトはfalse。tureに設定すると、注文は実行/失敗されなければなりません
account：売出者アカウント名
例：
[block:code]
{
  "codes": [
    {
      "code": "pprint(gph.limit_order_create(1, \"1.3.0\", 1, \"1.3.1\", account=\"test1\"))",
      "language": "python"
    }
  ]
}
[/block]
関数：limit_order_cancel
機能：所与の市場で作成した指値注文をキャンセルします
パラメーター：
order_numbers(list)：キャンセルする指値注文ID
account：操作者アカウント名
例：
[block:code]
{
  "codes": [
    {
      "code": "pprint(gph.limit_order_cancel([\"1.7.1\"], account=\"test1\"))",
      "language": "python"
    }
  ]
}
[/block]
**証人関連**
関数：creat_witness
機能：証人候補者を作成します
パラメーター：
account_name：証人候補者アカウント
url：証人のウェブリンク
key：証人ブロックのサイン付き公開鍵
例：
[block:code]
{
  "codes": [
    {
      "code": "pprint(gph.create_witness(\"test2\", \"\", \"COCOS5YnQru8mtYo9HkckwnuPe8fUcE4LSxdCfVheqBj9fMMK5zwiHb\"))",
      "language": "python"
    }
  ]
}
[/block]
関数：approve_witness
機能：証人候補者に投票します
パラメーター：
witnesses(list)：証人アカウント名またはID
account：投票するアカウント名
例：
[block:code]
{
  "codes": [
    {
      "code": "pprint(gph.disapprove_worker([\"1.14.1\"], \"test1\"))",
      "language": "python"
    }
  ]
}
[/block]
**理事会関連**
関数：committee_member_create
機能：理事会候補者を作成します
パラメーター：
url：ウェブリンク
account	：理事会候補者アカウント
例：
[block:code]
{
  "codes": [
    {
      "code": "pprint(gph.committee_member_create(\" \", \"test2\"))",
      "language": "python"
    }
  ]
}
[/block]
関数：committee_member_update
機能：理事会候補者情報をアップデートします
パラメーター：
new_url：新しいウェブリンク
account	：アップデートする理事会候補者アカウント
例：
[block:code]
{
  "codes": [
    {
      "code": "pprint(gph.committee_member_update(\" \", \"test2\"))",
      "language": "python"
    }
  ]
}
[/block]
**提議関連**
関数：relate_world_view
機能：世界観を関係付けます。関係付けしてから、初めてこの世界観に適用するNHアセットを作成できます。提議して、世界観の作成者が承認するというプロセスです。
パラメーター：
world_view：世界観名
account：関係付け者アカウント名
例：
[block:code]
{
  "codes": [
    {
      "code": "pprint(gph.relate_world_view(\"DRBALL\", \"test2\"))",
      "language": "python"
    }
  ]
}
[/block]
関数：approveproposal
機能：自分が作成した世界観と関係付ける提議を承認します
パラメーター：
proposal_ids(list)：提議ID
account：提議情報をアップデートするアカウント
例：
[block:code]
{
  "codes": [
    {
      "code": "pprint(gph.approveproposal([\"1.10.1\"], \"test1\"))",
      "language": "python"
    }
  ]
}
[/block]
**ウォレットAPIのコール例**
関数：unlock
機能：ウォレットをアンロックし、関連操作を行います。
パラメーター：
pwd：ウォレットパスワード
例：
[block:code]
{
  "codes": [
    {
      "code": "print(gph.wallet.unlock(pwd))",
      "language": "python"
    }
  ]
}
[/block]
関数：getAccounts
機能：ウォレットデータベースからアカウント情報を入手します
[block:code]
{
  "codes": [
    {
      "code": "print(gph.wallet.getAccounts())",
      "language": "python"
    }
  ]
}
[/block]
関数：getPrivateKeyForPublicKey
機能：もらった公開鍵で、ウォレットからペアの秘密鍵を入手します
パラメーター：
pub：公開鍵文字列
[block:code]
{
  "codes": [
    {
      "code": "print(gph.wallet.getPrivateKeyForPublicKey(pub))",
      "language": "python"
    }
  ]
}
[/block]
**RPCインターフェイスのコール例**
関数：get_object
機能：本objectのデータを入手します
パラメーター：
object_id：objectID
例：
[block:code]
{
  "codes": [
    {
      "code": "print(gph.rpc.get_object(\"1.2.18\")) # ID \"1.2.17\"のアカウント情報を入手します",
      "language": "python"
    }
  ]
}
[/block]
関数：get_contract
機能：コントラクト情報を入手します
パラメーター：
contract_id：コントラクト名またはID
例：
[block:code]
{
  "codes": [
    {
      "code": "print(gph.rpc.get_contract(\"1.16.0\")) # ID \"1.16.0\"のコントラクト情報を入手します",
      "language": "python"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Main-Packages"
}
[/block]
**grapheneEnhance**
説明：下記サブモジュールはチェーンシステム上すべてのクラスと一対一対応しています（例えば、アカウント、アセット、ブロック、提議、コントラクトなど）。クラスごとにコールできる関数があります。grapheneモジュールで、OPに関連するAPIがコールできます（例えば、振込、アカウント作成、アセット作成、コントラクト作成など）。
grapheneEnhance.account module
grapheneEnhance.aes module
grapheneEnhance.amount module
grapheneEnhance.asset module
grapheneEnhance.block module
grapheneEnhance.blockchain module
grapheneEnhance.committee module
grapheneEnhance.contract module
grapheneEnhance.dex module
grapheneEnhance.exceptions module
grapheneEnhance.extensions module
grapheneEnhance.graphene module
grapheneEnhance.instance module
grapheneEnhance.market module
grapheneEnhance.memo module
grapheneEnhance.notify module
grapheneEnhance.price module
grapheneEnhance.proposal module
grapheneEnhance.storage module
grapheneEnhance.transactionbuilder module
grapheneEnhance.utils module
grapheneEnhance.vesting module
grapheneEnhance.wallet module
grapheneEnhance.witness module
grapheneEnhance.worker module

grapheneEnhanacebase
説明：下記一部のモジュールはインフラデザインと関連しています（例えば、チェーンデータ、オブジェクト型、OP、データ構造など）。chainsモジュールを初期化する時以外、一般的には変更する必要がありません。
grapheneEnhancebase.account module

grapheneEnhancebase.asset_permissions module
grapheneEnhancebase.bip38 module
grapheneEnhancebase.chains module
grapheneEnhancebase.memo module
grapheneEnhancebase.objects module
grapheneEnhancebase.objecttypes module
grapheneEnhancebase.operationids module
grapheneEnhancebase.operations module
grapheneEnhancebase.signedtransactions module
grapheneEnhancebase.transactions module