---
title: "7.1 JS-SDK"
slug: "7-1-js-sdk"
excerpt: "COCOS-BCX RPC API를 사용하여 COCOS-BCX기반 블록 체인과 통합하기위한 Javascript API 정보"
hidden: false
createdAt: "2019-08-26T04:48:34.432Z"
updatedAt: "2019-09-19T11:56:20.670Z"
---
## Class Library Reference
**API files 소개**
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

**class library 객체 인스턴트화**
[block:code]
{
  "codes": [
    {
      "code": "var bcx=new BCX({\n            default_ws_node:”ws://XXXXXXXXX” //node rpc address, optional. If you do not specify this, it will automatically connect to the fastest node in ws_node_list\n            ws_node_list:[{url:\"ws://xxxxxxx\",name:\"xxxxx\"}]//API server node list, required\n            faucet_url:\"http://xxx.xxx.xxx.xxx:xxxx\", //Registration\n            networks:[{\n                core_asset:\"xxx\",//core asset symbol\n                chain_id:\"xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx\"//chain id   \n            }], \n            auto_reconnect:false,//Whether to connect automatically when RPC is disconnected, the default is true\n            app_keys:[\"xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx\"]//Contract authorization. Do not need to configure this if there is no contract authorization.\n\t })",
      "language": "javascript"
    }
  ]
}
[/block]
**호출-전송 인스턴트** 
[block:code]
{
  "codes": [
    {
      "code": "bcx.transferAsset({\n            fromAccount: 'test1',\n            toAccount: 'test2',\n            amount: amount,\n            assetId: 'COCOS',\n            feeAssetId: 'COCOS',\n            memo: memo,\n            onlyGetFee: false,\n        }).then(function (res) {\n             console.log('transferAsset res',res);\n        })",
      "language": "javascript"
    }
  ]
}
[/block]
## API 사용자 가이드
1. 달리 지정하지 않는 한 하나의 선택적 매개 변수 콜백이 있습니다. 콜백에 의해 리턴된 결과는 {code : 0, message : ""} 구조 객체입니다. code=1인 경우는 결과가 성공했으며 메시지 상태 설명은 없음을 의미합니다. Code!=1인 경우는 결과가 실패했음을 나타내며 메시지는 실패 상태에 대한 설명입니다.
2. 달리 명시되지 않는 한 하나의 매개 변수만 있습니다. 매개 변수는 콜백을 포함하여 모든 관련 매개 변수를 포함하는 객체입니다.
예시:
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
3. 서브 스크립션 인터페이스 외에도 다른 인터페이스는 콜백 매개 변수를 전달하지 않으면 지정된 객체를 반환합니다.
4. 인터페이스의 매개 변수 유형은 달리 지정되지 않는 한 문자열입니다.
5. 인터페이스의 매개 변수는 달리 지정하지 않으면 비워 둘 수 없습니다. 콜백은 선택적 매개 변수입니다.
6. 검색 인터페이스는 데이터 인스턴스를 반환합니다 : {code : 1, data : []}
7. 다른 인터페이스에서 리턴 한 데이터에는 하나의 오브젝트 값을 갖는 추가 데이터 필드 trxData에 있습니다.
예시:
[block:code]
{
  "codes": [
    {
      "code": "trx_data:{\n block_num:*****,//Block height\n trx_id:\"************************\"//Transaction ID\n}",
      "language": "javascript"
    }
  ]
}
[/block]
8. 비-쿼리 인터페이스에 관련 ID 비즈니스 (예 : NH 자산을 생성하여 생성된 ID)가 포함된 경우 반환되는 데이터에 데이터 개체가 포함됩니다.
예시:
[block:code]
{
  "codes": [
    {
      "code": "data:{\n  real_running_time: 387//Running time\n  result: \"4.2.288\"//Associated business id\n}",
      "language": "javascript"
    }
  ]
}
[/block]
## 상태 코드
**설명** 
[block:parameters]
{
  "data": {
    "0-0": "300",
    "0-1": "Chain sync error, please check your system clock",
    "h-0": "코드",
    "h-1": "메세지",
    "h-2": "설명",
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
    "9-0": "105",
    "8-1": "XX not found",
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
    "31-1": "Parameter ‘memo’ can not be empty\tmemo",
    "32-0": "130",
    "32-1": "Please enter the correct contract name(/^a-z{4,63}$/)",
    "33-0": "131",
    "33-1": "Parameter ‘worldView’ can not be empty",
    "34-0": "133",
    "34-1": "Parameter ‘toAccount’ can not be empty\ttoAccount",
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
## 프로젝트
CocosBCXWallet

## 오픈소스 링크주소
https://github.com/Cocos-BCX/JSSDK