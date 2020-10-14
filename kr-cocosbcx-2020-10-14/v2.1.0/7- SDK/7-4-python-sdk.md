---
title: "7.4 Python-SDK"
slug: "7-4-python-sdk"
hidden: false
createdAt: "2019-08-26T04:48:34.446Z"
updatedAt: "2019-08-26T05:02:01.764Z"
---
## 시작하기
우리는 python3.5의 기본값으로 Ubuntu 16.04 LTS (64 비트)를 빌드 할 것을 제안합니다
** 수동 설치 : **
[block:code]
{
  "codes": [
    {
      "code": "cd python-grapheneEnhance\npython3 setup.py install --user",
      "language": "python"
    }
  ]
}
[/block]
** 블록 체인 매개 변수 수정: **
[block:code]
{
  "codes": [
    {
      "code": "vi python-grapheneEnhance/grapheneEnhancebase/chains.py # Edit blockchain related parameters\n\n```python\nknown_chains = {\n\"xxxxxx\": {\n    \"chain_id\": \"xxxxxx\",\n    \"core_symbol\": \"xxxxxx\",\n    \"prefix\": \"xxxxxx\"} # Code edited in chains.py\n```\n\npython3 setup.py install --user # Reload the python library",
      "language": "python"
    }
  ]
}
[/block]
**Python스크립트 빌드:** 

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
## API 사용자 안내서
**계정**
메소드: create_account

기능: 계정을 만들고 개인 키를 지갑으로 가져 오기

매개 변수 :
account_name : 계정 이름 등록 규칙 /^[az][a-z0-9.-]{4,63}$/는 소문자 + 숫자 또는 소문자 또는 점 또는 대시로 시작합니다. 63 자
비밀번호 : 계정 비밀번호
참고 : 평생 계정 만 계정을 만들 수 있습니다
예제:
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
메소드: upgrade_account

기능 : 계정을 평생 계정으로 업그레이드하여 특정 계정이 필요한 하위 계정을 만들 수 있습니다.

매개 변수 :
계정 : 업그레이드 된 계정
예:

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
**자산**
메소드: transfer

기능: 수신자에게 토큰 보내기

매개 변수 :
받는 사람 : 받는 사람 계정 이름
amount (int) : 전송 된 토큰의 양
자산 : 자산 ID 또는 토큰 기호
메모 : 전송 메모
계정 : 발신자 계정 이름
예:
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
메소드: asset_create

기능 : 토큰 생성

매개 변수 :
기호 : 자산 기호, 일반 ^ [. A-Z] + $
정밀도 (int) : 소수점 이하 자릿수
amount (int) : 기본 자산의 양 (즉, 생성 된 토큰, 기본값 1)
자산 : 기본 자산 ID
_amount (int) : 견적 자산 (예 : 핵심 자산, 기본값 1)
_ 자산 : 견적 자산
common_options (dict) : 토큰 옵션
bitasset_opts (dict) : 비트 토큰 옵션 (필수 아님), 기본 매개 변수를 사용하여 비트 토큰을 작성하는 경우 {} 만 전달하십시오.
is_prediction_market (bool) : 예측 시장인지 여부 (비트가 아닌 토큰은이 매개 변수에주의 할 필요가 없음)
계정 : 토큰 제작자
commen_options 매개 변수 예 :
[block:code]
{
  "codes": [
    {
      "code": "common_options = {\n    \"max_supply\": 10000000000000, # Maximum supply\n    \"market_fee_percent\": 0, # Market transaction fee percent, default\n    \"max_market_fee\": 0, # Maximum market transaction fee, default\n    \"issuer_permissions\": 79, # Permissions can be updated by issuer, default\n    \"flags\": 0, # Current permissions\n    \"core_exchange_rate\": {\"base\": {}, \"quote\": {}}, # Exchange rate with core assets, determined by the above base assets and quote assets\n    \"whitelist_authorities\": [], # Whitelist accounts\n    \"blacklist_authorities\": [], # Blacklist accounts\n    \"whitelist_markets\": [], # Whitelist assets\n    \"blacklist_markets\": [], # Blacklist assets\n    \"description\": '{\"main\":\"\",\"short_name\":\"\",\"market\":\"\"}', #Content description\n    \"extension\": {}",
      "language": "python"
    }
  ]
}
[/block]
예:

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
메소드: asset_issue

기능 : 토큰 자산 발행

매개 변수 :
금액 (int) ： 발행 금액
자산 ： 자산 기호
issue_to_account ： 발행물
메모 ： 추가 메시지 (필수 아님)
계정 ： 토큰 제작자
예:
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
**NH Asset**
메소드: register_nh_asset_creator

기능 : 현재 계정을 개발자로 등록

매개 변수 :
계정 ： 등록자 계정 이름
예:
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
메소드: create_world_view

기능 : 지원되는 NH 자산 월드 뷰 생성 및 현재 계정 (일반적으로 게임 계정)이 지원하는 NH 자산 월드 뷰를 블록 체인 시스템에 등록

매개 변수 :
world_view ： 세계관 이름
계정 ： 작성자 계정 이름
예:
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
메소드: create_nh_asset

기능 : 고유 한 NH 자산 생성

매개 변수 :
owner ： NH 자산 소유자를 지정합니다 (NH 자산 소유자 계정, 기본적으로 NH 자산 작성자)
assetID ： 현재 NH 자산의 거래에 사용되는 자산 기호
world_view ： 세계관
설명 ： 제작자가 정의한 NH 자산의 현재 내용에 대한 설명
계정 ： 제작자
예:
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
메소드: create_nh_asset_order

기능 : NH 자산 판매

매개 변수 :
otcaccount ： 보류 주문을 청구하기위한 OTC 거래 플랫폼의 계정
pending_order_fee_amount ： 보류중인 주문에 대한 수수료 금액. 사용자가 OTC 플랫폼 계정에 지불 보류 주문 수수료
pending_order_fee_asset ： 보류 주문을 지불하는 데 사용 된 자산의 기호 또는 ID입니다. 사용자가 OTC 플랫폼 계정에 지불 한 보류 주문 수수료
nh_asset ： NH 자산 ID
메모 ： 보류 주문 메모
가격 ： 주문 수량
price ： 보류 주문 가격에 사용 된 자산 기호 또는 ID
계정 ： 판매자
예:

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
**Contract**
메소드: create_contract

기능 : 스마트 계약 생성

매개 변수 :
이름 ： 계약 이름, 일반 /^[a-z][a-z0-9.-]{4,63}$/, 문자 + 문자 또는 숫자 또는 점 또는 대시로 시작-길이 4-63
데이터 ： 계약 루아 코드
con_authority ： 계약 기관 (공개 및 개인 키 쌍의 publicKey)
계정 ： 계약자
예:

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
메소드: call_contract_function

기능 : 통화 계약 기능 인터페이스

매개 변수 :
계약 ： 계약 명 또는 계약 ID
기능 ： 계약의 기능 명
value_list (list) ： 계약 기능의 파라미터리스트를 호출
계정 ： 발신자 계정 이름
value_list 매개 변수 예 :

[block:code]
{
  "codes": [
    {
      "code": "value_list = [\n        [2, {\"baseValue\": \"test1\"}], \n        [2, {\"baseValue\": \"100\")}]\n    ]",
      "language": "python"
    }
  ]
}
[/block]
예:
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
**Market**
메소드: limit_order_create

기능 : 특정 시장에서 주문 생성

매개 변수 :
금액 (int) ： 판매 된 토큰의 수량
자산 ： 자산 ID 또는 토큰 기호 판매
min_amount (int) ： 획득해야하는 최소 토큰 양
min_amount_asset ： 자산 ID 또는 토큰 심볼을 가져와야합니다.
fill (bool) ： 기본값은 False입니다. 이 플래그가 True로 설정되면이 주문을 완전히 구매하거나 거부해야합니다.
계정 ： 판매자 계정 이름
예:

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
메소드: limit_order_cancel

기능 : 특정 시장에서 주문 취소

매개 변수 :
order_number (list) ： 취소 할 한도 주문의 ID
계정 ： 운영자 계정 이름
예:

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
**Witness**
메소드: create_witness

기능 : 증인 후보 생성

매개 변수 :
account_name ： 증인 후보자 계정
url ： 증인 웹 링크
키 ： 증인 차단 서명 공개 키
예:


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
메소드: approve_witness

기능 : 증인 후보자 투표

매개 변수 :
증인 (목록) : 증인 계정 이름 또는 증인 ID
계정 ： 투표 계정 이름
예:

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
**Committee**
메소드: committee_member_create

기능 :위원회 위원 후보 생성
매개 변수 :
url ： weblink
계정 ：위원회 위원 후보자 계정
예:


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
메소드: committee_member_update

기능 : 위원 후보 업데이트

매개 변수 :
new_url ： 새로운 웹 링크
계정 ：위원회 위원 후보자 계정 업데이트
예:

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
**Proposal**
메소드: relate_world_view

기능 : 월드 뷰와 연결하기 위해 개발자는 특정 월드 뷰에 연결 한 후에 만 월드 뷰의 NH 자산을 만들 수 있습니다. 월드 뷰 제작자가 승인 한 제안서를 통해 작업을 완료해야합니다.

매개 변수 :
world_view ： 세계관 이름
계정 ： 연결된 계정 이름
예:
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
메소드: approveproposal

기능 : 다른 사용자의 제안을 월드 뷰와 연결하도록 승인

매개 변수 :
proposal_ids (list) ： 제안서 ID
계정 ： 제안 된 계정 업데이트
예:

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
**Example of Wallet API Call:**
메소드: unlock

기능 : 관련 지갑 조작을 위해 지갑 잠금 해제

매개 변수 :
비밀번호 ： 지갑 비밀번호
예:

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
메소드: getAccounts

기능 : 지갑 데이터베이스에서 계정 정보 얻기
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
메소드: getPrivateKeyForPublicKey

기능 : 주어진 공개 키에 따라 지갑에서 해당 개인 키를 가져옵니다.

매개 변수 :
펍 ： 공개 열

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
**Example of RPC Interface Call:**
메소드: get_object

기능 :이 객체 정보를 얻는다

매개 변수 :
object_id ： 객체 id
예:

[block:code]
{
  "codes": [
    {
      "code": "print(gph.rpc.get_object(\"1.2.18\")) # Get account information of id \"1.2.17\"",
      "language": "python"
    }
  ]
}
[/block]
메소드: get_contract

기능 : 계약 내용 얻기

매개 변수 :
contract_id ： 계약 ID 또는 계약 명
예:

[block:code]
{
  "codes": [
    {
      "code": "print(gph.rpc.get_contract(\"1.16.0\")) # Get contract details of id \"1.16.0\"",
      "language": "python"
    }
  ]
}
[/block]
## Main-Packages 
**grapheneEnhance**
설명 : 하위 모듈은 계정, 자산, 블록, 제안서, 계약서 등과 같은 블록 체인 시스템과 관련된 모든 클래스에 해당합니다. 각 클래스에는 해당하는 호출 방법이 있습니다. 그래 핀 모듈에는 자금 이체, 계좌 생성, 자산 생성, 계약 생성 등과 같이 호출 할 수있는 작업과 관련된 API가 있습니다.

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

grapheneEnhancebase
설명 : 하위 모듈에는 일반적으로 변경하지 않아도되는 블록 체인 정보, 객체 유형, 작업, 데이터 구조 등과 같은 기본 설계와 관련된 내용이 포함됩니다. 체인 모듈은 초기화시 블록 체인 사용에 따라 수정해야합니다.

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