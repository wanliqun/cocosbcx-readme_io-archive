---
title: "8.3 Cocos터미널과 계약 구현"
slug: "8-3-cocos-"
excerpt: "Cocos Terminal adds Contract Manage function in Toolkits for​ developers to create, update contracts, and execute contract interfaces directly."
hidden: false
createdAt: "2019-08-26T04:48:34.439Z"
updatedAt: "2019-08-27T02:01:19.571Z"
---
# Contract 개발

##  1. 소개
a. 로그인 링크 [Terminal](http://cocos-terminal.com)
b. 왼쪽 디렉토리 표시 줄에서 계약 관리를 클릭하여 아래에 표시된대로 계약, 코드, 인터페이스, 데이터 영역 (public_data) 등의 기본 정보등을 포함하여 본 계정에 존재하는 다양한 계약 정보를 확인 할 수 있습니다.
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/af24778-1.png",
        "1.png",
        1920,
        902,
        "#2b2d2f"
      ]
    }
  ]
}
[/block]
## 2. 계약 생성
a. 새로운 계약 생성을 클릭 
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/3119512-2.png",
        "2.png",
        1920,
        902,
        "#2c2d2f"
      ]
    }
  ]
}
[/block]
b. 팝업 창에 계약 이름을 입력하세요. 계약 이름은 소문자 또는 숫자로 구성되는 4 ~ 63 자 범위 내여야하며 "contract.testnew"와 같이 "contract"로 시작합니다.
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/b9411b5-3.png",
        "3.png",
        538,
        259,
        "#50555c"
      ]
    }
  ]
}
[/block]
## 3. 계약코드 수정과 기존 계약 업데이트
[block:code]
{
  "codes": [
    {
      "code": "function hello()\n    chainhelper:log('Hello World! contract.testnew')\nend",
      "language": "lua"
    }
  ]
}
[/block]
## 4. 계약 배포
a. 배포 클릭
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/4cbc546-4.png",
        "4.png",
        1237,
        569,
        "#242425"
      ]
    }
  ]
}
[/block]
b. 랜덤 생성을 클릭하십시오. 계약이 권한 유효성 검증을 여는 경우 JS-SDK의 app_keys 구성 항목을 키로 채워야합니다. 키를 복사하여 저장하는 것이 좋습니다.
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/3d0246d-5.png",
        "5.png",
        940,
        507,
        "#494b51"
      ]
    }
  ]
}
[/block]
c. OK를 클릭하세요. 계약생성에는 특정 수수료가 발생합니다. 
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/def7ca8-6.png",
        "6.png",
        804,
        418,
        "#383d44"
      ]
    }
  ]
}
[/block]
## 5. 계약 호출
a. 계약이 릴리스되면 아래 그림의 화살표로 지시된 계약의 인터페이스를 찾을 수 있습니다. 인터페이스를 클릭하여 인터페이스를 실행할 매개 변수를 채웁니다.
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/8bbb501-7.png",
        "7.png",
        1397,
        544,
        "#262626"
      ]
    }
  ]
}
[/block]
b. 계약을 호출하는데 수수료가 발생합니다. 
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/035240b-8.png",
        "8.png",
        1103,
        637,
        "#2b2e33"
      ]
    }
  ]
}
[/block]
c. 호출 결과가 편집 영역 아래에 표시됩니다.
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/6723626-9.png",
        "9.png",
        1165,
        711,
        "#212121"
      ]
    }
  ]
}
[/block]
## 6. 계약 업데이트
a. init_data () 사용하여 데이터를 초기화 하십시오
[block:code]
{
  "codes": [
    {
      "code": "function hello()\n    chainhelper:log('Hello World! contract.testnew')\nend\n\nfunction hello2(num,amount)\n\tchainhelper:log('=======loooooog starts=======');\n\tchainhelper:log('{\"num\": \"'..num..'\",\"amount\":\"'..amount..'\"}');\n\tchainhelper:log('=======log ends=======');\nend\n\nfunction init_data()\n    read_list = {public_data={initdata=true}}\n    chainhelper:read_chain()\n    public_data.initdata  = 98\n    write_list = {public_data={initdata=true}}\n    chainhelper:write_chain()\nend",
      "language": "lua"
    }
  ]
}
[/block]
b. 계약 해제를 클릭하십시오 (기존 계약이 최신으로 업데이트 됨). 릴리스가 완료된 후 init_data () 인터페이스를 호출하여 데이터를 초기화해야합니다.
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/fc60e00-10.png",
        "10.png",
        1119,
        567,
        "#2a2e32"
      ]
    }
  ]
}
[/block]
c. Data텝을 클릭하여 데이터를 초기화 하십시오
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/7a1db29-11.png",
        "11.png",
        1435,
        621,
        "#252627"
      ]
    }
  ]
}
[/block]
## 7. 계약 보기
검색 상자에 계약 이름을 입력하여 계약 정보 및 통계를 볼 수도 있습니다.

a. 계약의 기본 정보 보기
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/c99f5cc-12.png",
        "12.png",
        1662,
        705,
        "#404349"
      ]
    }
  ]
}
[/block]
b. 계약 통계. 계약 호출 수, 전송 및 전송된 토큰 수를 포함한 운영 데이터를 편리하게 확인 할 수 있습니다.
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/07f5d63-13.png",
        "13.png",
        1659,
        818,
        "#34383e"
      ]
    }
  ]
}
[/block]
#계약 통계 
a. 인기 계약의 순위는 터미널에서도 제공되므로 계약 호출 수를 명확하게 볼 수 있을뿐만 아니라 계약 세부 사항과 계약의 실행 결과를 빠르게 볼 수 있습니다.
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/b549696-14.png",
        "14.png",
        1920,
        902,
        "#34393f"
      ]
    }
  ]
}
[/block]
b.  Contract을 클릭하여 계약 코드, 데이터 및 통계를보십시오.
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/5bf72db-15.png",
        "15.png",
        1907,
        850,
        "#31353b"
      ]
    }
  ]
}
[/block]