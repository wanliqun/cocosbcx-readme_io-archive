---
title: "7.5 Crypto API"
slug: "75-crypto-api"
hidden: true
createdAt: "2019-04-23T07:58:04.716Z"
updatedAt: "2019-05-31T11:31:35.020Z"
---
## 7.5.1 隐式

**1. blind**

**原型**
[block:code]
{
  "codes": [
    {
      "code": "commitment_type graphene::app::crypto_api::blind(const fc::ecc::blind_factor_type &blind, uint64_t value)",
      "language": "cplusplus"
    }
  ]
}
[/block]
**说明**
生成pedersen承诺：* commit = blind * G + value * G2。承诺是33个字节，隐式因子是32个字节。有关pederson承诺的信息可以参考https://en.wikipedia.org/wiki/Commitment_scheme
**返回值**
一个33字节的pedersen承诺：* commit = blind * G + value * G2
**参数**
blind：Sha-256盲因子类型
value：正64位整数值

**2. blind_sum** 

**原型**
[block:code]
{
  "codes": [
    {
      "code": "blind_factor_type graphene::app::crypto_api::blind_sum(const std::vector<blind_factor_type> &blinds_in, uint32_t non_neg)",
      "language": "cplusplus"
    }
  ]
}
[/block]
**说明**
获得sha-256 类型隐式因子
**返回值**
一个隐式类型因子
**参数**
blinds_in：sha-256盲因子类型列表
non_neg：32位整数值

## 7.5.2 隐式

**1. range_get_info**

**原型**
[block:code]
{
  "codes": [
    {
      "code": "range_proof_info graphene::app::crypto_api::range_get_info(const std::vector<char> &proof)",
      "language": "cplusplus"
    }
  ]
}
[/block]
**说明**
获取“范围验证”信息。cli_wallet包含发送隐式传输的功能，其中输入和输出数量的值是“隐形的”。在事务产生两个或多个输出的情况下，必须提供“范围证明”，以证明所有输出都没有提交负值。
**返回值**
一个范围证明的信息结构：指数，尾数，最大值和最小值
**参数**
proof: 证明字符列表

**2. range_proof_sign** 

**原型**
[block:code]
{
  "codes": [
    {
      "code": "std::vector<char> graphene::app::crypto_api::range_proof_sign(uint64_t min_value, constcommitment_type &commit, const blind_factor_type &commit_blind, const blind_factor_type &nonce, int8_t base10_exp, uint8_t min_bits, uint64_t actual_value)",
      "language": "cplusplus"
    }
  ]
}
[/block]
**说明**
对于min_value，证明了具有给定隐式因子和值的pedersen承诺的范围。
**返回值**
作为证明的字符列表
**参数**
min_value：正64位整数值
commit：33字节的pederson承诺
commit_blind：Sha-256隐式因子类型为正确的数字
nonce：非伪造签名的Sha-256盲因子类型
exp：指数基数为10 [-1; 18]
min_bits：8位正整数，必须在[0; 64]
actual_value：64位正整数，必须大于或等于min_value

## 7.5.3 验证

**1. verify_sum** 

**原型**
[block:code]
{
  "codes": [
    {
      "code": "bool graphene::app::crypto_api::verify_sum(const std::vector<commitment_type> &commits_in, const std::vector<commitment_type> &neg_commits_in, int64_t excess)",
      "language": "cplusplus"
    }
  ]
}
[/block]
**说明**
验证 commits + neg_commits + excess == 0
**返回值**
Bool运算，如果commits + neg_commits + excess == 0返回true, 否则返回 false
**参数**
commits_in：33字节pedersen承诺清单
neg_commits_in：33字节pedersen承诺清单
excess：两个33字节pedersen承诺列表的总和，其中第一组的总和减去第二组

**2. verify_range** 

**原型**
[block:code]
{
  "codes": [
    {
      "code": "verify_range_result graphene::app::crypto_api::verify_range(const fc::ecc::commitment_type &commit, const std::vector<char> &proof)",
      "language": "cplusplus"
    }
  ]
}
[/block]
**说明**
验证 commits + neg_commits + excess == 0
**返回值**
验证33字节pedersen承诺的范围证明
**参数**
commit：33字节的pedersen承诺
proof：字符列表

**3. verify_range_proof_rewind** 

**原型**
[block:code]
{
  "codes": [
    {
      "code": "verify_range_proof_rewind_result graphene::app::crypto_api::verify_range_proof_rewind(constblind_factor_type &nonce, const fc::ecc::commitment_type &commit, const std::vector<char> &proof)",
      "language": "cplusplus"
    }
  ]
}
[/block]
**说明**
验证历史记录中33字节pedersen承诺的范围证明
**返回值**
success，min，max，value_out，blind_out和message_out
**参数**
nonce：Sha-256盲目重构型
commit：33字节的佩德森承诺
proof：字符列表