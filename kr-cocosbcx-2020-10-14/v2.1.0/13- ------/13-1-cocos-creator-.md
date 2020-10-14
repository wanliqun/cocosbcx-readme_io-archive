---
title: "13.1 Cocos Creator 플러그인"
slug: "13-1-cocos-creator-"
hidden: false
createdAt: "2019-08-26T04:48:34.428Z"
updatedAt: "2019-08-26T05:02:01.772Z"
---
## Cocos Creator 소개
Cocos Creator(https://www.cocos.com/creator) 는 완전히 스크립트화되고 구성 요소화 된 데이터 중심의 기능을 갖춘 Cocos2d-x 기반 게임 개발 도구이며 콘텐츠 제작에 중점을 둡니다.

Cocos2d-x는 오픈 소스 프레임 워크인 Cocos2d-x를 기반으로 확장 가능하고 사용자 정의 가능한 일체형 워크플로 편집기를 구현하고 처음으로 Cocos 제품군으로 구성 요소화된 프로그래밍 아이디어와 데이터 중심 아키텍처 설계를 소개합니다. Cocos2d-x 개발 워크 플로우에서 장면 편집, UI 디자인, 리소스 관리, 게임 디버깅 및 미리보기, 멀티 플랫폼 게시와 같은 작업을 단순화하므로 Cocos2d-x를 사용하는 팀 협업 개발에 적합합니다.

## 프로젝트 구조
Cocos-BCX는 Github에 플러그인을 오픈 소스로 제공하고 있습니다. 자세한 정보는 Cocos-BCX For Cocos Creator(https://github.com/Cocos-BCX/bcx-sdk-creator) 입니다. BCX For Cocos Creator 플러그인 및 Cocos Creator에서 BCX를 연결하는 샘플 프로젝트가 사용자에게 제공됩니다.
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/8869a2d-617af9f-Cocos-BCX.png",
        "617af9f-Cocos-BCX.png",
        294,
        254,
        "#3f2f30"
      ]
    }
  ]
}
[/block]
BCX: BCX For Cocos Creator의 플러그인 패키지 (폴더는 프로젝트 패키지에 설치 한 후 사용 가능합니다.)

샘플: BCX를 호출하는 기본 방법이 포함 된 프로젝트.

## 필수 버전
CocosCreator 2.0 이상

## 설치

BCX 폴더를 Creator 프로젝트의 패키지 디렉토리로 옮깁니다.
   * 설치 후 Creator 메뉴에 다음 메뉴가 표시됩니다.
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/405960a-c49fd2e-bcx_menu_1.jpeg",
        "c49fd2e-bcx_menu (1).jpeg",
        279,
        110,
        "#798391"
      ]
    }
  ]
}
[/block]
* 설치 버튼을 클릭하면 자산 메뉴가 BCX 폴더를 새로 생성합니다.
* 프로젝트를 종료하고 다시 열면 BCX 폴더가 자산 메뉴에 있어야합니다.
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/f6b2cd2-64d8c40-bcx_assets.png",
        "64d8c40-bcx_assets.png",
        414,
        658,
        "#38383a"
      ]
    }
  ]
}
[/block]
* BCX 관련 인터페이스는 사용자 자신의 코드로 호출 할 수 있습니다.

## 샘플 명령

* Mac 사용자의 경우 CocosCreator 2.0 이상에서 sample / bcx-creator를 열고 실행하십시오.
* Windows 사용자의 경우 sample / bcx-creator / packages / bcx를 삭제하고 프로젝트 루트 디렉토리의 BCX 파일을 sample / bcx-creator / packages /에 복사 한 다음 CocosCreator 2.0 이상에서 실행하십시오.

## 해당 버전
[block:parameters]
{
  "data": {
    "h-0": "BCX For Creator",
    "h-1": "BCX JS SDK",
    "0-0": "0.0.1",
    "0-1": "1.3.0.2"
  },
  "cols": 2,
  "rows": 1
}
[/block]
위에서 명시된 바와 같이 BCX For Creator 0.0.1은 BCX JS SDK 1.3.0.2를 기반으로 생성됩니다.