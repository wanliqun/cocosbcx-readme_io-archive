---
title: "5.5 계약 API"
slug: "5-5-api"
hidden: false
createdAt: "2019-08-26T04:48:34.431Z"
updatedAt: "2019-08-26T05:02:01.761Z"
---
##1. 사용자 가이드
Cocos-BCX 스마트 계약은 Lua로 작성되었으며 모든 구문은 공식 5.3 버전을 기반으로 수정되었습니다. 온-체인 작동 기능은 블록 체인에서 실행하기에 더 적합하도록 기능별 라이브러리가 조정된 상태입니다. 

**1.1. 기본 개념**
**계약 데이터**
계약 데이터는 사용자 데이터 영역과 공개 데이터 영역으로 구분됩니다.
◆ 사용자 데이터 영역은 계약이 호출된 후 사용자가 생성한 데이터를 저장하는 데 사용됩니다. 사용자 데이터 영역은 계약 작성자가 직접 정의합니다.
◆ 공개 데이터 영역은 계약 규칙의 데이터를 저장하는 데 사용되며 계약 작성자는 소유자 어설션 (예 : assert (is_owner ()))을 사용하여 발신자를 한정 할 수 있습니다. 공개 데이터 영역은 public_data 테이블에 의해 기록되며 계약 작성자는 공개 데이터를 public_data 객체에 넣는데 주의를 기울여야합니다.

** 특정 객체 **
◆ public _data
공용 데이터 영역을 기록하는 데 사용됩니다. 오브젝트 특성은 계약 작성자가 정의합니다.
◆ private_data
사용자 데이터 영역은이 계약의 호출자를 가리 킵니다.
◆ read_list
계약 데이터 IO의 레지스트리를 읽는 중입니다. 계약은 read_list 테이블을 작성하여로드 될 컨텍스트를 알릴 수 있습니다. 기본 상태는 read_list = {public_data = {}, private_data = {}}이며 public_data 및 private_data 파티션의 모든 데이터는 기본적으로로드됩니다.
read_list = {public_data = {test = true}}는 public_data.test 데이터 만 읽으며 read_chain () 함수가 실행될 때 적용됩니다.
◆ write_list
계약 데이터 IO의 레지스트리 작성 계약은 write_list 테이블을 작성하여 체인이 기록 할 컨텍스트를 알릴 수 있습니다. 기본 상태는 read_list = {public_data = {}, private_data = {}}이며 public_data 및 private_data 파티션의 모든 데이터는 기본적으로 기록됩니다.
write_list = {public_data = {test = true}}는 public_data.test 데이터 만 작성하며 write_chain () 함수가 실행될 때 적용됩니다. (true / false)는 write_list의 각 경로 값입니다. 여기서 true는 존재하는 경우 업데이트되고 존재하지 않는 경우 작성되며, 존재하는 경우 지워짐을 나타냅니다. ;
◆ contract_base_info
계약을 저장하는 데 사용되는 기본 정보입니다. 계약 내의 오브젝트에 대한 수정 사항은 기록되지 않습니다. 개체 속성 : 이름 (계약 이름), id (계약 ID), 소유자 (계약 소유자 ID), 발신자 (현재 발신자 ID), creation_date (계약 작성 시간), contract_authority (계약은 승인에 의해 서명되어야 함)

## 1.2. 노트
** 계약 세션 복구 메커니즘에는 런타임 코드 복구가 포함되지 않습니다 **
즉, 람다 식은 table 및 metatable의 동적 속성 함수를 포함하여 현재 함수 컨텍스트에서만 유효합니다.
** 균일 계약 애플리케이션 레이어 테이블 데이터 구조, 메타 테이블 비활성화 **
이유:
◆ 람다 함수는 메타 테이블에서 일반적이지만 런타임 코드는 복원 할 수 없습니다.
◆ 메타 테이블 데이터 구조 IO의 속도는 테이블 데이터 구조의 속도보다 느립니다.

## 2. 기본 모듈 및 확장
** 2.1. 기본 모듈 **
계약 샌드 박스는 계약 번호 0의 ​​구성에 따라 기본 모듈을 지원하도록 제어 할 수 있습니다. 후속 번호 0 기본 지원 계약은 위원회에서 관리합니다.
** 2.2. 확장명 **
** 2.2.1. CJSON 모듈 **
CJSON 모듈은 종종 들어오는 함수 구조화 된 매개 변수를 구문 분석하는 데 사용됩니다.
현재 계약 ABI는 외부 테이블 데이터 구조의 매개 변수를 승인했지만 오브젝트를 전달하고 오브젝트의 직렬화를 문자열로 전달하기 위해 CJSON 모듈을 계속 보유합니다.
호출 방식 :
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
## 3. 계약 체인 상호 작용 모듈-정적 기능
체인 상호 작용 모듈의 정적 함수는 함수 이름과의 계약에서 직접 호출 할 수 있습니다.
** get_account_contract_data **

** 프로토 타입 **
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
** 설명 **
특정 사용자의 해당 경로의 사용자 데이터를 읽습니다.
** 반환 값 **
테이블 구조의 사용자 데이터를 반환합니다. 경로에 지정된 데이터가 없으면 해당 테이블 분기가 비어 있습니다.
**예**
nico_data = get_account_contract_data ( 'nicotest', {nicodata0 = {nicodata1 = true})
이 계약의 nicotest 계정에서 nicodata0.nicodata1 데이터를 읽으려면 nicotest가 계약 호출자 인 경우 nico_data는 private_data.nicodata0.nicodata1과 같아야합니다.

## 4. 계약 체인 상호 작용 모듈-동적 함수
"chainhelper : function name (parameter ...)"에 따라 계약에서 체인 상호 작용 모듈의 동적 기능을 호출해야합니다.

** 4.1. 해시 256 **

** 프로토 타입 **
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
** 반환 값 **
해시 256 문자열 반환
** 매개 변수 **
소스 : 계산해야하는 소스 데이터

** 4.2. 해시 512 **

** 프로토 타입 **
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
** 반환 값 **
해시 512 문자열 반환
** 매개 변수 **
소스 : 계산해야하는 소스 데이터

** 4.3. create_nh_asset **

** 프로토 타입 **
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
** 설명 **
비 균일 항목을 작성하려면 계약 소유자에게 해당 작성 권한이 있어야합니다.
** 매개 변수 **
name_or_id : 새 항목의 소유자
기호 : 순환 제한 동종 자산 기호 (예비) 예 : COCOS
world_view : 월드 뷰
base_describe : 기본 설명
enable_logger : 계약 결과에 관련 영향이 기록되는지 식별

** 4.4. adjust_lock_asset **

** 프로토 타입 **
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
** 설명 **
계약 소유자가이 계약에서 잠근 자산을 조정하십시오.
** 매개 변수 **
symbol_or_id : 조정해야 할 자산 ID 또는 기호
금액 : 정밀도가있는 숫자는 음수 일 수 있습니다 (잠금 금액을 줄이려는 의미). 조정 후 잠금 금액은 0보다 커야하지만 계약 소유자의 해당 자산의 최대 금액보다 작아야합니다.

** 4.5. read_chain **

** 프로토 타입 **
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
** 설명 **
read_list 레지스트리에 해당하는 계약 데이터 IO 읽기

** 4.6. write_chain **

** 프로토 타입 **
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
** 설명 **
write_list 레지스트리에 해당하는 계약 데이터 IO 쓰기

** 4.7. get_account_balancen **

** 프로토 타입 **
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
** 설명 **
지정된 계정의 동종 자산 잔액 조회
** 반환 값 **
균형
** 매개 변수 **
account_name_or_id : 조회 할 계정 이름 또는 ID
asset_symbol_or_id : 쿼리 할 자산 심볼 또는 ID

** 4.8. transfer_from_caller **
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
**프로토타입**
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
** 설명 **
계약 호출자에서 계정으로 자산을 이전합니다. 금액은 토큰, 토큰 기호 : 기호입니다.
** 매개 변수 **
받는 사람 :받는 사람의 계정 ID
토큰 : 금액은 0보다 크고 루아 수의 최대 범위보다 작아야합니다.
기호 : 자산 기호
enable_logger : 계약 결과에 관련 영향이 기록되는지 식별

** 4.9. transfer_from_owner **

** 프로토 타입 **
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
** 설명 **
계약 호출자에서 계정으로 자산을 이전합니다. 금액은 토큰, 토큰 기호 : 기호입니다.
** 매개 변수 **
받는 사람 :받는 사람의 계정 ID
토큰 : 금액은 0보다 크고 루아 수의 최대 범위보다 작아야합니다.
기호 : 자산 기호
enable_logger : 계약 결과에 관련 영향이 있는지 식별

** 4.10. make_memo **

** 프로토 타입 **
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
** 설명 **
암호화 된 데이터 생성자.
** 매개 변수 **
받는 사람 : 지정된 메시지 암호 해독기 계정 ID
키 : ECC 공유 키에서 제공 한 비밀번호 시드
값 : 암호화 된 콘텐츠
enable_logger : 계약 결과에 관련 영향이 기록되는지 식별

** 4.11. transfer_nht_from_caller **

** 프로토 타입 **
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
** 설명 **
비균질 자산을 계약 발신자에서 계정으로 이체
** 매개 변수 **
받는 사람 :받는 사람의 계정 ID
token_hash_or_id : 지정된 비균질 토큰 해시 값 또는 ID
enable_logger : 계약 결과에 관련 영향이 기록되는지 식별

** 4.12. transfer_nht_from_owner **

** 프로토 타입 **
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
** 설명 **
비균질 자산을 계약 소유자에서 계정으로 이전
** 매개 변수 **
받는 사람 :받는 사람의 계정 ID
token_hash_or_id : 지정된 비균질 토큰 해시 값 또는 ID
enable_logger : 계약 결과에 관련 영향이 기록되는지 식별

** 4.13. change_nht_active_by_owner **

** 프로토 타입 **
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
** 설명 **
비균질 자산의 사용 권한을 수정하십시오. 계약 소유자는 지정된 비균질 토큰 프록시 권한을 가지고 있거나 소유권과 사용 권한을 모두 가지고 있어야합니다.
** 매개 변수 **
beneficiary_account : 균질하지 않은 토큰을 사용할 권리가 부여 된 계정 이름 또는 계정 ID
token_hash_or_id : 지정된 비균질 토큰 해시 값 또는 ID
enable_logger : 계약 결과에 관련 영향이 기록되는지 식별

** 4.14. transfer_nht_active_from_caller **

** 프로토 타입 **
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
** 설명 **
계약 호출자로부터 비균질 토큰의 사용 권한을 이전하십시오. 호출자는 지정된 비균질 토큰 프록시 권한 또는 소유권과 사용 권한을 모두 가지고 있어야합니다.
** 매개 변수 **
to : 균질하지 않은 토큰을 사용할 권리가 부여 될 계정 이름 또는 계정 ID
token_hash_or_id : 지정된 비균질 토큰 해시 값 또는 ID
enable_logger : 계약 결과에 관련 영향이 기록되는지 식별

** 4.15. transfer_nht_authority_from_owner **

** 프로토 타입 **
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
** 설명 **
계약 소유자로부터 동종이 아닌 토큰 프록시 제어를 이전하십시오. 계약 소유자에게는 지정된 동종이 아닌 토큰 프록시 권한이 있어야합니다.
** 매개 변수 **
to : 동종이 아닌 토큰에 대한 프록시 제어에 할당 될 계정 이름 또는 계정 ID
token_hash_or_id : 지정된 비균질 토큰 해시 값 또는 ID
enable_logger : 계약 결과에 관련 영향이 기록되는지 식별

** 4.16. transfer_nht_authority_from_caller **

** 프로토 타입 **
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
** 설명 **
계약 소유자로부터 동종이 아닌 토큰 프록시 제어를 전송하십시오. 호출자는 지정된 동종이 아닌 토큰 프록시 권한을 가져야합니다.
** 매개 변수 **
to : 동종이 아닌 토큰에 대한 프록시 제어에 할당 될 계정 이름 또는 계정 ID
token_hash_or_id : 지정된 비균질 토큰 해시 값 또는 ID
enable_logger : 계약 결과에 관련 영향이 기록되는지 식별

** 4.17. set_nht_limit_list **

** 프로토 타입 **
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
** 설명 **
지정된 항목의 확장 필드 (계약 데이터 필드)에 대한 읽기 및 쓰기 권한을 설정하십시오. 호출자는 지정된 비균질 토큰의 소유권과 사용 권한을 가져야합니다.
** 매개 변수 **
token_hash_or_id : 지정된 비균질 토큰 해시 값 또는 ID
contract_name_or_ids : 여러 데이터 필드 (계약)가 ","
limit_type : true의 결과는 지정된 데이터 필드에 쓸 수있는 화이트리스트를 나타냅니다. false는 블랙리스트를 나타내며, 지정된 데이터 필드는 쓸 수 없습니다.
enable_logger : 계약 결과에 관련 영향이 기록되는지 식별

** 4.18. relate_nh_asset **

** 프로토 타입 **
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
** 설명 **
두 개의 비균질 자산을 연결하십시오.
** 매개 변수 **
parent_token_hash_or_id : 지정된 상위 비 동종 자산의 해시 또는 ID
child_token_hash_or_id : 지정된 하위 비 동질 자산의 해시 또는 ID
관련 : 관련 여부
enable_logger : 계약 결과에 관련 영향이 기록되는지 식별

** 4.19. 랜덤 **

** 프로토 타입 **
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
**설명*
Generate an internal random number. 
**반환값**
Radom number result

**4.20. is_owner**

**프로토타입**
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
** 설명 **
계약 발신자가 계약 주장의 소유자인지 확인하십시오.
** 반환 값 **
결정

** 4.21. nht_describe_change **

** 프로토 타입 **
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
** 설명 **
비균질 토큰의 영역 데이터 설명을 수정하십시오. 계약에 해당하는 영역 만 수정할 수 있습니다.
** 매개 변수 **
token_hash_or_id : 지정된 하위 비 동질 자산의 해시 또는 ID
키 : 영역 데이터의 키 이름
값 : 영역 데이터 키에 해당하는 값
enable_logger : 계약 결과에 관련 영향이 기록되는지 식별

** 4.22. set_permissions_flag **

** 프로토 타입 **
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
** 설명 **
계약 서명 요구 사항을 사용하거나 사용하지 않도록 계약 권한 확인 ID를 설정하십시오. 해당하는 신뢰할 수있는 실행 환경에만 계약 권한이 있습니다. 신뢰할 수있는 실행 환경에서 사용자가 계약을 호출하면 사용자 서명과 계약 서명이 동시에 완료됩니다.
** 매개 변수 **
플래그 : 서명 요구 사항 사용 여부

** 4.23. change_contract_authority **

** 프로토 타입 **
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
** 설명 **
계약 확인 권한 수정
** 계약 확인 권한 수정 **
퍼블릭 키 : 확인 권한에 해당하는 퍼블릭 키

## 5. 스마트 계약 기능

** 5.1. Hello World (로그 출력) **
[block:code]
{
  "codes": [
    {
      "code": "function logtest()\n    chainhelper:log('hello world')\n    chainhelper:log(date('%Y-%m-%dT%H:%M:%S', chainhelper:time()))\nend\n",
      "language": "lua"
    }
  ]
}
[/block]
** 5.2. 체인 시간 얻기 **
[block:code]
{
  "codes": [
    {
      "code": "function timetest() \n    public_data.time=date('%Y-%m-%dT%H:%M:%S', chainhelper:time()) \n    write_list={public_data={time=true}} \n    chainhelper:write_chain() \nend\n\n",
      "language": "lua"
    }
  ]
}
[/block]
**5.3. 전송**
[block:code]
{
  "codes": [
    {
      "code": "function transfer(amount,symbol,islog) \n    chainhelper:transfer_from_caller(contract_base_info.owner,amount,symbol,islog) --Transfer homogenous assets from the contract owner to the account\n    chainhelper:transfer_from_owner(contract_base_info.caller,amount,symbol,islog) --Transfer homogenous assets from the contract owner to the account\nend\n\n\n",
      "language": "lua"
    }
  ]
}
[/block]
**5.4. 자산 동결 구성**
[block:code]
{
  "codes": [
    {
      "code": "function init()\n    assert(chainhelper:is_owner(),'chainhelper:is_owner()')\n    read_list={public_data={is_init=true}}\n    chainhelper:read_chain()\n    assert(public_data.is_init==nil,'public_data.is_init==nil')\n    public_data.locked=0\n    public_data.is_init=true\n    chainhelper:write_chain()\nend\n\nfunction pay_with_lock(amount,symbol)\n    assert(amount>0,'amount > 0')\n    read_list={public_data={}}\n    chainhelper:read_chain()\n    assert(public_data.locked+amount>public_data.locked,'public_data.locked+amount>public_data.locked')\n    public_data.locked=public_data.locked+amount;  --[[Adjust lock record]]\n  assert(public_data.locked<=chainhelper:number_max(),'public_data.locked<=chainhelper:number_max()')\n    chainhelper:transfer_from_caller(contract_base_info.owner,amount,symbol,true)\n--[[Transfer the tokens in]]\n    chainhelper:adjust_lock_asset(symbol,amount)  --[[Lock the tokens]]\n    write_list=read_list\n    chainhelper:write_chain()\nend    \n\nfunction adjustment_lock_and_transfer(to,amount,symbol)\n    assert(chainhelper:is_owner(),'chainhelper:is_owner()')\n    read_list={public_data={}}\n    chainhelper:read_chain()\n    assert(amount > 0 and public_data.locked – amount >= 0, 'amount>0 and public_data.locked-amount>=0')\n    public_data.locked=public_data.locked-amount  --[[Adjust lock record]]\n    chainhelper:adjust_lock_asset(symbol,-amount)      --[[Unlock the tokens]]\n    if(to~=contract_base_info.owner)then\n        chainhelper:transfer_from_owner(to,amount,symbol,true)  --[[Transfer the tokens out]]\n    end\n    write_list=read_list\n    chainhelper:write_chain()\nend\n\n\n\n",
      "language": "lua"
    }
  ]
}
[/block]
**5.5. 해시 생성/인증**
[block:code]
{
  "codes": [
    {
      "code": "function set_hash(source) \n    public_data.hash256=chainhelper:hash256(source) \n    public_data.hash512=chainhelper:hash512(source) \n    chainhelper:write_chain() --Default: write_list={public_data={},private_data={}}, update all data, this contract has two data of hash256 and hash512 \nend \nfunction check_hash(source) \n    chainhelper:read_chain() --Default: read_list={public_data={},private_data={}}, load all data, this contract has two data of hash256 and hash512 \n    assert(public_data.hash256==chainhelper:hash256(source),'hash256 check error') \n    assert(public_data.hash512==chainhelper:hash512(source),'hash512 check error') \nend\n\n\n",
      "language": "lua"
    }
  ]
}
[/block]
**5.6. 대체 불가능한 자산의 설명 자료 수정**
[block:code]
{
  "codes": [
    {
      "code": "--Modify non-homogeneous asset descriptions with json strings\nfunction my_nht_describe_change( nht_hash_or_id,values_json) \n    local values=cjson.decode(values_json) \n    for key,value in pairs(values)  do  \n        chainhelper:log('key:'..key..',value:'..value)   \n        chainhelper:nht_describe_change( nht_hash_or_id,key,value,true)  \n    end  \nend\n\n--Modify non-homogeneous asset descriptions in lua form\nfunction nht_change_with_table( nht_hash_or_id,values_table) \n    for key,value in pairs(values_table)  do  \n        chainhelper:log('key:'..key..',value:'..value)   \n        chainhelper:nht_describe_change( nht_hash_or_id,key,value,true)  \n    end  \nend",
      "language": "lua"
    }
  ]
}
[/block]
**5.7. 랜덤 기능의 예시**
[block:code]
{
  "codes": [
    {
      "code": "--This example is a function of accumulating 10 randomness and outputting the result.\nfunction sum_public_by_rand()\n    read_list={public_data={sum_rand_10=true}}\nchainhelper:read_chain()\n--Interface caller permissions can be qualified by assertion in combination with the is_owner function\n    assert(chainhelper:is_owner(),'You`re not the contract`s owner')\n    local i=0\n    while(i<10)do\n        i=i+1\n        if(public_data.sum_rand_10==nil)then\n            public_data.sum_rand_10=0\n            public_data.sum_rand_10=public_data.sum_rand_10+chainhelper:random()%100\n--The value of % after random() is the range of values that need to be random. For example, the random result in this example is 0~99.\n        else\n            public_data.sum_rand_10=public_data.sum_rand_10+chainhelper:random()%100\n        end\n    end\n    write_list={public_data={sum_rand_10=true}}\n    chainhelper:write_chain()\n    chainhelper:log('date:'..date('%Y-%m-%dT%H:%M:%S', chainhelper:time())..',sum:'..public_data.sum_rand_10) end\nend\n\n\n",
      "language": "lua"
    }
  ]
}
[/block]
**5.8. 배팅 게임**
[block:code]
{
  "codes": [
    {
      "code": "--Set prize pool\nfunction set_ticket(ticket)                \n  assert(chainhelper:is_owner(),'You`re not the contract`s owner')            \n  read_list={public_data={ticket_pool_1=true,ticket_pool_2=true}}  \n  chainhelper:read_chain()  \n  if(public_data.ticket_pool_1==nil)then \n      public_data.ticket_pool_1={}  \n    public_data.ticket_pool_2={}  \n    if (public_data.ticket_pool_1[ticket]==nil) then            \n        public_data.ticket_pool_2[#public_data.ticket_pool_2+1]=ticket  \n        public_data.ticket_pool_1[ticket]=#public_data.ticket_pool_2  \n    end     \n  else\n    if (public_data.ticket_pool_1[ticket]==nil) then  \n        public_data.ticket_pool_2[#public_data.ticket_pool_2+1]=ticket  \n        public_data.ticket_pool_1[ticket]=#public_data.ticket_pool_2  \n    end     \n  end\n  assert(#public_data.ticket_pool_2<=12)\n  write_list={public_data={ticket_pool_1={[ticket]=true},ticket_pool_2={[#public_data.ticket_pool_2]=true}}}  \n  chainhelper:write_chain()  \n  end\n\n--Draw a lottery\nfunction luck_draw(ticket,amount,asset)  \n  assert(amount>=1000000,'amount should not be less than 1000000')  \n  assert(asset=='COCOS','asset error')  \n  read_list={public_data={ticket_pool_1=true,ticket_pool_2=true}}  \n  chainhelper:read_chain()      \n  local total=chainhelper:get_account_balance(contract_base_info.owner,asset)      \n  assert((#public_data.ticket_pool_2)*amount<=total,'Current maximum compensation ratio:'..#public_data.ticket_pool_2..'The biggest bet at present:'..total/(#public_data.ticket_pool_2))  \n  chainhelper:transfer_from_caller(contract_base_info.owner,amount,asset,true)  \n  local index=chainhelper:random()%(#public_data.ticket_pool_2)+1      \n  local rate = chainhelper:random()%(#public_data.ticket_pool_2)+1\n  chainhelper:log('luck:'..public_data.ticket_pool_2[index]..',rate:'..rate)\n  if(public_data.ticket_pool_2[index]==ticket)then  \n    chainhelper:transfer_from_owner(contract_base_info.caller,rate*amount,asset,true)      \n  end\n end\n --Reset the prize pool\nfunction reset_ticket() \n    write_list_list={public_data={ticket_pool_1=false,ticket_pool_2=false}}\n    chainhelper:write_chain()\nend \n\n\n",
      "language": "lua"
    }
  ]
}
[/block]
**5.9. 예제 1: set the prize pool**
[block:code]
{
  "codes": [
    {
      "code": "function set_ticket(ticket)\nassert(is_owner(),'You`re not the contract`s owner')\n    if(public_data.ticket_pool_1==nil)then\n        public_data.ticket_pool_1={}\n        public_data.ticket_pool_2={}\n        if (public_data.ticket_pool_1[ticket]==nil) then\n            public_data.ticket_pool_2[#public_data.ticket_pool_2+1]=ticket --Note: the lua array subscript starts with 1\n            public_data.ticket_pool_1[ticket]=#public_data.ticket_pool_2\n        end\n    else\n        if (public_data.ticket_pool_1[ticket]==nil) then\n            public_data.ticket_pool_2[#public_data.ticket_pool_2+1]=ticket\n            public_data.ticket_pool_1[ticket]=#public_data.ticket_pool_2\n        end\n    end\nend\n--Lottery, ticket: lots, amount: token amount，asset: token type\nfunction luck_draw(ticket,amount,asset)\n    assert(amount>=1000000,'amount should not be less than 1000000')\n    assert(asset=='COCOS','asset error')\nlocal total=get_account_balance(contract_base_info.owner,asset)\nassert((#public_data.ticket_pool_2)*amount<=total,'Current maximum compensation ratio:'..#public_data.ticket_pool_2..'The biggest bet at present:'..total/(#public_data.ticket_pool_2))\n    transfer_from_caller(contract_base_info.owner,amount,asset,true)\n    local index=random()%(#public_data.ticket_pool_2)+1  --Note: the lua array subscript starts with 1\nlocal rate=0\n    if(public_data.ticket_pool_2[index]==ticket)then\n        while(true)do\nrate =random()%(#public_data.ticket_pool_2)\nif(rate*amount<=total) then\ntransfer_from_owner(contract_base_info.caller,rate*amount,asset,true)\nbreak\nend\nend\n    end\nlog('ticket:'..public_data.ticket_pool_2[index]..',rate:'..rate)\nend\n--Random accumulation function for verifying random numbers on the chain (for testing)\nfunction sum_public_by_rand()\nassert(is_owner(),'You`re not the contract`s owner')\n    local i=0\n    while(i<10)do\n    i=i+1\n        if(public_data.sum_rand_10==nil)then\n            public_data.sum_rand_10=0\n          public_data.sum_rand_10=public_data.sum_rand_10+random()%100\n        else\n            public_data.sum_rand_10=public_data.sum_rand_10+random()%100\n        end\n    end\nend\n\n\n",
      "language": "lua"
    }
  ]
}
[/block]
**5.10. 예제 2: Modify the contract-related description of the non-homogeneous token, and the part to be modified is the ​corresponding area of the contract.**
[block:code]
{
  "codes": [
    {
      "code": "function my_nht_describe_change( nht_hash_or_id,change_values_json)\nlocal change_values=cjson.decode(change_values_json)--Note: here is the use of the cjson module\nfor key,value in pairs(change_values) do--Note: traversal of lua table, distinguishing between ipairs and pairs\nlog('key:'..key..',value:'..value)\nnht_describe_change( nht_hash_or_id,key,value,true)\nend\nend\n//nht_hash_or_id：Non-homogeneous token hash or id\n//change_values_json：Specified modification content in json format for batch modification\nModify contract verification permissions\n\nfunction my_change_contract_authority(publickey)\nassert(is_owner(),'You`re not the contract`s owner')\n    change_contract_authority(publickey)\nend\n--Set contract authority verification ID to enable or disable contract signing requirements. Only the corresponding trusted execution environment has contract authority.\n\nfunction set_permissions_flag(flag)\n    assert(is_owner(),'You`re not the contract`s owner')\n    set_permissions_flag(flag)\nend\n--Encrypted data constructor\nfunction my_make_memo(to,key,value) make_memo(to,key,value,true) end\n\n\n",
      "language": "lua"
    }
  ]
}
[/block]