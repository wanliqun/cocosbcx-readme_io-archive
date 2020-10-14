---
title: "5.5 コントラクトAPI"
slug: "55-コントラクトapi"
hidden: false
createdAt: "2019-09-17T09:26:17.051Z"
updatedAt: "2019-09-17T09:51:13.394Z"
---
[block:api-header]
{
  "title": "1．マニュアル"
}
[/block]
Cocos-BCXのスマートコントラクトはLUA言語を使用し、シンタックスをそのまま残す上、オフィシャル5.3のバージョンを修正しました。そして、ブロックチェーンの実行環境に応じて、オンチェーンでの操作関数を追加し、関数のデータベースを調整しました。

**1.1　基本概念**

コントラクトデータ
コントラクトのデータはユーザーデータゾーンとパブリックデータゾーンに分けられます
◆ユーザーデータゾーン：ユーザーがコントラクトのコールで発生したデータを保存します。コントラクトの作成者によって定義します。
◆パブリックデータゾーン：コントラクトルールなどのデータを保存します。owner関数をアサーションし、コントラクトのコール権限を設定できます。Public_dataリストにも記録されるため、パブリックデータをpublic_dataオブジェクトに書き込むようにしてください。

特殊オブジェクト
◆public_data
パブリックデータを保存するゾーンです。オブジェクト属性はコントラクトの作成によって定義します； 
◆private_data
ユーザーデータゾーンであり、コントラクトのコールした者と対応します
◆read_list：コントラクトデータIOのreadリストです。read_listの編集によって、ロードするコンテキストをコントラクトへ通知します。デフォルト設定：read_list={public_data={},private_data={}}、public_data、private_dataゾーンのデータを全部自動的にロードします；
read_list={public_data={test=true}}、public_data.testのデータだけを読み込み、read_chain関数を執行する時機能します；
◆write_list
コントラクトデータIOのwriteリストです。write_listの編集によって、オンチェーンで記録するコンテキストをコントラクトへ通知します。デフォルト設定：read_list={public_data={},private_data={}}、public_data、private_dataゾーンのデータを全部自動的に記録します；
write_list={public_data={test=true}}、public_data.testのデータだけを書き込み、write_chain関数を執行する時機能します。write_listのパス値（true/false）：true：存在する場合アップデートを行い、存在しない場合作成します、falseは：存在する場合削除します；
◆contract_base_info
コントラクトの基本情報を保存します。コントラクト内で修正されてもオブジェクトを記録しません。オブジェクト属性：name（コントラクトの名前）、id（コントラクトのid）、owner（コントラクトの所有者id）、caller（現在コールする者のid）、creation_date（コントラクトの作成時刻）、caontract_authority（コントラクトが授権署名を要求します）；

**1.2　備考**

コントラクトセッションの復元メカニズムは実行時コードの復元を含んでいません
即ち：lambda式はtableとmetatableのダイナミックな関数を含み、現在関数のコンテキストだけで有効です；
コントラクトアプリケーションレイヤーtableデータ構造を統一し、metatableを無効にします
理由：
◆lambda関数はよくmetatableで使われますが、実行時にコードが復元できません；
◆tableと比べて、metatableデータのIO速度が遅い

[block:api-header]
{
  "title": "2．基本モジュールと拡張"
}
[/block]
**2.1基本モジュール**

0号コントラクトによって、コントラクトのサンドボックスが基本モジュールへのサポートをコントロールします。後期に至って、0号コントラクトは理事会によって管理されます
2.2基本モジュールへの拡張
2.2.1　CJSONモジュール
CJSONモジュールはよく受け入れた関数構造化パラメーターの解析に用いられます。
現在コントラクトABIは既に外部tableデータ構造パラメーターを受け入れることができます。Cjsonモジュールを保留したのは文字列でオブジェクト及びオブジェクトの直列化（シリアライズ）をインポートするためです。
コール：
[block:code]
{
  "codes": [
    {
      "code": "cjson.function_name(*)",
      "language": "lua"
    }
  ]
}
[/block]

[block:code]
{
  "codes": [
    {
      "code": "table decode(string jsonstr)",
      "language": "lua"
    }
  ]
}
[/block]

[block:code]
{
  "codes": [
    {
      "code": "string encode(table tal)",
      "language": "lua"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "3．コントラクトとチェーンのインタラクションモジュール――スタティック関数"
}
[/block]
チェーンシステムとのインタラクションモジュールのスタティック関数は関数名でそのままコールできます
get_account_contract_data

プロトタイプ

[block:code]
{
  "codes": [
    {
      "code": "table get_account_contract_data(string name_or_id,table private_data_register_list)",
      "language": "lua"
    }
  ]
}
[/block]
説明
指定アカウントと対応するパスのユーザーデータを読み取ります
リターン値
table構造のユーザーデータをリターンします。パス内で指定したデータがない場合、対応するtable branchが空になります；
例
nico_data=get_account_contract_data('nicotest',{nicodata0={nicodata1=true})
nicotestアカウントが本コントラクト内でのnicodata0.nicodata1データを読み込みます。もしnicotestはコールするものである場合、nico_dataはprivate_data.nicodata0.nicodata1と同じになります。
[block:api-header]
{
  "title": "4．コントラクトとチェーンのインタラクションモジュール――ダイナミック関数"
}
[/block]
チェーンシステムとのインタラクションモジュールのダイナミック関数は“chainhelper:関数名（パラメーター......）”でコールします。

**4.1　hash256**
プロトタイプ


[block:code]
{
  "codes": [
    {
      "code": "string hash256(string source)",
      "language": "lua"
    }
  ]
}
[/block]
リターン値
hash256文字列をリターンします
パラメーター
source：
計算されるソースデータ

**4.2　hash512**
プロトタイプ
[block:code]
{
  "codes": [
    {
      "code": "string hash512(string source)",
      "language": "lua"
    }
  ]
}
[/block]
リターン値
hash512文字列をリターンします
パラメーター
source：計算されるソースデータ

**4.3　create_nh_asset**
プロトタイプ
[block:code]
{
  "codes": [
    {
      "code": "void create_nh_asset(string owner_id_or_name, string symbol, string world_view, string base_describe, bool enable_logger)",
      "language": "lua"
    }
  ]
}
[/block]
説明
NHアイテムを作成するには、コントラクト所有者は作成権限を持たなければなりません
パラメーター
name_or_id：新アイテムの所有者
symbol：流通限定の代替可能なアセットシンボル（例：COCOS）
world_view：世界観
base_describe：基本説明
enable_logger：contract resultで関連する影響を記録するかどうかを識別します

**4.4 ajust_lock_asset**
プロトタイプ
[block:code]
{
  "codes": [
    {
      "code": "void adjust_lock_asset(string symbol_or_id, int64_t amount)",
      "language": "lua"
    }
  ]
}
[/block]
説明
コントラクト所有者が本コントラクト内でロックしたアセットを調整します
パラメーター
symbol_or_id：調整するアセットIDまたはシンボル
amount：精度付きの値は負に設置することでき（ロックするアセット量を下げる）、調整した量は0から所有アセットの上限の間になります

**4.5　read_chain**
プロトタイプ
[block:code]
{
  "codes": [
    {
      "code": "void read_chain()",
      "language": "lua"
    }
  ]
}
[/block]
説明
コントラクトデータIO操作のreadであり、read_listと対応します

**4.6　write_chain**
プロトタイプ
[block:code]
{
  "codes": [
    {
      "code": "void write_chain()",
      "language": "lua"
    }
  ]
}
[/block]
説明
コントラクトデータIO操作のwriteであり、write_listと対応します

**4.7　get_accout_balance**
プロトタイプ
[block:code]
{
  "codes": [
    {
      "code": "int get_account_balance(string account_name_or_id,string asset_symbol_or_id)",
      "language": "lua"
    }
  ]
}
[/block]
説明
指定アカウント内の代替可能なアセットの残高を照会します
リターン値
残高の数値
パラメーター
account_name_or_id：照会するアカウント名またはid
asset_symbol_or_id：照会するアセットシンボルまたはid

**4.8　transfer_from_caller**
プロトタイプ
[block:code]
{
  "codes": [
    {
      "code": "void transfer_from_caller(string to, uint token, string symbol,bool enable_logger)",
      "language": "lua"
    }
  ]
}
[/block]
説明
コントラクトのコール者からアセットをアカウントに（to）移転します。金額はtoken、シンボルはsymbol
パラメーター
to：受け手アカウントid
token：金額、数値は0からlua numberの上限の間
symbol：アセットシンボル
enable_logger：contract resultで関連する影響を記録するかどうかを識別します

**4.9　transfer_from_owner**
プロトタイプ
[block:code]
{
  "codes": [
    {
      "code": "void transfer_from_owner(string to, uint token, string symbol,bool enable_logger)",
      "language": "lua"
    }
  ]
}
[/block]
説明
コントラクトのコール者からアセットをアカウントに（to）移転します。金額はtoken、シンボルはsymbol
パラメーター
to：受け手アカウントid
token：金額、数値は0からlua numberの上限の間
symbol：アセットシンボル
enable_logger：contract resultで関連する影響を記録するかどうかを識別します

**4.10　make_memo**
プロトタイプ
[block:code]
{
  "codes": [
    {
      "code": "void make_memo (string to, string key, string value,bool enable_logger)",
      "language": "lua"
    }
  ]
}
[/block]
説明
データ構造を暗号化する関数
パラメーター
to：指定されたメッセージを復号するアカウントid
key：ECC共有鍵（shared key）が提供したパスワードシード
value：暗号化内容
enable_logger：contract resultで関連する影響を記録するかどうかを識別します

**4.11　transfer_nht_from_caller**
プロトタイプ
[block:code]
{
  "codes": [
    {
      "code": "void transfer_nht_from_caller(string to, string token_hash_or_id,bool enable_logger)",
      "language": "lua"
    }
  ]
}
[/block]
説明
コントラクトのコール者からNHTをアカウントに（to）移転します
パラメーター
to：受け手アカウントid
token_hash_or_id：指定したNFTのhash値またはid番号
enable_logger：contract resultで関連する影響を記録するかどうかを識別します

**4.12　transfer_nht_from_owner**
プロトタイプ
[block:code]
{
  "codes": [
    {
      "code": "void transfer_nht_from_owner(string to, string token_hash_or_id,bool enable_logger)",
      "language": "lua"
    }
  ]
}
[/block]
説明
コントラクト所有者からNFTをアカウントに（to）移転します
パラメーター
to：受け手アカウントid
token_hash_or_id：指定したNFTのhash値またはid番号
enable_logger：contract resultで関連する影響を記録するかどうかを識別します

**4.13　change_nht_active_by_owner**
プロトタイプ
[block:code]
{
  "codes": [
    {
      "code": "void change_nht_active_by_owner (string beneficiary_account, string token_hash_or_id, bool enable_logger)",
      "language": "lua"
    }
  ]
}
[/block]
説明
NFTに使用権限を変更するには、コントラクト所有者は指定NFTの代理（proxy）権限または所有権と使用権両方を持たなければなりません
パラメーター
beneficiary_account：NFTの使用権をアサインされるアカウント名またはid
token_hash_or_id：指定したNFTのhashまたはid
enable_logger：contract resultで関連する影響を記録するかどうかを識別します

**4.14　transfer_nht_active_from_caller**
プロトタイプ
[block:code]
{
  "codes": [
    {
      "code": "void transfer_nht_active_from_caller( string to, string token_hash_or_id, bool enable_logger)",
      "language": "lua"
    }
  ]
}
[/block]
説明
コントラクトのコール者からNFTの使用権を移転するには、コール者は指定したNFTの代理権限または所有権と使用権両方を持たなければなりません
パラメーター
to：指定したNFTの使用権をアサインされるアカウント名またはid
token_hash_or_id：指定したNFTのhashまたはid
enable_logger：contract resultで関連する影響を記録するかどうかを識別します

**4.15　transfer_nht_authority_from_owner**
プロトタイプ
[block:code]
{
  "codes": [
    {
      "code": "void transfer_nht_authority_from_owner(string to, string token_hash_or_id, bool enable_logger)",
      "language": "lua"
    }
  ]
}
[/block]
説明
コントラクト所有者からNFTの代理管理権を移転するには、所有者はしてしたNFTの代理権限を持たなければなりません
パラメーター
to：NFTの代理管理権をアサインされるアカウント名またはid
token_hash_or_id：指定したNFTのhashまたはid
enable_logger：contract resultで関連する影響を記録するかどうかを識別します

**4.16　transfer_nht_authority_from_caller**
プロトタイプ
[block:code]
{
  "codes": [
    {
      "code": "void transfer_nht_authority_from_caller( string to, string token_hash_or_id, bool enable_logger)",
      "language": "lua"
    }
  ]
}
[/block]
説明
コントラクト所有者からNFTの代理管理権を移転するには、コール者は指定したNFTの代理権限を持たなければなりません
パラメーター
to：指定したNFTの代理管理権をアサインされるアカウント名またはid
token_hash_or_id：指定したNFTのhashまたはid
enable_logger：contract resultで関連する影響を記録するかどうかを識別します

**4.17　set_nht_limit_list**
プロトタイプ
[block:code]
{
  "codes": [
    {
      "code": "void set_nht_limit_list( string token_hash_or_id, string contract_name_or_ids, bool limit_type, bool enable_logger)",
      "language": "lua"
    }
  ]
}
[/block]
説明
指定アイテムの指定拡張ゾーン（コントラクトのデータゾーン）のread/write権限を設定するには、コール者は指定したNFTの所有権と使用権両方を持たなければなりません
パラメーター
token_hash_or_id：指定したNFTのhashまたはid
contract_name_or_ids：いつくかのデータゾーン（コントラクト）、“,”で区切りします
limit_type：trueの場合はホワイトリストになり、指定データゾーンへのwriteが可能です；falseの場合はブラックリストになり、write操作ができません
enable_logger：contract resultで関連する影響を記録するかどうかを識別します

**4.18　relate_nh_asset**
プロトタイプ
[block:code]
{
  "codes": [
    {
      "code": "void relate_nh_asset(string parent_token_hash_or_id, string child_token_hash_or_id, bool relate, bool enable_logger)",
      "language": "lua"
    }
  ]
}
[/block]
説明
二つのNFTをリンクします
パラメーター
parent_token_hash_or_id：指定した親（parent）NHTのhashまたはid
child_token_hash_id：指定した子（child）NFTのhashまたはid
relate：リンクします
enable_logger：contract resultで関連する影響を記録するかどうかを識別します

**4.19　random**
プロトタイプ
[block:code]
{
  "codes": [
    {
      "code": "int random()",
      "language": "lua"
    }
  ]
}
[/block]
説明
内部ランダム数を生成します
リターン値
ランダム数の結果

**4.20　is_owner**
プロトタイプ
[block:code]
{
  "codes": [
    {
      "code": "bool is_owner()",
      "language": "lua"
    }
  ]
}
[/block]
説明
コントラクトをコールした者がownerであるかを判定し、コントラクトのアサーションに使用できます
リターン値
判定結果

**4.21　nht_describe_change**
プロトタイプ
[block:code]
{
  "codes": [
    {
      "code": "void nht_describe_change(string nht_hash_or_id, string key, string value,bool enable_logger)",
      "language": "lua"
    }
  ]
}
[/block]
説明
NFTのゾーンデータ記述を修正します。ただし、コントラクトと対応するゾーンのみ修正できます
パラメーター
token_hash_or_id：指定したNFTのhash値またはid番号
key：ゾーンデータのキー名
value：ゾーンデータキーに対応する値
enable_logger：contract resultで関連する影響を記録するかどうかを識別します

**4.22　set_permission_flag**
プロトタイプ
[block:code]
{
  "codes": [
    {
      "code": "void set_permissions_flag(bool flag)",
      "language": "lua"
    }
  ]
}
[/block]
説明
コントラクト権限を検証するidを設定し、コントラクト署名要求を有効/無効にします。対応する信頼できる実行環境（TEE）のみ権限を持っていて、ユーザーはTEEでコントラクトをコールするとき、ユーザー署名とコントラクト署名が同時完了します。
パラメーター
flag：署名要求を有効にします

**4.23　change_contract_authority**
プロトタイプ
[block:code]
{
  "codes": [
    {
      "code": "void change_contract_authority(string publickey)",
      "language": "lua"
    }
  ]
}
[/block]
説明
コントラクト検証の権限を修正します
パラメーター
publickey：検証権限と対応する公開鍵
[block:api-header]
{
  "title": "5．スマートコントラクトの機能例"
}
[/block]
**5.1　Hello World（ログのアウトプット）** 
[block:code]
{
  "codes": [
    {
      "code": "function logtest()\n    chainhelper:log('hello world')\n    chainhelper:log(date('%Y-%m-%dT%H:%M:%S', chainhelper:time()))\nend",
      "language": "lua"
    }
  ]
}
[/block]
5.2　オンチェーン時間の入手
[block:code]
{
  "codes": [
    {
      "code": "function timetest() \n    public_data.time=date('%Y-%m-%dT%H:%M:%S', chainhelper:time()) \n    write_list={public_data={time=true}} \n    chainhelper:write_chain() \nend",
      "language": "lua"
    }
  ]
}
[/block]
**5.3　トランザクション** 
[block:code]
{
  "codes": [
    {
      "code": "function transfer(amount,symbol,islog) \n    chainhelper:transfer_from_caller(contract_base_info.owner,amount,symbol,islog) –コントラクト所有者から代替可能なアセットをアカウントに移転します\n    chainhelper:transfer_from_owner(contract_base_info.caller,amount,symbol,islog) –コントラクトのコール者から代替可能なアセットをアカウントに移転します\nend",
      "language": "lua"
    }
  ]
}
[/block]
**5.4　アセットロックの設置** 
[block:code]
{
  "codes": [
    {
      "code": "function init()\n    assert(chainhelper:is_owner(),'chainhelper:is_owner()')\n    read_list={public_data={is_init=true}}\n    chainhelper:read_chain()\n    assert(public_data.is_init==nil,'public_data.is_init==nil')\n    public_data.locked=0\n    public_data.is_init=true\n    chainhelper:write_chain()\nend\n\nfunction pay_with_lock(amount,symbol)\n    assert(amount>0,'amount > 0')\n    read_list={public_data={}}\n    chainhelper:read_chain()\n    assert(public_data.locked+amount>public_data.locked,'public_data.locked+amount>public_data.locked')\n    public_data.locked=public_data.locked+amount;  --[[ロック履歴を調整]] \n    assert(public_data.locked<=chainhelper:number_max(),'public_data.locked<=chainhelper:number_max()')\n    chainhelper:transfer_from_caller(contract_base_info.owner,amount,symbol,true)\n--[[トークンを転送in]]\n    chainhelper:adjust_lock_asset(symbol,amount)  --[[トークンをロック]]\n    write_list=read_list\n    chainhelper:write_chain()\nend    \n\nfunction adjustment_lock_and_transfer(to,amount,symbol)\n    assert(chainhelper:is_owner(),'chainhelper:is_owner()')\n    read_list={public_data={}}\n    chainhelper:read_chain()\n    assert(amount > 0 and public_data.locked – amount >= 0, 'amount>0 and public_data.locked-amount>=0')\n    public_data.locked=public_data.locked-amount  --[[ロック履歴を調整]]\n    chainhelper:adjust_lock_asset(symbol,-amount)      --[[トークンをアンロック]]\n    if(to~=contract_base_info.owner)then\n        chainhelper:transfer_from_owner(to,amount,symbol,true)  --[[トークンを転送out]]\n    end\n    write_list=read_list\n    chainhelper:write_chain()\nend",
      "language": "lua"
    }
  ]
}
[/block]
**5.5　Hashの生成/検証** 
[block:code]
{
  "codes": [
    {
      "code": "function set_hash(source) \n    public_data.hash256=chainhelper:hash256(source) \n    public_data.hash512=chainhelper:hash512(source) \n    chainhelper:write_chain() –デフォルト：write_list={public_data={},private_data={}} ,すべてのデータを更新します。本コントラクトはhash256とhash512二つのデータを持っています \nend \nfunction check_hash(source) \n    chainhelper:read_chain() –デフォルト：read_list={public_data={},private_data={}} ,すべてのデータをロードします。本コントラクトはhash256とhash512二つのデータを持っています \n    assert(public_data.hash256==chainhelper:hash256(source),'hash256 check error') \n    assert(public_data.hash512==chainhelper:hash512(source),'hash512 check error') \nend",
      "language": "lua"
    }
  ]
}
[/block]
**5.6　NFTの記述データの修正** 
[block:code]
{
  "codes": [
    {
      "code": "--json文字列でNFT記述を修正する場合\nfunction my_nht_describe_change( nht_hash_or_id,values_json) \n    local values=cjson.decode(values_json) \n    for key,value in pairs(values)  do  \n        chainhelper:log('key:'..key..',value:'..value)   \n        chainhelper:nht_describe_change( nht_hash_or_id,key,value,true)  \n    end  \nend\n\n--luaテーブルでNFT記述を修正する場合\nfunction nht_change_with_table( nht_hash_or_id,values_table) \n    for key,value in pairs(values_table)  do  \n        chainhelper:log('key:'..key..',value:'..value)   \n        chainhelper:nht_describe_change( nht_hash_or_id,key,value,true)  \n    end  \nend",
      "language": "lua"
    }
  ]
}
[/block]
**5.7　ランダム関数** 
[block:code]
{
  "codes": [
    {
      "code": "--これは、10回ランダムな累積と出力結果の関数例です\nfunction sum_public_by_rand()\n    read_list={public_data={sum_rand_10=true}}\nchainhelper:read_chain()\n--is_owner関数をアサーションし、インターフェイスのコール権限を設定します\n    assert(chainhelper:is_owner(),'You`re not the contract`s owner')\n    local i=0\n    while(i<10)do\n        i=i+1\n        if(public_data.sum_rand_10==nil)then\n            public_data.sum_rand_10=0\n            public_data.sum_rand_10=public_data.sum_rand_10+chainhelper:random()%100\n--random()の後の％の値は、必要なランダム数の値の範囲です。ここでのランダム結果は0～99です\n        else\n            public_data.sum_rand_10=public_data.sum_rand_10+chainhelper:random()%100\n        end\n    end\n    write_list={public_data={sum_rand_10=true}}\n    chainhelper:write_chain()\n    chainhelper:log('date:'..date('%Y-%m-%dT%H:%M:%S', \tchainhelper:time())..',sum:'..public_data.sum_rand_10) end\nend",
      "language": "lua"
    }
  ]
}
[/block]
**5.8　くじ引きの例** 
[block:code]
{
  "codes": [
    {
      "code": "--賞金プールを設置\nfunction set_ticket(ticket)                \n  assert(chainhelper:is_owner(),'You`re not the contract`s owner')            \n  read_list={public_data={ticket_pool_1=true,ticket_pool_2=true}}  \n  chainhelper:read_chain()  \n  if(public_data.ticket_pool_1==nil)then  \n    public_data.ticket_pool_1={}  \n    public_data.ticket_pool_2={}  \n    if (public_data.ticket_pool_1[ticket]==nil) then            \n        public_data.ticket_pool_2[#public_data.ticket_pool_2+1]=ticket  \n        public_data.ticket_pool_1[ticket]=#public_data.ticket_pool_2  \n    end     \n  else\n    if (public_data.ticket_pool_1[ticket]==nil) then  \n        public_data.ticket_pool_2[#public_data.ticket_pool_2+1]=ticket  \n        public_data.ticket_pool_1[ticket]=#public_data.ticket_pool_2  \n    end     \n  end\n  assert(#public_data.ticket_pool_2<=12)\n  write_list={public_data={ticket_pool_1={[ticket]=true},ticket_pool_2={[#public_data.ticket_pool_2]=true}}}  \n  chainhelper:write_chain()  \n  end\n\n--くじを引きます\nfunction luck_draw(ticket,amount,asset)  \n  assert(amount>=1000000,'amount should not be less than 1000000')  \n  assert(asset=='COCOS','asset error')  \n  read_list={public_data={ticket_pool_1=true,ticket_pool_2=true}}  \n  chainhelper:read_chain()      \n  local total=chainhelper:get_account_balance(contract_base_info.owner,asset)      \n  assert((#public_data.ticket_pool_2)*amount<=total,'Current maximum compensation ratio:'..#public_data.ticket_pool_2..'The biggest bet at present:'..total/(#public_data.ticket_pool_2))  \n  chainhelper:transfer_from_caller(contract_base_info.owner,amount,asset,true)  \n  local index=chainhelper:random()%(#public_data.ticket_pool_2)+1      \n  local rate = chainhelper:random()%(#public_data.ticket_pool_2)+1\n  chainhelper:log('luck:'..public_data.ticket_pool_2[index]..',rate:'..rate)\n  if(public_data.ticket_pool_2[index]==ticket)then  \n    chainhelper:transfer_from_owner(contract_base_info.caller,rate*amount,asset,true)      \n  end\n end\n --賞金プールをリセットします\nfunction reset_ticket() \n    write_list_list={public_data={ticket_pool_1=false,ticket_pool_2=false}}\n    chainhelper:write_chain()\nend",
      "language": "lua"
    }
  ]
}
[/block]
**5.9　例1：賞金プールの設置** 
[block:code]
{
  "codes": [
    {
      "code": "assert(is_owner(),'You`re not the contract`s owner')\n    if(public_data.ticket_pool_1==nil)then\n        public_data.ticket_pool_1={}\n        public_data.ticket_pool_2={}\n        if (public_data.ticket_pool_1[ticket]==nil) then\n            public_data.ticket_pool_2[#public_data.ticket_pool_2+1]=ticket—備考：Lua 配列のサブスクリプトは1からです\n            public_data.ticket_pool_1[ticket]=#public_data.ticket_pool_2\n        end\n    else\n        if (public_data.ticket_pool_1[ticket]==nil) then\n            public_data.ticket_pool_2[#public_data.ticket_pool_2+1]=ticket\n            public_data.ticket_pool_1[ticket]=#public_data.ticket_pool_2\n        end\n    end\nend\nくじ引き、ticket：チケット、amount：トークンの数、asset：トークンの種類\n\nLua\n\n    assert(amount>=1000000,'amount should not be less than 1000000')\n    assert(asset=='COCOS','asset error')\nlocal total=get_account_balance(contract_base_info.owner,asset)\nassert((#public_data.ticket_pool_2)*amount<=total,'Current maximum compensation ratio:'..#public_data.ticket_pool_2..'The biggest bet at present:'..total/(#public_data.ticket_pool_2))\n    transfer_from_caller(contract_base_info.owner,amount,asset,true)\n    local index=random()%(#public_data.ticket_pool_2)+1  -- 備考：Lua 配列のサブスクリプトは1から\nlocal rate=0\n    if(public_data.ticket_pool_2[index]==ticket)then\n        while(true)do\nrate =random()%(#public_data.ticket_pool_2)\nif(rate*amount<=total) then\ntransfer_from_owner(contract_base_info.caller,rate*amount,asset,true)\nbreak\nend\nend\n    end\nlog('ticket:'..public_data.ticket_pool_2[index]..',rate:'..rate)\nend\n関数をランダムに累積し、オンチェーンでのランダムデータの検証に用いる（テスト用）\n\nLua\nfunction sum_public_by_rand()\nassert(is_owner(),'You`re not the contract`s owner')\n    local i=0\n    while(i<10)do\n        i=i+1\n        if(public_data.sum_rand_10==nil)then\n            public_data.sum_rand_10=0\n          public_data.sum_rand_10=public_data.sum_rand_10+random()%100\n        else\n            public_data.sum_rand_10=public_data.sum_rand_10+random()%100\n        end\n    end\nend",
      "language": "lua"
    }
  ]
}
[/block]
例2：NFTのコントラクトと関連する記述を修正します。修正できるのはコントラクトと対応するゾーンだけです
[block:code]
{
  "codes": [
    {
      "code": "function my_nht_describe_change( nht_hash_or_id,change_values_json)\nlocal change_values=cjson.decode(change_values_json)—備考：ここではcjsonモジュールを使用しています\nfor key,value in pairs(change_values) do—注意：lua tableのトラバースであり、ipairsとpairsを間違わないよう\nlog('key:'..key..',value:'..value)\nnht_describe_change( nht_hash_or_id,key,value,true)\nend\nend\n//nht_hash_or_id：NFTのhashまたはid\n//change_values_json：json型の指定修正内容であり、一括修正に用います\n\nコントラクト検証の権限を修正\nfunction my_change_contract_authority(publickey)\nassert(is_owner(),'You`re not the contract`s owner')\n    change_contract_authority(publickey)\nend\n--コントラクトの署名要求を有効/無効にする際、対応するTEEのみが権限を持つよう、コントラクト権限を検証するidを設置します\nfunction set_permissions_flag(flag)\n    assert(is_owner(),'You`re not the contract`s owner')\n    set_permissions_flag(flag)\nend\n-- データ構造を暗号化する関数\nfunction my_make_memo(to,key,value) make_memo(to,key,value,true) end",
      "language": "lua"
    }
  ]
}
[/block]
**5.6　互いにコントラクトをコールする**
一つのコントラクト内で別のコントラクトをコールします。例では、コントラクト2がコントラクト1をコールしました。

コントラクト１
コントラクト名：contract.test002
[block:code]
{
  "codes": [
    {
      "code": "function logtest()\n\tchainhelper:log('hello world')\n\tchainhelper:log(date('%Y-%m-%dT%H:%M:%S', chainhelper:time()))\nend\n\nfunction handsome_parem(num,amount)\n\tchainhelper:log('=======log starts=======');\n\tchainhelper:log('{\"num\": \"'..num..'\",\"amount\":\"'..amount..'\"}');\n\tchainhelper:log('=======log ends=======');\nend",
      "language": "lua"
    }
  ]
}
[/block]
コントラクト2
コントラクト名：contract.test003
[block:code]
{
  "codes": [
    {
      "code": "function raven_call_handsome_parem(num1,num2)\n    -- contract name: contract.test002\n    local temp=import_contract('contract.test002')\n    temp.chainhelper=chainhelper\n    chainhelper:log('{\"name\": \"raven\",\"num1\": \"'..num1..'\",\"num2\":\"'..num2..'\"}');\n    chainhelper:log('xxxxx call test002 handsome_parem begin xxxxx');\n    temp.handsome_parem(num1,num2);\n    chainhelper:log('xxxxx call test002 handsome_parem end xxxxx');\nend\n\nfunction raven_call_logtest()\n    -- contract name: contract.test002\n    local temp=import_contract('contract.test002')\n    temp.chainhelper=chainhelper\n    chainhelper:log('xxxxx call test002 logtest begin xxxxx');\n    --because method logtest() in contract 1 calls method date(), so need temp.date = date, if other is needed, same way\n    temp.date = date;\n    temp.logtest();\n    chainhelper:log('xxxxx call test002 logtest end xxxxx');\nend",
      "language": "text"
    }
  ]
}
[/block]
コール結果
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/0ad538d-5_1.png",
        "5_1.png",
        969,
        619,
        "#2e3339"
      ]
    }
  ]
}
[/block]