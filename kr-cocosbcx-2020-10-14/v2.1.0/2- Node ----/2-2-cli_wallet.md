---
title: "2.2 cli_wallet"
slug: "2-2-cli_wallet"
hidden: false
createdAt: "2019-08-26T04:48:34.415Z"
updatedAt: "2019-08-26T05:02:01.753Z"
---
블록 체인과의 상호 작용을 지원하는 월렛 커맨드라인툴입니다. 작동 내용은 아래과 같습니다.
[block:api-header]
{
  "type": "basic",
  "title": "2.2.1 로그인"
}
[/block]
1. 커맨드라인 지갑 실행 파일 cli_wallet을 가져 와서 스케줄된 디렉토리로 복사하십시오.
2. 커맨드라인 지갑이 있는 디렉토리로 이동하십시오. 다음 명령을 실행하여 커맨드라인 지갑에 로그인하십시오.
** 명령 형식 **
--chain-id [체인 ID] -s [증인 노드 RPC 주소] -r [명령 줄 지갑의 RPC 서비스가 수신하는 주소]
[block:code]
{
  "codes": [
    {
      "code": "./cli_wallet --chain-id 81003974d328ff17b64076928ab87b24d7dffbc87df3d4cde89d2fa1877e4f6a -s ws://127.0.0.1:8070 -r 127.0.0.1:8099",
      "language": "shell"
    }
  ]
}
[/block]
**결과값: **
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/fad6cb7-cda4ef2-2.2.1.2.png",
        "cda4ef2-2.2.1.2.png",
        804,
        341,
        "#0d0c0c"
      ]
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "2.2.2 지갑의 비밀번호 설정하기"
}
[/block]
1. 처음 로그인 할 때 지갑 비밀번호를 설정해야합니다
**명령 형식**
unlock [비밀번호설정]
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
**결과값: **
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/6fd21cc-4cdbbbb-2.2.2.1.png",
        "4cdbbbb-2.2.2.1.png",
        802,
        80,
        "#050605"
      ]
    }
  ]
}
[/block]
2. 비밀번호를 설정 한 후 지갑을 잠금 해제해야합니다.
**명령 형식 **
unlock [비밀번호 설정]
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
**결과값: **
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/3de7f51-cb078c6-2.2.2.2.png",
        "cb078c6-2.2.2.2.png",
        804,
        82,
        "#040504"
      ]
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "2.2.3 계정을 지갑으로 가져 오기"
}
[/block]
1. 로그인하여 지갑을 잠금 해제하고 다음 명령을 실행하여 사용자 정보를 가져옵니다.
**명령 형식**
import_key [사용자이름] [사용자 개인키]
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
**결과값: **
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/2cddec1-9039bac-2.2.3.3.png",
        "9039bac-2.2.3.3.png",
        803,
        159,
        "#0c0d06"
      ]
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "2.2.4 지갑으로 자산 가지고 오기"
}
[/block]
1. 자산을 가져 오기 위해 지갑을 잠금 해제하려면 로그인하십시오
** 명령 형식 **
import_balance [사용자 이름] [자산 주소에 해당하는 개인 키] [브로드 캐스트 (참 / 거짓)]
**문맥**
설립 자산이 수출되지 않은 새로운 체인
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
**결과값:**
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/7f217c8-096c7a8-2.2.4.png",
        "096c7a8-2.2.4.png",
        803,
        139,
        "#090a07"
      ]
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "2.2.5 트렌스퍼"
}
[/block]
**명령형식**
import_balance [transfer] [from to] [amount] [token asset type] [remarks] [broadcast (true/false)]
**상태값**
지갑을 잠금 해제하려면 로그인하십시오. 계좌 잔고가 충분해야합니다
**예시**
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
**결과값:**
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/3f3d293-16e8e31-2.2.5.png",
        "16e8e31-2.2.5.png",
        937,
        721,
        "#050505"
      ]
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "2.2.6 등록"
}
[/block]
**명령 형식**
register_account [username] [owner public key] [active public key] [registrar account name] [referrer account name] [cost percentage] [broadcast (true/false)]
**상태값**
지갑을 잠금 해제하려면 로그인하십시오. 레지스트라는 계정에 잔액이 충분한 회원이어야합니다
**예시**
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
**결과값:**
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/e7447e3-45d2364-2.2.6.png",
        "45d2364-2.2.6.png",
        798,
        1218,
        "#060606"
      ]
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "2.2.7 회원 계정 업그레이드"
}
[/block]
**상태값**
계정에 잔액이 충분해야 합니다. 
**명령 형식 **
upgrade_account [username] [broadcast (true/false)]
**예시**
upgrade_account test-account true
**참고**
cli_wallet supports upgrading to a lifetime membership only, but not the annual membership.
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
**결과값:**
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/327eded-38a7171-2.2.7.png",
        "38a7171-2.2.7.png",
        802,
        525,
        "#050606"
      ]
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "2.2.8 체인ID, 활동중인 증인, 위원회 회원정도 어디"
}
[/block]
**명령 형식**
info
[block:code]
{
  "codes": [
    {
      "code": "info",
      "language": "shell"
    }
  ]
}
[/block]
**결과:**
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/dce4540-3701e25-2.2.8.png",
        "3701e25-2.2.8.png",
        801,
        743,
        "#040404"
      ]
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "2.2.9 클라이언트 버전, 컴파일 시간, 부스트 버전, openssl 버전 등과 같은 정보 반환"
}
[/block]
**명령 형식**
about
[block:code]
{
  "codes": [
    {
      "code": "about",
      "language": "text"
    }
  ]
}
[/block]
**결과:**
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/fc9bb34-c22898e-2.2.9.png",
        "c22898e-2.2.9.png",
        802,
        249,
        "#070707"
      ]
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "2.2.10 지정된 블록 정보 얻기"
}
[/block]
**명령 형식**
get_block [block height]
**예시**
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
**결과값:**
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/3c8d992-d43e894-2.2.10.png",
        "d43e894-2.2.10.png",
        803,
        249,
        "#0a0a0a"
      ]
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "2.2.11 체인에 등록된 총 계정수 얻기"
}
[/block]
**명령 형식**
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
**결과값:**
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/fdaaa2c-c7337d0-2.2.11.png",
        "c7337d0-2.2.11.png",
        800,
        59,
        "#040504"
      ]
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "2.2.12 지갑으로 가져온 계정 나열하기"
}
[/block]
**명령 형식**
list_my_accounts
[block:code]
{
  "codes": [
    {
      "code": "list_my_accounts",
      "language": "shell"
    }
  ]
}
[/block]
**결과값:**
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/49a8528-c12c6f3-2.2.12.png",
        "c12c6f3-2.2.12.png",
        801,
        1132,
        "#050505"
      ]
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "2.2.13 잔고목록"
}
[/block]
**명령 형식**
list_account_balances [account name]
**예시**
list_account_balances official-account
[block:code]
{
  "codes": [
    {
      "code": "list_account_balances official-account ",
      "language": "shell"
    }
  ]
}
[/block]
**결과값:**
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/690922b-e5b10d7-2.2.13.png",
        "e5b10d7-2.2.13.png",
        800,
        77,
        "#070707"
      ]
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "2.2.14 온체인 토큰 목록"
}
[/block]
**명령 형식 **
list_assets [lowerbound] [limit]
**예시**
list_assets “” 1
**참고**
The return results are sorted by the token symbols. The “lower bound” parameter is the minimum limit, and the “limit” is the maximum number of returns, which is to return a maximum of “limit” tokens whose symbol is not less than the “lower bound”.
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
**결과:**
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/ddc2b7a-1cd17d4-2.2.14.png",
        "1cd17d4-2.2.14.png",
        799,
        663,
        "#040404"
      ]
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "2.2.15 계정 기록 얻기"
}
[/block]
**명령 형식**
get_account_history [account name] [limit]
**예시**
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
**결과:**
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/eb42f00-aebe3bf-2.2.15.png",
        "aebe3bf-2.2.15.png",
        803,
        124,
        "#0b0c0b"
      ]
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "2.2.16 수수료와 같은 정적 속성 가져 오기"
}
[/block]
**명령 형식*
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
**결과:**
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/a7cc8fd-5c4a6db-2.2.16.1.png",
        "5c4a6db-2.2.16.1.png",
        796,
        944,
        "#020202"
      ],
      "caption": "결과값 출력 모습"
    }
  ]
}
[/block]

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/d120f09-0f69190-2.2.16.2.png",
        "0f69190-2.2.16.2.png",
        793,
        1228,
        "#050606"
      ]
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "2.2.17 헤드 블록 ID, 시간 및 다음 유지 보수 시간과 같은 동적 특성 가져 오기"
}
[/block]
**명령 형식 **
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
**결과:**
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/03a94b3-1f1b7f3-2.2.17.png",
        "1f1b7f3-2.2.17.png",
        796,
        381,
        "#080808"
      ]
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "2.2.18 계정 정보 얻기"
}
[/block]
**명령 형식 **
get_account  [account name or ID]
**예시**
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
**결과:**
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/9d74168-579f8bb-2.2.18.png",
        "579f8bb-2.2.18.png",
        797,
        1142,
        "#050505"
      ]
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "2.2.19 토큰 자산 정보 얻기"
}
[/block]
**명령 형식 **
get_asset  [asset name or ID]
**예시**
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
**결과:**
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/69542a7-0f8a2a0-2.2.19.png",
        "0f8a2a0-2.2.19.png",
        793,
        644,
        "#040404"
      ]
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "2.2.20 계정ID 얻기"
}
[/block]
**명령 형식 **
get_account_id [account name]
**예시**
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
**결과:**
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/871445c-87ccf1d-2.2.20.png",
        "87ccf1d-2.2.20.png",
        795,
        63,
        "#050505"
      ]
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "2.2.21 토큰 자산에 대한 정보 얻기"
}
[/block]
**명령 형식**
get_asset [account name]
**예시**
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
**결과:**
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/ac02962-d9adb1e-2.2.21.png",
        "d9adb1e-2.2.21.png",
        794,
        649,
        "#040404"
      ]
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "2.2.22 객체 얻기"
}
[/block]
**명령 형식*
get_object [object ID]
**예시**
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
**결과:**
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/7edff75-c4c2912-2.2.22.png",
        "c4c2912-2.2.22.png",
        795,
        1248,
        "#040505"
      ]
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "2.2.23 프라이빗 키 얻기"
}
[/block]
**명령 형식 **
get_private_key [public key]
**예시**
get_private_key XXX6esv8d6u2eqzKyiQvCYJa6XK74c7BrmzUqL4Z3
**참고**
The private key must be saved in the wallet.
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
**결과:**
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/aa570e0-3c07c29-2.2.23.png",
        "3c07c29-2.2.23.png",
        804,
        98,
        "#0e0f0e"
      ]
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "2.2.24 지갑 동결"
}
[/block]
**명령 형식 **
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
**결과:**
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/73234aa-e762508-2.2.24.png",
        "e762508-2.2.24.png",
        799,
        64,
        "#020202"
      ]
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "2.2.25 안전한 brain key, public key, and private key 그룹의 변환"
}
[/block]
**명령 형식**
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
**결과:**
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/858accf-c5c3cfe-2.2.25.png",
        "c5c3cfe-2.2.25.png",
        802,
        163,
        "#0c0d0d"
      ]
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "2.2.26 Committee member 등록"
}
[/block]
**명령 형식 **
create_committee_member [account name] [url address] [broadcast (true/false)]
**예시**
create_committee_member official-account "http://my-web" true
**참고**
The user becomes a candidate committee member after registration. He will be the official member only by winning the vote.
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
**결과:**
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/60b8675-9a05f1c-2.2.26.png",
        "9a05f1c-2.2.26.png",
        797,
        495,
        "#060706"
      ]
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "2.2.27 Witness 등록"
}
[/block]
**명령 형식 **
create_witness [account name] [url address] [broadcast (true/false)]
**예시**
create_witness official-account "http://my-web" true
**참고**
The user becomes​ a candidate witness after application. He will be the official witness only by winning the vote.
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
**결과:**
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/35cca73-505a3c8-2.2.27.png",
        "505a3c8-2.2.27.png",
        802,
        539,
        "#060706"
      ]
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "2.2.28 Witnesses 목록"
}
[/block]
**명령 형식**
list_witnesses [lowerbound] [limit]
**예씨**
list_witnesses "" 100
**참고**
Returned results are sorted by the witness account name. The “lowerbound” parameter is the minimum limit, and the “limit” is the maximum number of returns.
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
**결과:**
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/637a9d4-8c49eb3-2.2.28.png",
        "8c49eb3-2.2.28.png",
        795,
        200,
        "#020303"
      ]
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "2.2.29 Committee members 목록"
}
[/block]
**명령 형식**
list_committee_members [lowerbound] [limit]
**예시**
list_committee_members "" 100
**참고**
Returned results are sorted by the committee member account name. The “lowerbound” parameter is the minimum limit, and the “limit” is the maximum number of returns.
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
**결과:**
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/9bbf319-5d8b01e-2.2.29.png",
        "5d8b01e-2.2.29.png",
        802,
        203,
        "#030303"
      ]
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "2.2.30 Witness 정보 얻기"
}
[/block]
**명령 형식**
get_witness [witness name or ID]
**예시**
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
**결과:**
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/cc64bc1-c162d5b-2.2.30.png",
        "c162d5b-2.2.30.png",
        802,
        522,
        "#060606"
      ]
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "2.2.31 Committee member 얻기"
}
[/block]
*명령 형식 **
get_committee_member [committee member name or ID]
**예시**
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
**결과:**
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/7a644af-8cb9fd9-2.2.31.png",
        "8cb9fd9-2.2.31.png",
        801,
        180,
        "#060606"
      ]
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "2.2.32 계약 생성"
}
[/block]
**명령 형식**
create_contract [contract owner] [contract name] [contract authority (publicKey in a pair of public and private keys)] [data] [broadcast (true/false)]
**예시**
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
**결과:**
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/2152d21-2ee3d29-2.2.32.png",
        "2ee3d29-2.2.32.png",
        805,
        665,
        "#080908"
      ]
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "2.2.33 계약 갱신"
}
[/block]
**명령 형식**
revise_contract [contract updater username] [contract name or ID] [data] [broadcast (broadcast (true/false))]
**예시**
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
**결과:**
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/aea1c38-45637c9-2.2.33.png",
        "45637c9-2.2.33.png",
        804,
        634,
        "#080808"
      ]
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "2.2.34 계약 호출"
}
[/block]
**명령 형식 **
call_contract_function [username or ID] [contract name or contract ID] [function name] [value list] [broadcast (true/false)]
**예시**
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
**결과:**
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/c7d554f-36057ef-2.2.34.png",
        "36057ef-2.2.34.png",
        804,
        579,
        "#060606"
      ]
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "2.2.35 계정 바운티 잔고 표시"
}
[/block]
***명령 형식**
get_vesting_balances [username]
**예시**
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
**결과:**
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/e10a027-66fefac-2.2.35.png",
        "66fefac-2.2.35.png",
        797,
        484,
        "#050505"
      ]
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "2.2.36 바운티 얻기 (for witnesses only)"
}
[/block]
**명령 형식 **
withdraw_vesting [witness name] [amount] [asset symbol] [broadcast (true/false)]
**예시**
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

[block:api-header]
{
  "title": "2.2.37 Witnesses 투표"
}
[/block]
**명형 형식**
vote_for_witness [username] [witness username] [agree or not] [broadcast (true/false)]
**예시**
vote_for_witness official-account cocos-witness-0 true true
**필수 단계**
1. 명령 행 지갑이있는 디렉토리로 이동하여 ./cli_wallet-sws://127.0.0.1:8070-r127.0.0.1:8099 명령을 실행하여 지갑에 로그인하십시오.
2. unlock xxxx 명령을 실행하여 지갑을 잠금 해제하십시오.
3. import_key 공식 계정 5KaVpJa9G4oqA5WHcSGitauFRuzdHcPVEAaESaA7jG8s를 실행하여 사용자를 가져옵니다.
4. import_balance official-account [ "5KAUeN3Yv51FzpLGGf4S1ByKpMqVFNzXTyKpeuqc3"] true 명령을 실행하여 사용자의 자산을 가져옵니다.
5. vote_for_witness 공식 계정 cocos-witness-0 명령을 실행합니다. true, 공식 계정이 감시 계정 cocos-witness-0에 투표합니다.
6. 4 단계에 따라 다른 증인에게 투표하십시오.
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
**결과:**
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/4c02453-3eb8d64-2.2.37.png",
        "3eb8d64-2.2.37.png",
        801,
        718,
        "#050605"
      ]
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "2.2.38 Committee members 투표"
}
[/block]
**명령 형식**
vote_for_committee_member [username] [witness username] [agree or not] [broadcast (true/false)]
**예시**
vote_for_committee_member official-account cocos-witness-0 true true
**필수 단계**
1. 명령 행 지갑이있는 디렉토리로 이동하여 ./cli_wallet-sws://127.0.0.1:8070-r127.0.0.1:8099 명령을 실행하여 명령 행 지갑에 로그인하십시오.
2. unlock xxxx 명령을 실행하여 지갑을 잠금 해제하십시오.
3. import_key 공식 계정 5KaVpJa9G4oqA5WHcSGitauFRuzdHcPVEAaESaA7jG8s를 실행하여 사용자를 가져옵니다.
4. import_balance official-account "5KAUeN3Yv51FzpLGGf4S1ByKpMqVFNzXTJK7euq"] true 명령을 실행하여 사용자의 자산을 가져옵니다.
5. vote_for_committee_member official-account Witness-0 명령을 실행하십시오. true, 공식 계정은 감시 계정 cocos-witness-0에 투표합니다.
6. 4 단계에 따라 다른 증인에게 투표하십시오.
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
**결과:**
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/e8722cb-55f232b-2.2.38.png",
        "55f232b-2.2.38.png",
        802,
        723,
        "#050606"
      ]
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "2.2.39 수수료 변경에 대한 Committee member의 제안"
}
[/block]
**명령 형식**
1. propose_fee_change [username] [deadline] [content] [broadcast (true/false)]
2. approve_proposal [username] [proposal ID] [proposer username] [broadcast (true/false)]
**예시**
1. propose_fee_change Witness-0 "2018-07-24T06:55:40" {"transfer" : {"fee": 244000, "price_per_kbyte": 100000}} true
2. approve_proposal Witness-0 1.10.0 {"active_approvals_to_add" : ["Witness-0"]} true
**필수 단계**
1. 명령 행 지갑이있는 디렉토리로 이동하여 ./cli_wallet-sws://127.0.0.1:8070-r127.0.0.1:8099 명령을 실행하여 명령 행 지갑에 로그인하십시오.
2. unlock xxxx 명령을 실행하여 지갑을 잠금 해제하십시오.
3. import_key Witness-0 5KaVpJa9G4oqA5WHcSGitauFRuzdHcPVEAaE를 실행하여 사용자를 가져옵니다.
4. propose_fee_change Witness-0 "2018-07-24T06 : 55 : 40"{ "transfer": { "fee": 244000, "price_per_kbyte": 100000}} 명령을 실행하여 전송 요금 변경 제안
5. 사용자위원회 계정으로 이전하려면 명령 이전 공식 계정위원회 계정 100 XXX ""true를 실행하십시오 (사용자는 제안된 실행 자임)
6. approve_proposal Witness-0 1.10.0 { "active_approvals_to_add": [ "Witness-0"]} 명령을 실행하여 제안을 승인합니다 (제안 집행자는위원회 계정이며 각위원회 구성원은 특정 활동 위원회 위원이 획득 한 투표 수에 따른 계정의 권한 가중치이므로 제안을 승인 한 위원의 가중치가위원회 계정의 임계 값을 초과하면 제안을 실행할 수 있습니다.)
7. 제안서가 만료 되려고 할 때 시스템은 제안서의 실행 가능 여부를 자동으로 결정합니다. 그렇다면 제안서가 실행 된 후 다음 유지 보수 후에 수수료가 업데이트됩니다.
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

[block:code]
{
  "codes": [
    {
      "code": "approve_proposal Witness-0 1.10.0 {\"active_approvals_to_add\" : [\"Witness-0\"]} true",
      "language": "shell"
    }
  ]
}
[/block]
결과:
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/a307e31-f14ea5b-2.2.39.1.png",
        "f14ea5b-2.2.39.1.png",
        799,
        918,
        "#040404"
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
        "https://files.readme.io/f802137-3a00cea-2.2.39.2.png",
        "3a00cea-2.2.39.2.png",
        800,
        956,
        "#070707"
      ]
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "2.2.40 체인의 글로벌 파라미터 변경에 대한 Committee member의 제안"
}
[/block]
◼ 명령 형식
propose_parameter_change [username] [deadline] [content] [broadcast (true/false)]
◼ 예시
propose_parameter_change Witness-0 "2018-07-24T06:55:40" {"committee_proposal_review_period": 300} true
◼ 필수 단계
1. 명령 행 지갑이있는 디렉토리로 이동하여 ./cli_wallet-sws://127.0.0.1:8070-r127.0.0.1:8099 명령을 실행하여 명령 행 지갑에 로그인하십시오.
2. unlock xxxx 명령을 실행하여 지갑을 잠금 해제하십시오.
3. import_key Witness-0 5KaVpJa9G4oqA5WHcSGitauFRuzdHcPVEAaE 명령을 실행하여위원회 구성원 사용자를 가져 오십시오.
4. Prepare_parameter_change Witness-0 "2018-07-24T06 : 55 : 40"{ "committee_proposal_review_period": 300} 명령을 실행하여위원회가 제안한 체인의 전체 매개 변수 검토 기간을 변경하도록 제안합니다.
5.위원회 계정으로 이전하려면 명령 이전 공식 계정위원회 계정 100 XXX ""true를 실행하십시오 (사용자는 제안 된 실행 자임)
6. approve_proposal Witness-0 1.10.0 { "active_approvals_to_add": [ "Witness-0"]} 명령을 실행하여 제안을 승인합니다 (제안 집행자는위원회 계정이며 각위원회 구성원은 특정 활성 권한을가집니다. 위원회 위원이 획득 한 투표 수에 따른 계정의 가중치 따라서 제안을 승인 한 위원의 가중치가위원회 계정의 임계 값을 초과하면 제안을 실행할 수 있습니다.)
7. 제안서가 만료 되려고 할 때 시스템은 제안서의 실행 가능 여부를 자동으로 결정합니다. 그렇다면 제안서가 실행 된 후 다음 유지 보수 후에 수수료가 업데이트됩니다.

◼ 구성 가능한 매개 변수
"block_interval"	
"maintenance_interval"	
"maintenance_skip_slots"
"committee_proposal_review_period"	
"maximum_transaction_size"	
"maximum_block_size"	
"maximum_time_until_expiration"	
"maximum_proposal_lifetime"	
"maximum_asset_whitelist_authorities"	
"maximum_asset_feed_publishers"
"maximum_witness_count"
"maximum_committee_count"
"maximum_authority_membership"
"reserve_percent_of_fee"
"network_percent_of_fee"
"lifetime_referrer_percent_of_fee"	
"cashback_vesting_period_seconds"	
"cashback_vesting_threshold"	
"count_non_member_votes"	
"allow_non_member_whitelists"	
"witness_pay_per_block"	
"worker_budget_per_day"	
"max_predicate_opcode"	
"fee_liquidation_threshold"	
"accounts_per_fee_scale"	
"account_fee_scale_bitshifts"	
"max_authority_depth"	One account can authorize another account. This parameter can be configured to be effective up to several layers downwards.
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
결과:
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/68937b7-8446cfe-2.2.40.2.png",
        "8446cfe-2.2.40.2.png",
        800,
        984,
        "#070808"
      ]
    }
  ]
}
[/block]