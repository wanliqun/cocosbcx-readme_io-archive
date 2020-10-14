---
title: "5.5 合约api"
slug: "55-contractapi"
hidden: false
createdAt: "2019-06-20T03:33:26.536Z"
updatedAt: "2020-06-04T03:47:57.148Z"
---
##1. 使用须知
Cocos-BCX 智能合约采用 Lua 语言编写，在官方5.3版本进行修改，语法上全部保留。新增链内操作函数并调整了函数库，使其更适应在链环境下的运行。

**1.1. 基本概念**
**合约数据**
合约数据分为用户数据区和公共数据区
◆	用户数据区：用于存放用户调用合约后产生的数据，用户数据区由合约编写者自定义；
◆	公共数据区：用于存放合约的规则性数据，合约编写者可使用owner断言(即：assert(is_owner()))限定调用者。公共数据区由public_data数据表记录，所以编写者应注意将公共数据放入public_data对象；

**特殊对象**
◆	public_data
用于记录公共数据区，对象属性由合约编写者定义；
◆	private_data
用户数据区指向本次合约调用者；
◆	read_list
合约数据IO的读操作注册表，合约可以通过编写read_list表通知合约需要载入的上下文，默认状态：read_list={public_data={},private_data={}}，默认加载public_data、private_data分区的所有数据；
read_list={public_data={test=true}},只读取public_data.test数据，在执行read_chain()函数时生效；
◆	write_list
合约数据IO的写操作注册表，合约可以通过编写write_list表通知合约需要被链记录的上下文，默认状态：read_list={public_data={},private_data={}}，默认记录public_data、private_data分区的所有数据；
write_list={public_data={test=true}},只写入public_data.test数据，在执行write_chain()函数时生效，write_list每条路径的值(true/false):true:表示若存在则更新，不存在则创建，false表示：若存在则清除；
◆	contract_base_info
用于存放合约的基本信息，若在合约内修改该对象将不会被记录，对象属性：name（合约名字）、id（合约id）、owner（合约拥有者id）、caller（当前呼叫者id）、creation_date（合约编写时间）、contract_authority（合约要求授权签名）；

##1.2. 注意事项
**合约会话恢复机制不包含运行时代码的恢复**
即：lambda表达式仅在当前函数上下文有效，包含table和metatable的动态属性函数；
**统一合约应用层table数据结构，停用metatable**
原因：
◆	metatable中常见lambda函数的使用，而运行时代码无法恢复；
◆	metatable数据结构IO速度与table数据结构相比较慢


## 2. 基础模块和基础模块扩展
**2.1. 基础模块**
可根据0号合约的配置，控制合约沙箱对基础模块的支持，后期0号基础支撑合约将由理事会管理
**2.2. 基础模块扩展**
**2.2.1. CJSON模块**
CJSON模块，常用于解析传入的函数结构化参数。
目前合约ABI已经接受外部table数据结构的参数，但继续保留CJSON模块以便以字符串的方式传入对象以及对象的序列化。
调用方式：
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
## 3. 合约链交互模块——静态函数
链交互模块的静态函数可在合约内直接以函数名调用
**get_account_contract_data**

**原型**
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
**说明**
读取指定用户对应路径的用户数据
**返回值**
返回一个table结构的用户数据，如没有路径中指定的某一条数据则对应的table分支为空；
**例**
nico_data=get_account_contract_data('nicotest',{nicodata0={nicodata1=true}) 
意图读取nicotest账户在本合约中的nicodata0.nicodata1数据，如nicotest为合约呼叫者则：nico_data应与private_data.nicodata0.nicodata1 相同。

## 4. 合约链交互模块——动态函数
链交互模块的动态函数需在合约内按照“chainhelper:函数名(参数……)”方式调用。

**4.1. hash256**

**原型**
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
**返回值**
返回hash256字符串
**参数**
source: 需要运算的源数据

**4.2. hash512**

**原型**
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
**返回值**
返回hash512字符串
**参数**
source: 需要运算的源数据

**4.3. create_nh_asset**

**原型**
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
**说明**
创建非同质道具，合约拥有者必须有对应的创建权限。
**参数**
name_or_id:新道具的拥有者
symbol:流通限定同质资产符号(预留)，例COCOS
world_view:世界观
base_describe:基础描述
enable_logger:标识是否在contract result中记录相关影响

**4.4. adjust_lock_asset**

**原型**
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
**说明**
调整合约拥有者在本合约中锁定的资产。
**参数**
symbol_or_id:需要调整的资产ID或符号
amount:带精度的数量可以为负数（意为降低锁定），调整之后的锁定量应大于0小于合约拥有者对应资产的最大额度

**4.5. read_chain**

**原型**
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
**说明**
合约数据IO读操作，与read_list注册表对应。

**4.6. write_chain**

**原型**
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
**说明**
合约数据IO写操作，与write_list注册表对应。

**4.7. get_account_balance**

**原型**
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
**说明**
查询指定账户同质资产余额
**返回值**
余额数值
**参数**
account_name_or_id:需要查询的账户名或者id
asset_symbol_or_id:需要查询的资产符号或者id

**4.8. transfer_from_caller**

**原型**
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
**说明**
从合约调用者转移资产到账户to，数量为:token，代币符号:symbol
**参数**
to:接收账户id
token:数额，应大于0且小于lua number的最大范围
symbol:资产符号
enable_logger: 标识是否在contract result中记录相关影响

**4.9. transfer_from_owner**

**原型**
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
**说明**
从合约调用者转移资产到账户to，数量为:token，代币符号:symbol
**参数**
to:接收账户id
token:数额，应大于0且小于lua number的最大范围
symbol:资产符号
enable_logger: 标识是否在contract result中记录相关影响

**4.10. make_memo**

**原型**
[block:code]
{
  "codes": [
    {
      "code": "void make_memo (string receiver_id_or_name, string key, string value, uint64_t ss, bool enable_logger)",
      "language": "lua"
    }
  ]
}
[/block]
**说明**
加密数据构造函数。
**参数**
receiver_id_or_name: 指定的消息解密人账户id或名称
key: ECC共享秘钥提供的密码种子
value: 加密内容
ss: nonce随机值，和key一起组成密码种子
enable_logger: 标识是否在contract result中记录相关影响

**4.11. transfer_nht_from_caller**

**原型**
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
**说明**
从合约调用者转移非同质资产到账户to
**参数**
to:接收账户id
token_hash_or_id:指定的非同质代币hash值或者id编号
enable_logger: 标识是否在contract result中记录相关影响

**4.12. transfer_nht_from_owner**

**原型**
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
**说明**
从合约拥有者转移非同质资产到账户to
**参数**
to:接收账户id
token_hash_or_id:指定的非同质代币hash值或者id编号
enable_logger: 标识是否在contract result中记录相关影响

**4.13. change_nht_active_by_owner**

**原型**
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
**说明**
修改非同质资产的使用权限，合约拥有者必须具有指定非同质代币代理权限或同时具有拥有权和使用权。
**参数**
beneficiary_account:将被赋予指定非同质代币使用权的账户名或账户ID
token_hash_or_id:指定的非同质代币的hash或id
enable_logger:标识是否在contract result中记录相关影响

**4.14. transfer_nht_active_from_caller**

**原型**
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
**说明**
从合约调用者转移非同质代币使用权，调用者必须具有指定非同质代币代理权限或同时具有拥有权和使用权。
**参数**
to:将被赋予指定非同质代币使用权的账户名或账户ID
token_hash_or_id:指定的非同质代币的hash或id
enable_logger:标识是否在contract result中记录相关影响

**4.15. transfer_nht_authority_from_owner**

**原型**
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
**说明**
从合约拥有者转移非同质代币代理控制权，合约拥有者必须具有指定非同质代币代理权限
**参数**
to:将被赋予指定非同质代币代理控制权的账户名或账户ID
token_hash_or_id:指定的非同质代币的hash或id
enable_logger:标识是否在contract result中记录相关影响

**4.16. transfer_nht_authority_from_caller**

**原型**
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
**说明**
从合约拥有者转移非同质代币代理控制权，调用者必须拥有指定非同质代币代理权限
**参数**
to:将被赋予指定非同质代币代理控制权的账户名或账户ID
token_hash_or_id:指定的非同质代币的hash或id
enable_logger:标识是否在contract result中记录相关影响

**4.17. set_nht_limit_list**

**原型**
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
**说明**
设置指定道具的指定扩展域（合约数据域）的读写权限，调用者者必须具有指定非同质代币的具有拥有权和使用权。
**参数**
token_hash_or_id:指定的非同质代币的hash或id
contract_name_or_ids:多个数据域（合约）使用“,”分割
limit_type:为true时代表白名单，被指定的数据域将允许写入；为false时代表黑名单，被指定的数据域将不允许写入
enable_logger:标识是否在contract result中记录相关影响

**4.18. relate_nh_asset**

**原型**
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
**说明**
将两个非同质资产进行关联。
**参数**
parent_token_hash_or_id:指定的父级非同质资产的hash或id
child_token_hash_or_id :指定的子级非同质资产的hash或id
relate :是否关联
enable_logger:标识是否在contract result中记录相关影响

**4.19. random**

**原型**
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
**说明**
生成内源随机数。
**返回值**
随机数结果

**44.20. is_owner**

**原型**
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
**说明**
判定合约呼叫者是否是owner，可用于合约断言。
**返回值**
判断结果

**4.21. nht_describe_change**

**原型**
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
**说明**
修改非同质代币的域数据描述，只能修改合约对应的域。
**参数**
token_hash_or_id:指定的非同质代币hash值或者id编号
key:域数据键名
value: 域数据键对应值
enable_logger: 标识是否在contract result中记录相关影响

**4.22. set_permissions_flag**

**原型**
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
**说明**
设置合约权限验证标识，以启用或停止合约签名要求。仅有对应的可信执行环境拥有合约权限，在可信执行环境下，用户调用合约时将完成用户签名以及合约签名双重签名。
**参数**
flag: 是否启用签名要求

**4.23. change_contract_authority**

**原型**
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
**说明**
修改合约验证权限
**参数**
publickey:对应验证权限的公钥

##5. 智能合约功能范例

**5.1. Hello World(日志输出)**
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
**5.2. 获取链时间**
[block:code]
{
  "codes": [
    {
      "code": "function timetest() \n    public_data.time=date('%Y-%m-%dT%H:%M:%S', chainhelper:time()) \n    write_list={public_data={time=true}} \n    chainhelper:write_chain() \nend\n",
      "language": "lua"
    }
  ]
}
[/block]
**5.3. 转账**
[block:code]
{
  "codes": [
    {
      "code": "function transfer(amount,symbol,islog) \n    chainhelper:transfer_from_caller(contract_base_info.owner,amount,symbol,islog) --从合约所有者转移同质资产到账户\n    chainhelper:transfer_from_owner(contract_base_info.caller,amount,symbol,islog) --从合约调用者转移同质资产到账户\nend\n",
      "language": "lua"
    }
  ]
}
[/block]
**5.4. 资产锁定配置**
[block:code]
{
  "codes": [
    {
      "code": "function init()\n    assert(chainhelper:is_owner(),'chainhelper:is_owner()')\n    read_list={public_data={is_init=true}}\n    chainhelper:read_chain()\n    assert(public_data.is_init==nil,'public_data.is_init==nil')\n    public_data.locked=0\n    public_data.is_init=true\n    chainhelper:write_chain()\nend\n\nfunction pay_with_lock(amount,symbol)\n    assert(amount>0,'amount > 0')\n    read_list={public_data={}}\n    chainhelper:read_chain()\n    assert(public_data.locked+amount>public_data.locked,'public_data.locked+amount>public_data.locked')\n    public_data.locked=public_data.locked+amount;  --[[调整锁定记录]]\n  assert(public_data.locked<=chainhelper:number_max(),'public_data.locked<=chainhelper:number_max()')\n    chainhelper:transfer_from_caller(contract_base_info.owner,amount,symbol,true)\n--[[转入代币]]\n    chainhelper:adjust_lock_asset(symbol,amount)  --[[锁定代币]]\n    write_list=read_list\n    chainhelper:write_chain()\nend    \n\nfunction adjustment_lock_and_transfer(to,amount,symbol)\n    assert(chainhelper:is_owner(),'chainhelper:is_owner()')\n    read_list={public_data={}}\n    chainhelper:read_chain()\n    assert(amount > 0 and public_data.locked – amount >= 0, 'amount>0 and public_data.locked-amount>=0')\n    public_data.locked=public_data.locked-amount  --[[调整锁定记录]]\n    chainhelper:adjust_lock_asset(symbol,-amount)      --[[解锁代币]]\n    if(to~=contract_base_info.owner)then\n        chainhelper:transfer_from_owner(to,amount,symbol,true)  --[[转出代币]]\n    end\n    write_list=read_list\n    chainhelper:write_chain()\nend\n\n",
      "language": "lua"
    }
  ]
}
[/block]
**5.5. 生成/校验哈希**
[block:code]
{
  "codes": [
    {
      "code": "function set_hash(source) \n    public_data.hash256=chainhelper:hash256(source) \n    public_data.hash512=chainhelper:hash512(source) \n    chainhelper:write_chain() --默认：write_list={public_data={},private_data={}} ,更新全部数据 ，本合约仅有hash256，跟hash512两个数据 \nend \nfunction check_hash(source) \n    chainhelper:read_chain() --默认：read_list={public_data={},private_data={}} ,载入全部数据，本合约仅有hash256，跟hash512两个数据 \n    assert(public_data.hash256==chainhelper:hash256(source),'hash256 check error') \n    assert(public_data.hash512==chainhelper:hash512(source),'hash512 check error') \nend\n",
      "language": "lua"
    }
  ]
}
[/block]
**5.6. 非同质资产描述数据修改**
[block:code]
{
  "codes": [
    {
      "code": "--以json字符串修改非同质资产描述\nfunction my_nht_describe_change( nht_hash_or_id,values_json) \n    local values=cjson.decode(values_json) \n    for key,value in pairs(values)  do  \n        chainhelper:log('key:'..key..',value:'..value)   \n        chainhelper:nht_describe_change( nht_hash_or_id,key,value,true)  \n    end  \nend\n\n--以lua表格方式修改非同质资产描述\nfunction nht_change_with_table( nht_hash_or_id,values_table) \n    for key,value in pairs(values_table)  do  \n        chainhelper:log('key:'..key..',value:'..value)   \n        chainhelper:nht_describe_change( nht_hash_or_id,key,value,true)  \n    end  \nend",
      "language": "lua"
    }
  ]
}
[/block]
**5.7. 随机函数范例**
[block:code]
{
  "codes": [
    {
      "code": "--此随机数范例为一个10次随机累加并输出结果的函数\nfunction sum_public_by_rand()\n    read_list={public_data={sum_rand_10=true}}\nchainhelper:read_chain()\n--可以通过断言方式结合is_owner函数限定接口调用者权限\n    assert(chainhelper:is_owner(),'You`re not the contract`s owner')\n    local i=0\n    while(i<10)do\n        i=i+1\n        if(public_data.sum_rand_10==nil)then\n            public_data.sum_rand_10=0\n            public_data.sum_rand_10=public_data.sum_rand_10+chainhelper:random()%100\n--random()后取%的数值即为需要随机的数值范围，例如本例中随机结果为0~99\n        else\n            public_data.sum_rand_10=public_data.sum_rand_10+chainhelper:random()%100\n        end\n    end\n    write_list={public_data={sum_rand_10=true}}\n    chainhelper:write_chain()\n    chainhelper:log('date:'..date('%Y-%m-%dT%H:%M:%S', chainhelper:time())..',sum:'..public_data.sum_rand_10) end\nend\n",
      "language": "lua"
    }
  ]
}
[/block]
**5.8. 抽奖游戏范例**
[block:code]
{
  "codes": [
    {
      "code": "--设置奖池\nfunction set_ticket(ticket)                \n  assert(chainhelper:is_owner(),'You`re not the contract`s owner')            \n  read_list={public_data={ticket_pool_1=true,ticket_pool_2=true}}  \n  chainhelper:read_chain()  \n  if(public_data.ticket_pool_1==nil)then \n      public_data.ticket_pool_1={}  \n    public_data.ticket_pool_2={}  \n    if (public_data.ticket_pool_1[ticket]==nil) then            \n        public_data.ticket_pool_2[#public_data.ticket_pool_2+1]=ticket  \n        public_data.ticket_pool_1[ticket]=#public_data.ticket_pool_2  \n    end     \n  else\n    if (public_data.ticket_pool_1[ticket]==nil) then  \n        public_data.ticket_pool_2[#public_data.ticket_pool_2+1]=ticket  \n        public_data.ticket_pool_1[ticket]=#public_data.ticket_pool_2  \n    end     \n  end\n  assert(#public_data.ticket_pool_2<=12)\n  write_list={public_data={ticket_pool_1={[ticket]=true},ticket_pool_2={[#public_data.ticket_pool_2]=true}}}  \n  chainhelper:write_chain()  \n  end\n\n--进行抽奖\nfunction luck_draw(ticket,amount,asset)  \n  assert(amount>=1000000,'amount should not be less than 1000000')  \n  assert(asset=='COCOS','asset error')  \n  read_list={public_data={ticket_pool_1=true,ticket_pool_2=true}}  \n  chainhelper:read_chain()      \n  local total=chainhelper:get_account_balance(contract_base_info.owner,asset)      \n  assert((#public_data.ticket_pool_2)*amount<=total,'Current maximum compensation ratio:'..#public_data.ticket_pool_2..'The biggest bet at present:'..total/(#public_data.ticket_pool_2))  \n  chainhelper:transfer_from_caller(contract_base_info.owner,amount,asset,true)  \n  local index=chainhelper:random()%(#public_data.ticket_pool_2)+1      \n  local rate = chainhelper:random()%(#public_data.ticket_pool_2)+1\n  chainhelper:log('luck:'..public_data.ticket_pool_2[index]..',rate:'..rate)\n  if(public_data.ticket_pool_2[index]==ticket)then  \n    chainhelper:transfer_from_owner(contract_base_info.caller,rate*amount,asset,true)      \n  end\n end\n --重置奖池\nfunction reset_ticket() \n    write_list_list={public_data={ticket_pool_1=false,ticket_pool_2=false}}\n    chainhelper:write_chain()\nend \n",
      "language": "lua"
    }
  ]
}
[/block]
**5.9. 综合示例一：设置奖票池**
[block:code]
{
  "codes": [
    {
      "code": "function set_ticket(ticket)\nassert(is_owner(),'You`re not the contract`s owner')\n    if(public_data.ticket_pool_1==nil)then\n        public_data.ticket_pool_1={}\n        public_data.ticket_pool_2={}\n        if (public_data.ticket_pool_1[ticket]==nil) then\n            public_data.ticket_pool_2[#public_data.ticket_pool_2+1]=ticket --注意：lua数组下标以1开始\n            public_data.ticket_pool_1[ticket]=#public_data.ticket_pool_2\n        end\n    else\n        if (public_data.ticket_pool_1[ticket]==nil) then\n            public_data.ticket_pool_2[#public_data.ticket_pool_2+1]=ticket\n            public_data.ticket_pool_1[ticket]=#public_data.ticket_pool_2\n        end\n    end\nend\n--抽奖，ticket：奖票，amount：代币数量，asset：代币种类\nfunction luck_draw(ticket,amount,asset)\n    assert(amount>=1000000,'amount should not be less than 1000000')\n    assert(asset=='COCOS','asset error')\nlocal total=get_account_balance(contract_base_info.owner,asset)\nassert((#public_data.ticket_pool_2)*amount<=total,'Current maximum compensation ratio:'..#public_data.ticket_pool_2..'The biggest bet at present:'..total/(#public_data.ticket_pool_2))\n    transfer_from_caller(contract_base_info.owner,amount,asset,true)\n    local index=random()%(#public_data.ticket_pool_2)+1  --注意：lua数组下标以1开始\nlocal rate=0\n    if(public_data.ticket_pool_2[index]==ticket)then\n        while(true)do\nrate =random()%(#public_data.ticket_pool_2)\nif(rate*amount<=total) then\ntransfer_from_owner(contract_base_info.caller,rate*amount,asset,true)\nbreak\nend\nend\n    end\nlog('ticket:'..public_data.ticket_pool_2[index]..',rate:'..rate)\nend\n--随机累加函数，用于校验链上随机数（测试用）\nfunction sum_public_by_rand()\nassert(is_owner(),'You`re not the contract`s owner')\n    local i=0\n    while(i<10)do\n    i=i+1\n        if(public_data.sum_rand_10==nil)then\n            public_data.sum_rand_10=0\n          public_data.sum_rand_10=public_data.sum_rand_10+random()%100\n        else\n            public_data.sum_rand_10=public_data.sum_rand_10+random()%100\n        end\n    end\nend\n",
      "language": "lua"
    }
  ]
}
[/block]
**5.10. 综合示例二：修改非同质代币的合约相关描述，修改部分为合约对应相关区域**
[block:code]
{
  "codes": [
    {
      "code": "function my_nht_describe_change( nht_hash_or_id,change_values_json)\nlocal change_values=cjson.decode(change_values_json)--注意：此处是cjson模块的使用\nfor key,value in pairs(change_values) do--注意：lua table的遍历，区分ipairs与pairs\nlog('key:'..key..',value:'..value)\nnht_describe_change( nht_hash_or_id,key,value,true)\nend\nend\n//nht_hash_or_id：非同质代币hash或者id\n//change_values_json：json格式的指定修改类容，用于批量修改\n修改合约验证权限\n\nfunction my_change_contract_authority(publickey)\nassert(is_owner(),'You`re not the contract`s owner')\n    change_contract_authority(publickey)\nend\n--设置合约权限验证标识以启用或停止合约签名要求仅有对应的可信执行环境拥有合约权限\n\nfunction set_permissions_flag(flag)\n    assert(is_owner(),'You`re not the contract`s owner')\n    set_permissions_flag(flag)\nend\n--加密数据构造函数\nfunction my_make_memo(to,key,value) make_memo(to,key,value,true) end\n",
      "language": "lua"
    }
  ]
}
[/block]