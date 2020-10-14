---
title: "2.2 cli_wallet"
slug: "22-cli_wallet"
hidden: false
createdAt: "2019-09-17T04:20:17.895Z"
updatedAt: "2019-09-17T07:33:37.591Z"
---
ウォレットコマンドラインツールはブロックチェーンとのインタラクションができます。続いて、操作手順を説明します。
[block:api-header]
{
  "title": "2.2.1 ログイン"
}
[/block]
1．コマンドラインウォレットの実行ファイル：cli_walletを入手し、指定したディレクトリに保存します
Githubから複数バージョンのcli_walletを入手できます。アドレスはこちら。

2．ディレクトリを開き、以下コマンドを実行し、ログインしてください。
■コマンドフォーマット
--chain-id [チェーンID] -s [証人ノードRPCアドレス] -r [コマンドラインウォレットのRPCサーバーがリッスンするアドレス]
[block:code]
{
  "codes": [
    {
      "code": "./cli_wallet  --chain-id 90a45949c27a3de6f71d2cfb68e4a04a2fce9052f8192d405c581ba9b36d991b -s ws://127.0.0.1:8020  -r  127.0.0.1:8099",
      "language": "shell"
    }
  ]
}
[/block]
結果：
[block:code]
{
  "codes": [
    {
      "code": "Logging RPC to file: logs/rpc/rpc.log\n2125047ms th_a       main.cpp:131                  main                 ] key_to_wif( committee_private_key ): 5KCBDTcyDqzsqeh******c3saYSzbDZ5W \n2125062ms th_a       main.cpp:135                  main                 ] nico_pub_key: COCOS7yE9skpB******tXTz88HtbpQsZf \n2125063ms th_a       main.cpp:136                  main                 ] key_to_wif( nico_private_key ): 5KAUeN3Yv51******XTJK7euqc3NnaaLz1GJm \nStarting a new wallet with chain ID 90a45949c27a3de6f71d2cfb68e4a04a2fce9052f8192d405c581ba9b36d991b (from CLI)\n2125073ms th_a       main.cpp:183                  main                 ] wdata.ws_server: ws://127.0.0.1:8020 \n2125108ms th_a       main.cpp:188                  main                 ] wdata.ws_user:  wdata.ws_password:  \n\nPlease use the set_password method to initialize a new wallet before continuing\n2139294ms th_a       main.cpp:227                  main                 ] Listening for incoming RPC requests on 127.0.0.1:8099\nnew >>>",
      "language": "text"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "2.2.2 ロックとアンロック"
}
[/block]
1．初めてログインするとき、パスワードを設置する必要があります。
■コマンドフォーマット
　set_password[パスワード]
[block:code]
{
  "codes": [
    {
      "code": "set_password xxxx",
      "language": "shell"
    }
  ]
}
[/block]
結果：
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/12070fc-image002.jpg",
        "image002.jpg",
        851,
        85,
        "#050605"
      ]
    }
  ]
}
[/block]
2．パスワードの設置が完了したら、ウォレットをアンロックしてください。
■コマンドフォーマット
　unlock[パスワード]
[block:code]
{
  "codes": [
    {
      "code": "unlock xxxx",
      "language": "shell"
    }
  ]
}
[/block]
結果：
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/42b1e9d-image004.jpg",
        "image004.jpg",
        850,
        87,
        "#050605"
      ]
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "2.2.3 アカウントをウォレットへインポート"
}
[/block]
1．ウォレットへログイン、アンロックし、以下コマンドを実行してみてください。
■コマンドフォーマット
　import_key[ユーザー名][秘密鍵]
[block:code]
{
  "codes": [
    {
      "code": "import_key official-account 5KaVpJa9G4oqA5WHcSGitauFRuzdHcPVEAaESaA",
      "language": "shell"
    }
  ]
}
[/block]
結果：
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/62998c7-image006.jpg",
        "image006.jpg",
        850,
        168,
        "#0e0e0a"
      ]
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "2.2.4 アセットをウォレットへインポート"
}
[/block]
1．ウォレットへログイン、アンロックし、以下コマンドを実行してみてください。
■コマンドフォーマット
import_balance[ユーザー名][アセットアドレスに対応する秘密鍵][ブロードキャスト（true/false）]
 コンテキスト
作成したアセットはまだエクスポートされていない新しいチェーンの場合
[block:code]
{
  "codes": [
    {
      "code": "import_balance official-account [\"5KAUeN3Yv51FzpLGGf4S1ByKpMqVFNzXTJK7euqc3L\"] true",
      "language": "shell"
    }
  ]
}
[/block]
結果：
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/9126d3f-image008.jpg",
        "image008.jpg",
        850,
        148,
        "#0a0b09"
      ]
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "2.2.5 振込"
}
[/block]
■コマンドフォーマット
import_balance[送り手][受けて][金額]	[トークンタイプ][備考][ブロードキャスト（true/false）]
■条件
ウォレットがアンロックで、且つアカウント内アセットの残高が十分な場合
■例
transfer official-account test-account 100 COCOS "info" true
[block:code]
{
  "codes": [
    {
      "code": "transfer from to amount asset_symblo \"memo_info\" true",
      "language": "shell"
    }
  ]
}
[/block]
結果：
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/cc1acff-image010.png",
        "image010.png",
        850,
        654,
        "#060606"
      ]
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "2.2.6 新規登録"
}
[/block]
■コマンドフォーマット
register_account[ユーザー名][owner公開鍵][active公開鍵][登録するアカウント名][推薦者アカウント][ブロードキャスト（true/false）]
■条件
ウォレットがアンロックで、且つアカウント内アセットの残高が十分な場合
■例
register_account test-account XXX6esv8d6u2eqzKyiQvCYJa6XK74c7BrmzUqL4Z7zfhtvB4db XXX6esv8d6u2eqzKyiQvCYJa6XK74c7BrmzUqL4Z7zfhtvB4db official-account official-account 0 true
[block:code]
{
  "codes": [
    {
      "code": "register_account name owner_key active_key registrar_account referrer_account referrer_percent true",
      "language": "shell"
    }
  ]
}
[/block]
結果：
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/8253372-image012.jpg",
        "image012.jpg",
        850,
        1297,
        "#070707"
      ]
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "2.2.7 メンバーシップのアップグレード"
}
[/block]
■条件
　アカウント内アセットの残高が十分な場合
■コマンドフォーマット
　upgrade_account[ユーザー名][ブロードキャスト（true/false）]
■例
　upgrade_account test-account true
注：コマンドラインウォレットは終身メンバーシップのみにアップグレードができ、年次会員へのアップグレードができません。
[block:code]
{
  "codes": [
    {
      "code": "upgrade_account test-account true",
      "language": "shell"
    }
  ]
}
[/block]
結果：
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/7936f8e-image014.png",
        "image014.png",
        851,
        557,
        "#060606"
      ]
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "2.2.8 チェーンID、現在のアクティブな証人、理事会メンバーなど情報の獲得"
}
[/block]
■コマンドフォーマット
　info
[block:code]
{
  "codes": [
    {
      "code": "Info",
      "language": "shell"
    }
  ]
}
[/block]
結果：
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/a2a8758-image016.png",
        "image016.png",
        851,
        789,
        "#040404"
      ]
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "2.2.9 クライアント端末バージョン、コンパイル時間、boostバージョン、opensslバージョンなど情報のリターン"
}
[/block]
■コマンドフォーマット
　About
[block:code]
{
  "codes": [
    {
      "code": "about",
      "language": "shell"
    }
  ]
}
[/block]
結果：
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/17b50e0-image018.png",
        "image018.png",
        851,
        264,
        "#080808"
      ]
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "2.2.10 指定ブロック情報の獲得"
}
[/block]
■コマンドフォーマット
 get_block[ブロックの高さ]
■例
 get_block 10
[block:code]
{
  "codes": [
    {
      "code": "get_block block_num",
      "language": "shell"
    }
  ]
}
[/block]
結果：
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/e4a8d18-image020.png",
        "image020.png",
        850,
        264,
        "#0b0b0b"
      ]
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "2.2.11 オンチェーンで登録しているアカウント数の獲得"
}
[/block]
■コマンドフォーマット
　get_account_count
[block:code]
{
  "codes": [
    {
      "code": "get_account_count",
      "language": "shell"
    }
  ]
}
[/block]
結果：
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/d9be5bb-image022.png",
        "image022.png",
        851,
        63,
        "#050505"
      ]
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "2.2.12 ウォレットにインポートされたアカウントのリスティング"
}
[/block]
■コマンドフォーマット
　list_my_account
[block:code]
{
  "codes": [
    {
      "code": "list_my_account",
      "language": "shell"
    }
  ]
}
[/block]
結果：
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/cf961cf-image024.jpg",
        "image024.jpg",
        851,
        1202,
        "#060606"
      ]
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "2.2.13 アカウント内アセットの残高の表示"
}
[/block]
■コマンドフォーマット
　list_account_balances[アカウント名]
■例
　list_account_balances official-account
[block:code]
{
  "codes": [
    {
      "code": "list_account_balances official-account",
      "language": "shell"
    }
  ]
}
[/block]
結果：
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/e656768-image026.png",
        "image026.png",
        851,
        81,
        "#080808"
      ]
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "2.2.14 オンチェーンのトークンの表示"
}
[/block]
■コマンドフォーマット
　list_assets[lowerbound][limit]
■例
　list_assets″″1
説明：リターンの結果は、トークンシンボル順で並べます。 「lowerbound」パラメータは最小制限、「limit」はリターンの最大個数です。つまり、トークンシンボルが「lowerbound」以上のトークンを最大「limit」個をリターンします。
[block:code]
{
  "codes": [
    {
      "code": "list_assets lowerbound limit",
      "language": "shell"
    }
  ]
}
[/block]
結果：
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/d4451cf-image028.png",
        "image028.png",
        851,
        706,
        "#040404"
      ]
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "2.2.15 アカウント履歴の入手"
}
[/block]
■コマンドフォーマット
　get_account_history[アカウント名][limit]
■例
　get_account_history official-account 2
[block:code]
{
  "codes": [
    {
      "code": "get_account_history account limit",
      "language": "shell"
    }
  ]
}
[/block]
結果：
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/8cd3dcd-image030.png",
        "image030.png",
        850,
        131,
        "#0c0c0c"
      ]
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "2.2.16 手数料など静的な属性の入手"
}
[/block]
■コマンドフォーマット
　get_global_properties
[block:code]
{
  "codes": [
    {
      "code": "get_global_properties",
      "language": "shell"
    }
  ]
}
[/block]
結果：
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/af7f168-image032.png",
        "image032.png",
        850,
        1008,
        "#020303"
      ],
      "caption": ""
    }
  ]
}
[/block]
注：表示結果が長いため、一部を抜粋して添付したものです。
[block:api-header]
{
  "title": "2.2.17 最新ブロックID、時間、次回メンテナンス時間など動的な属性の入手"
}
[/block]
■コマンドフォーマット
　get_dynamic_global_properties
[block:code]
{
  "codes": [
    {
      "code": "get_dynamic_global_properties",
      "language": "shell"
    }
  ]
}
[/block]
結果：
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/6281a62-image034.png",
        "image034.png",
        850,
        407,
        "#090909"
      ]
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "2.2.18 アカウント情報の入手"
}
[/block]
■コマンドフォーマット
　get_account[アカウント名またはID]
■例
　get_account official-account
[block:code]
{
  "codes": [
    {
      "code": "get_account_id account_name_or_id",
      "language": "shell"
    }
  ]
}
[/block]
結果：
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/0beed21-image036.jpg",
        "image036.jpg",
        850,
        1220,
        "#060606"
      ]
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "2.2.19 アセット情報の入手"
}
[/block]
■コマンドフォーマット
　get_asset[アセット名またはID]
■例
　get_asset COCOS
[block:code]
{
  "codes": [
    {
      "code": "get_asset asset_name_or_id",
      "language": "shell"
    }
  ]
}
[/block]
結果：
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/d778bcc-image038.png",
        "image038.png",
        851,
        691,
        "#040404"
      ]
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "2.2.20 アカウントIDの入手"
}
[/block]
■コマンドフォーマット
　get_account_id[アカウント名]
■例
　get_account_id official-account
[block:code]
{
  "codes": [
    {
      "code": "get_account_id account_name",
      "language": "shell"
    }
  ]
}
[/block]
結果：
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/45bfd60-image040.png",
        "image040.png",
        850,
        68,
        "#050505"
      ]
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "2.2.21 アセット情報の入手"
}
[/block]
■コマンドフォーマット
　get_asset[アカウント名]
■例
　get_asset COCOS
[block:code]
{
  "codes": [
    {
      "code": "get_asset asset_name",
      "language": "shell"
    }
  ]
}
[/block]
結果：
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/5c99dbd-image042.png",
        "image042.png",
        850,
        695,
        "#040404"
      ]
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "2.2.22 オブジェクトの入手"
}
[/block]
■コマンドフォーマット
　get_object[オブジェクトID]
■例
　get_object 1.2.6
[block:code]
{
  "codes": [
    {
      "code": "get_object object_id",
      "language": "shell"
    }
  ]
}
[/block]
結果：
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/15fc265-image044.png",
        "image044.png",
        837,
        1316,
        "#050505"
      ]
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "2.2.23 秘密鍵の入手"
}
[/block]
■コマンドフォーマット
　get_private_key[公開鍵]
■例
　get_private_key XXX6esv8d6u2eqzKyiQvCYJa6XK74c7BrmzUqL4Z3
注：秘密鍵がウォレットに保存された場合のみ照会できます。
[block:code]
{
  "codes": [
    {
      "code": "get_private_key public_key",
      "language": "shell"
    }
  ]
}
[/block]
結果：
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/9a881dc-image046.jpg",
        "image046.jpg",
        850,
        104,
        "#0f100f"
      ]
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "2.2.24 ウォレットのロック"
}
[/block]
■コマンドフォーマット
　lock
[block:code]
{
  "codes": [
    {
      "code": "lock",
      "language": "shell"
    }
  ]
}
[/block]
結果：
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/e446368-image048.png",
        "image048.png",
        851,
        68,
        "#020302"
      ]
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "2.2.25 セキュリティのあるBrainkey、公開鍵、秘密鍵のリターン"
}
[/block]
■コマンドフォーマット
　suggest_brain_key
[block:code]
{
  "codes": [
    {
      "code": "suggest_brain_key",
      "language": "shell"
    }
  ]
}
[/block]
結果：
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/911ecf3-image050.png",
        "image050.png",
        851,
        173,
        "#0d0e0d"
      ]
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "2.2.26 理事会へ入会"
}
[/block]
■コマンドフォーマット
　creat_committee_member[アカウント名][url][ブロードキャスト（true/false）]
■例
　creat_committee_member official-account"http//my-web"true
注：理事会へ入会したら、候補者になり、一定の投票を得てから初めて理事会メンバーになります。
[block:code]
{
  "codes": [
    {
      "code": "create_committee_member account \"url\" true",
      "language": "shell"
    }
  ]
}
[/block]
結果：
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/e936edd-image052.png",
        "image052.png",
        850,
        529,
        "#070707"
      ]
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "2.2.27 証人の申込"
}
[/block]
■コマンドフォーマット
　creat_witness[アカウント名][ur;][ブロードキャスト（true/false）]
■例
　creat_witness official-account″http//my-ewb″true
注：申し込んだ後、証人候補になり、一定の投票を得てから初めて証人になります。
[block:code]
{
  "codes": [
    {
      "code": "create_witness account \"url\" true",
      "language": "shell"
    }
  ]
}
[/block]
結果：
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/66c00d7-image054.png",
        "image054.png",
        851,
        572,
        "#070707"
      ]
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "2.2.28 証人のリスティング"
}
[/block]
■コマンドフォーマット
　list_witnesses[lowerbound][limit]
■例
　list_witness″″100
説明：アカウント名順でリスティングします。lowerboungは最小限であり、limitはリターンする最大個数です。
[block:code]
{
  "codes": [
    {
      "code": "list_witnesses lowerbound limit",
      "language": "shell"
    }
  ]
}
[/block]
結果：
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/7cf453d-image056.png",
        "image056.png",
        850,
        214,
        "#030303"
      ]
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "2.2.29 理事会メンバーのリスティング"
}
[/block]
■コマンドフォーマット
　list_committee_members[lowerbound][limit]
■例
　list_committee_members″″100
説明：理事会メンバーのアカウント名順でリスティングします。lowerboundは最小限であり、limitはリターンする最大個数です。
[block:code]
{
  "codes": [
    {
      "code": "list_committee_members lowerbound limit",
      "language": "shell"
    }
  ]
}
[/block]
結果：
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/ca7a6ff-image058.png",
        "image058.png",
        851,
        216,
        "#030303"
      ]
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "2.2.30 証人情報の入手"
}
[/block]
■コマンドフォーマット
　get_witness[証人名またはID]
■例
　get_witness Witness-0
[block:code]
{
  "codes": [
    {
      "code": "get_witness witness_name_or_id",
      "language": "shell"
    }
  ]
}
[/block]
結果：
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/9f4560a-image060.png",
        "image060.png",
        851,
        553,
        "#060706"
      ]
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "2.2.31 理事会メンバー情報の入手"
}
[/block]
■コマンドフォーマット
　get_committee_member[理事会メンバー名またはID]
■例
　get_committee_member Witness-0
[block:code]
{
  "codes": [
    {
      "code": "get_committee_member committee_member_name_or_id",
      "language": "shell"
    }
  ]
}
[/block]
結果：
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/32e699e-image062.png",
        "image062.png",
        851,
        191,
        "#060606"
      ]
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "2.2.32 コントラクトの作成"
}
[/block]
■コマンドフォーマット
　creat_contract[所有者][名前][権限（公開鍵秘密鍵ペアのpublicKey）][データ内容][ブロードキャスト（true/false）]
■例
　create_contract 1.2.17 contract.helloworld "COCOS1DE213......" "function hello() chainhelper:log('Hello World!') end" true
[block:code]
{
  "codes": [
    {
      "code": "create_contract owner name contract_authority data broadcast",
      "language": "shell"
    }
  ]
}
[/block]
結果：
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/7660524-image064.png",
        "image064.png",
        850,
        702,
        "#090909"
      ]
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "2.2.33 コントラクトのアップデート"
}
[/block]
■コマンドフォーマット
　revise_contract[更新者のユーザー名][名前またはID][データ内容][ブロードキャスト（true/false）]
■例
　revise_contract 1.2.17 contract.helloworld "function hello() chainhelper:log('Hello World!') chainhelper:log(date('%Y-%m-%dT%H:%M:%S', chainhelper:time())) end" true
[block:code]
{
  "codes": [
    {
      "code": "revise_contract owner name contract_authority data broadcast",
      "language": "shell"
    }
  ]
}
[/block]
結果：
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/5480d74-image066.png",
        "image066.png",
        850,
        670,
        "#090909"
      ]
    }
  ]
}
[/block]
結果：
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/7a32371-image066.png",
        "image066.png",
        850,
        670,
        "#090909"
      ]
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "2.2.34 コントラクトのコール"
}
[/block]
■コマンドフォーマット
　call_contract_founction[ユーザー名またはID][名前またはID][関数名][値リスト][ブロードキャスト（true/false）]
■例
call_contract_function 1.2.17 contract.helloworld [] true
[block:code]
{
  "codes": [
    {
      "code": "call_contract_function account_id_or_name contract_id_or_name function_name value_list broadcast",
      "language": "shell"
    }
  ]
}
[/block]
結果：
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/a359a8f-image068.png",
        "image068.png",
        850,
        612,
        "#060707"
      ]
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "2.2.35 アカウント内インセンティブ情報の入手"
}
[/block]
■コマンドフォーマット
　get_vesting_balances[ユーザー名]
■例
　get_vesting_balances official-account
[block:code]
{
  "codes": [
    {
      "code": "get_vesting_balances account_name",
      "language": "shell"
    }
  ]
}
[/block]
結果：
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/b084005-image070.png",
        "image070.png",
        850,
        516,
        "#050505"
      ]
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "2.2.36 インセンティブの受取（証人のみ）"
}
[/block]
■コマンドフォーマット
　withdraw_vesting[ユーザー名][金額][アセットシンボル][ブロードキャスト（true/false）]
■例
withdraw_vesting cocos-witness-0 10 XXX true
withdraw_vesting(string witness_name, string amount, string asset_symbol, bool broadcast)
[block:code]
{
  "codes": [
    {
      "code": "withdraw_vesting witness_name amount asset_symbol true",
      "language": "shell"
    }
  ]
}
[/block]
結果：
[block:api-header]
{
  "title": "2.2.37 証人に投票"
}
[/block]
■コマンドフォーマット
　vote_for_witness[ユーザー名][証人アカウント名][投票（true/false）][ブロードキャスト（true/false）]
■例
　vote_for_witness official-account cocos-witness-0 true true

投票前の手順
1．コマンドラインウォレットのディレクトリを開き、./cli_wallet-sws://127.0.0.1:8070-r127.0.0.1:8099を実行し、ウォレットへログインしてください。
2．unlock XXXを実行し、ウォレットをアンロックします。
3．import_key official-account 5KaVpJa9G4oqA5WHcSGitauFRuzdHcPVEAaESaA7jG8sを実行し、アカウントをインポートします。
4．import_balance official-account ["5KAUeN3Yv51FzpLGGf4S1ByKpMqVFNzXTJK7euqc3"] trueを実行し、アセットをインポートします。
5．vote_for_witness official-account cocos-witness-0 true trueを実行すれば、official-accountは証人cocos-witness-0に投票します。
6．手順４に従って、他の証人にも投票できます。
[block:code]
{
  "codes": [
    {
      "code": "vote_for_witness official-account cocos-witness-0 true true",
      "language": "shell"
    }
  ]
}
[/block]
結果：
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/a55248f-image072.png",
        "image072.png",
        851,
        763,
        "#060606"
      ]
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "2.2.38 理事会メンバーに投票"
}
[/block]
■コマンドフォーマット
　vote_for_committee_member[ユーザー名][証人アカウント名][投票（true/false）][ブロードキャスト（true/false）]
■例
　vote_for_committee_member official-account cocos-witness-0 true true

投票前の手順
1．コマンドラインウォレットのディレクトリを開き、./cli_wallet-sws://127.0.0.1:8070-r127.0.0.1:8099を実行し、ウォレットへログインしてください。
2．unlock XXXを実行し、ウォレットをアンロックします。
3．import_keyofficial-account 5KaVpJa9G4oqA5WHcSGitauFRuzdHcPVEAaESaA7jG8sを実行し、アカウントをインポートします。
4．import_balance official-account ["5KAUeN3Yv51FzpLGGf4S1ByKpMqVFNzXTJK7euq"] trueを実行し、アセットをインポートします。
5．vote_for_committee_member official-account Witness-0 true trueを実行すれば、official-accountは証人Witness-oに投票します。
6．手順４に従って、他の理事会メンバーにも投票できます。
[block:code]
{
  "codes": [
    {
      "code": "vote_for_committee_member official-account cocos-witness-0 true true",
      "language": "shell"
    }
  ]
}
[/block]
結果：
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/b2c710b-image074.png",
        "image074.png",
        851,
        766,
        "#060606"
      ]
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "2.2.39 理事会により手数料を変更する提議及び承認"
}
[/block]
■コマンドフォーマット
　1．propose_fee_change[ユーザー名][有効期限][変更内容][ブロードキャスト（true/false）]
　2．approve_proposal[ユーザー名][提議ID][提議者ユーザー名][ブロードキャスト（true/false）]
　例
1．propose_fee_change Witness-0 "2018-07-24T06:55:40" {"transfer" : {"fee": 244000, "price_per_kbyte": 100000}} true
2．approve_proposal Witness-0 1.10.0 {"active_approvals_to_add" : ["Witness-0"]} true

提議・承認前の手順
1．コマンドラインウォレットのディレクトリを開き、./cli_wallet-sws://127.0.0.1:8070-r127.0.0.1:8099を実行し、ウォレットへログインしてください。
2．unlock　XXXを実行し、ウォレットをアンロックします。
3．import_key Witness-0 5KaVpJa9G4oqA5WHcSGitauFRuzdHcPVEAaEを実行し、理事会メンバーアカウントをインポートします。
4．propose_fee_change Witness-0 "2018-07-24T06:55:40" {"transfer" : {"fee": 244000, "price_per_kbyte": 100000}} trueを実行し、手数料変更を提議します。
5．transfer official-account committee-account 100 XXX "" trueを実行し、ユーザーcommittee-account（提議執行者）に振込します。
6．approve_proposal Witness-0 1.10.0 {"active_approvals_to_add" : ["Witness-0"]} trueを実行し、提議を承認します（提議執行者はcommittee-accountです。理事会メンバーはそれぞれの投票数によって、committee-accountに対するweightを持っています。よって、承認したメンバーの加算weightがcommittee-accountの閾値に達した場合のみ、提議が執行されます）。
7．提議の有効期限が切れた際、システムによって提議の執行状況を判断します。執行可能な場合、提議を執行し、次のメンテナンス期間が終了すると手数料が変更されます。
[block:code]
{
  "codes": [
    {
      "code": "propose_fee_change Witness-0 \"2018-07-24T06:55:40\" {\"transfer\" : {\"fee\": 244000, \"price_per_kbyte\": 100000}} true",
      "language": "shell"
    }
  ]
}
[/block]
結果：
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/22fcda2-image076.png",
        "image076.png",
        851,
        977,
        "#040505"
      ]
    }
  ]
}
[/block]
注：表示結果が長いため、一部を抜粋して添付します。
[block:api-header]
{
  "title": "2.2.40 理事会によりオンチェーンパラメーターを変更する提議及び承認"
}
[/block]
■コマンドフォーマット
　propose_parameter_change[ユーザー名][有効期限][変更内容][ブロードキャスト（true/false）]
■例
propose_parameter_change Witness-0 "2018-07-24T06:55:40" {"committee_proposal_review_period": 300} true
■提議・承認前の手順
1．コマンドラインウォレットのディレクトリを開き、./cli_wallet-sws://127.0.0.1:8070-r127.0.0.1:8099を実行し、ウォレットへログインしてください。
2．unlock　XXXを実行し、ウォレットをアンロックします。
3．mport_key Witness-0 5KaVpJa9G4oqA5WHcSGitauFRuzdHcPVEAaEを実行し、理事会メンバーアカウントをインポートします。
4．propose_parameter_change Witness-0 "2018-07-24T06:55:40" {"committee_proposal_review_period": 300} trueを実行し、オンチェーンパラメーターにおいての提議の有効期限を変更するのを提議します。
5．transfer official-account committee-account 100 XXX "" trueを実行し、committee-account（提議執行者）に振込します。
6．approve_proposal Witness-0 1.10.1 {"active_approvals_to_add" : ["Witness-0"]} trueを実行し、承認します（提議執行者はcommittee-accountです。理事会メンバーはそれぞれの投票数によって、committee-accountに対するweightをもっています。よって、承認したメンバーの加算weightがcommittee-accountの閾値に達した場合のみ、提議が執行されます）。
7．提議の有効期限が切れた際、システムによって提議の執行状況を判断します。執行可能な場合、提議を執行し、次のメンテナンス期間が終了するとパラメーターが変更されます。

■設定可能なパラメーター一覧
"block_interval"　ブロック間隔
"maintenance_interval"　メンテナンス期間
"maintenance_skip_slots"　メンテナンスをスキップ
"committee_proposal_review_period"　提議期間
"maximum_transaction_size"　取引の上限
"maximum_block_size"　ブロックサイズの上限
"maximum_time_until_expiration"　最長有効期限
"maximum_proposal_lifetime"　提議の最長有効期限
"maximum_asset_whitelist_authorities"　アセットの最大ホワイトリスト権限
"maximum_asset_feed_publishers"　アセットが満足させる最大発行者数
"maximum_witness_count"　最大BPノード
"maximum_committee_count"　最大理事会メンバー数
"maximum_authority_membership"　最高権威者数
"reserve_percent_of_fee"　手数料
"network_percent_of_fee"　ネット料金
"lifetime_referrer_percent_of_fee"　終身会員費
"cashback_vesting_period_seconds"　返金時間（単位：秒）
"cashback_vesting_threshold"　インセンティブ閾値
"count_non_member_votes"　非会員からの投票
"allow_non_member_whitelists"　非会員のホワイトリスト
"witness_pay_per_block"　証人へのインセンティブ
"worker_budget_per_day"　日給
"max_predicate_opcode"　（一つのブロック）最大操作
"fee_liquidation_threshold"　手数料清算の閾値
"accounts_per_fee_scale"　手数料基準
"account_fee_scale_bitshifts"　アカウントの移転手数料
"max_authority_depth" 最高権限depth。一つのアカウントは別のアカウントに権限を与えます。権限をレイヤー○○まで有効するパラメーターです。
[block:code]
{
  "codes": [
    {
      "code": "propose_parameter_change Witness-0 \"2018-07-24T06:55:40\" {\"committee_proposal_review_period\": 300} true",
      "language": "shell"
    }
  ]
}
[/block]
結果：
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/b00c393-image078.png",
        "image078.png",
        851,
        1046,
        "#080808"
      ]
    }
  ]
}
[/block]