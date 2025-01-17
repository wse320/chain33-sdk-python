- [环境接口](#环境接口)
  - [1 查询节点同步状态](#1-查询节点同步状态)
      - [isSync()](#issync)
- [账户接口](#账户接口)
  - [1 创建账户](#1-创建账户)
      - [newAccountLocal](#newaccountlocal)
  - [2 验证地址](#2-验证地址)
      - [validAddress](#validaddress)
  - [3 转账](#3-转账)
    - [3.1 构造并签名转账交易](#31-构造并签名转账交易)
      - [transferBalanceMain](#transferbalancemain)
    - [3.2 发送交易](#32-发送交易)
      - [submitTransaction](#submittransaction)
    - [3.3 查询主积分余额](#33-查询主积分余额)
      - [getCoinsBalance](#getcoinsbalance)
- [自定义积分接口](#自定义积分接口)
  - [自定义积分的黑名单配置,审核者配置](#自定义积分的黑名单配置审核者配置)
      - [createManage](#createmanage)
  - [预创建自定义积分](#预创建自定义积分)
      - [createPrecreateTokenTx](#createprecreatetokentx)
  - [完成预创建的自定义积分](#完成预创建的自定义积分)
      - [createTokenFinishTx](#createtokenfinishtx)
  - [转自定义积分](#转自定义积分)
      - [createTokenTransferTx](#createtokentransfertx)
  - [查询已经创建的自定义积分](#查询已经创建的自定义积分)
      - [queryCreateTokens](#querycreatetokens)
  - [查询自定义积分](#查询自定义积分)
      - [getTokenBalance](#gettokenbalance)
- [存证接口](#存证接口)
  - [内容明文存证](#内容明文存证)
      - [contentStore](#contentstore)
  - [哈希存证模型，推荐使用sha256哈希，限制256位得摘要值](#哈希存证模型推荐使用sha256哈希限制256位得摘要值)
      - [createHashStorage](#createhashstorage)
  - [链接存证模型](#链接存证模型)
      - [createLinkNotaryStorage](#createlinknotarystorage)
  - [内容对称加密存证](#内容对称加密存证)
      - [createEncryptNotaryStorage](#createEncryptNotaryStorage)
  - [存证结果查询](#存证结果查询)
      - [queryStorage](#querystorage)
- [代理重加密接口](#代理重加密接口)
  - [生成对称秘钥](#生成对称秘钥)
      - [GenerateEncryptKey](#generateencryptkey)
  - [生成重加密共享秘钥分片](#生成重加密共享秘钥分片)
      - [GenerateKeyFragments](#generatekeyfragments)
  - [发送秘钥分片](#发送秘钥分片)
      - [sendKeyFragment](#sendkeyfragment)
  - [请求重加密](#请求重加密)
      - [reencrypt](#reencrypt)
  - [重组重加密共享秘钥分片](#重组重加密共享秘钥分片)
      - [AssembleReencryptFragment](#assemblereencryptfragment)
- [证书服务接口](#证书服务接口)
  - [注册用户](#注册用户)
      - [certUserRegister](#certuserregister)
  - [注销用户](#注销用户)
      - [certUserRevoke](#certuserrevoke)
  - [证书申请](#证书申请)
      - [certEnroll](#certenroll)
  - [用户证书重新申请，用于用户证书被注销后](#用户证书重新申请用于用户证书被注销后)
      - [certReEnroll](#certreenroll)
  - [用户证书注销](#用户证书注销)
      - [certRevoke](#certrevoke)
  - [获取crl列表](#获取crl列表)
      - [certGetCRL](#certgetcrl)
  - [获取用户信息](#获取用户信息)
      - [certGetUserInfo](#certgetuserinfo)
  - [获取证书信息](#获取证书信息)
      - [certGetCertInfo](#certgetcertinfo)
- [国密接口](#国密接口)
  - [SM2生成密钥对](#sm2生成密钥对)
      - [SM2Util.generateKeyPair](#sm2utilgeneratekeypair)
  - [SM2签名](#sm2签名)
      - [SM2Util.sign](#sm2utilsign)
  - [SM2验签](#sm2验签)
      - [SM2Utils.verify](#sm2utilsverify)
  - [SM2非对称加密](#sm2非对称加密)
      - [SM2Utils.encrypt](#sm2utilsencrypt)
  - [SM2非对称解密](#sm2非对称解密)
      - [SM2Utils.decrypt](#sm2utilsdecrypt)
  - [SM3哈希算法](#sm3哈希算法)
      - [SM3Util.hash](#sm3utilhash)
  - [SM4生成对称秘钥](#sm4生成对称秘钥)
      - [SM4Util.generateKey](#sm4utilgeneratekey)
  - [SM4对称加密](#sm4对称加密)
      - [SM4Util.encryptECB](#sm4utilencryptecb)
  - [SM4对称解密](#sm4对称解密)
      - [SM4Util.encryptECB](#sm4utilencryptecb-1)

# 环境接口
> 以下接口操作适用于联盟链和私链的场合，公链和平行链请参考对应的接口说明文档
> 更新时间：2020-02-12

## 1 查询节点同步状态

#### isSync() 
> 用于查询节点同步状态,返回: true表示同步完成，false表示同步未完成

**函数原型：**

```java
public Boolean isSync()
```

**请求参数：**

|参数|类型|是否必填|说明|
|----|----|----|----|
|null|null|null|null|

**返回字段：**

|返回字段|字段类型|说明|
|----|----|----|
|result|bool|同步状态：true表示同步完成，false表示同步未完成， 建议应用层判断同步完成后再发送交易|

**示例：**

```java
RpcClient client = new RpcClient("localhost", 8801);
System.out.println("is sync:" + client.isSync());
```

**适用场景：**

|公链|联盟链|私链|平行链|
|----|----|----|----|
|√|√|√|×|


# 账户接口
## 1 创建账户

#### newAccountLocal

**函数原型：**

```java
public AccountInfo newAccountLocal()
```

**请求参数：**

|参数|类型|是否必填|说明|
|----|----|----|----|
|null|null|null|null|

**返回字段：**

|返回字段|字段类型|说明|
|----|----|----|
|accountInfo|AccountInfo|账户信息，包含私钥，公钥，地址|

**示例：**

```java
AccountInfo accountInfo = account.newAccountLocal();
System.out.println("privateKey is:" + accountInfo.getPrivateKey());
System.out.println("publicKey is:" + accountInfo.getPublicKey());
System.out.println("Address is:" + accountInfo.getAddress());
```

**适用场景：**

|公链|联盟链|私链|平行链|
|----|----|----|----|
|√|√|√|√|


## 2 验证地址

#### validAddress

**函数原型：**

```java
public static boolean validAddress(String address)
```

**请求参数：**

|参数|类型|是否必填|说明|
|----|----|----|----|
|address|string|是|地址|

**返回字段：**

|返回字段|字段类型|说明|
|----|----|----|
|result|bool|地址验证结果|

**示例：**

```java
String address = "1G1L2M1w1c1gpV6SP8tk8gBPGsJe2RfTks";
boolean validAddressResult = TransactionUtil.validAddress(address);
System.out.printf("validate result is:%s", validAddressResult);
```

**适用场景：**

|公链|联盟链|私链|平行链|
|----|----|----|----|
|√|√|√|√|


## 3 转账
> 此处转账只针对联盟链基础积分，此积分在创始区块时就完成初始化,不用手工创建，并且后续不可增发。
> 对于一条确定的链来说，有且只有一种基础积分。 如果要创建多种类不同的积分，可以参考4 token接口

### 3.1 构造并签名转账交易
#### transferBalanceMain

**函数原型：**

```java
public static String transferBalanceMain(TransferBalanceRequest transferBalanceRequest)
```

**请求参数：**

|参数|类型|是否必填|说明|
|----|----|----|----|
|transferBalanceRequest|TransferBalanceRequest|是|构造转账交易的参数|

**示例：**

```java
TransferBalanceRequest transferBalanceRequest = new TransferBalanceRequest();

// 转账说明
transferBalanceRequest.setNote("转账说明");
// 转主积分的情况下，默认填""
transferBalanceRequest.setCoinToken("");
// 转账数量 ， 以下代表转1个积分
transferBalanceRequest.setAmount(1 * 100000000L);
// 转到的地址
transferBalanceRequest.setTo("1CbEVT9RnM5oZhWMj4fxUrJX94VtRotzvs");
// 签名私私钥
transferBalanceRequest.setFromPrivateKey("55637b77b193f2c60c6c3f95d8a5d3a98d15e2d42bf0aeae8e975fc54035e2f4");
// 执行器名称，主链主积分固定为coins
transferBalanceRequest.setExecer("coins");
// 签名类型 (支持SM2, SECP256K1, ED25519)
transferBalanceRequest.setSignType(SignType.SECP256K1);
// 构造好，并本地签好名的交易
String createTransferTx = TransactionUtil.transferBalanceMain(transferBalanceRequest);
System.out.printf("createTransferTx is:%s", createTransferTx);
```

**适用场景：**
|公链|联盟链|私链|平行链|
|----|----|----|----|
|√|√|√|×|

### 3.2 发送交易
> 发送3.1中构造并签好名的交易
#### submitTransaction

**函数原型：**

```java
public String submitTransaction(String data)
```

**请求参数：**

|参数|类型|是否必填|说明|
|----|----|----|----|
|data|String|是|3.1中构造并签好名的交易|

**示例：**

```java
// 交易发往区块链
String txHash = client.submitTransaction(data);
System.out.println(txHash);
```

**适用场景：**

|公链|联盟链|私链|平行链|
|----|----|----|----|
|√|√|√|√|


### 3.3 查询主积分余额
#### getCoinsBalance

**函数原型：**

```java
public List<AccountAccResult> getCoinsBalance(List<String> addresses, String execer)
```

**请求参数：**

|参数|类型|是否必填|说明|
|----|----|----|----|
|addresses|List|是|地址列表|
|execer|String|是|执行器名称：主链主积分情况下，默认为coins|


**示例：**

```java
List<String> list = new ArrayList<>();
list.add("1CbEVT9RnM5oZhWMj4fxUrJX94VtRotzvs");
list.add("1EHWKLEixvfanTHWmnF7mYMuDDXTCorZd7");

QueryTransactionResult queryTransaction1;

List<AccountAccResult> queryBtyBalance;
queryBtyBalance = client.getCoinsBalance(list, "coins");
if (queryBtyBalance != null) {
    for (AccountAccResult accountAccResult : queryBtyBalance) {
        System.out.println(accountAccResult);
    }
```

**适用场景：**

|公链|联盟链|私链|平行链|
|----|----|----|----|
|√|√|√|×|


# 自定义积分接口
> 包含积分名称黑名单，审核者,积分的预发行,积分发行,积分查询等接口
> 积分发行步骤：
> 1. 通过当前链的超级管理员来配置自定义积分的黑名单(全局配置：通常情况下只需要执行一次)。
> 2. 通过当前链的超级管理员来配置自定义积分的审核者(全局配置：通常情况下只需要执行一次)。
> 3. 通过积分审核者来预发行自定义积分。
> 4. 通过积分审核者来正式发行自定义积分。

## 自定义积分的黑名单配置,审核者配置
#### createManage

**函数原型：**

```java
public static String createManage(String key, String value, String op, String privateKey, String execer)
```

**请求参数：**

|参数|类型|是否必填|说明|
|----|----|----|----|
|key|String|是|类型：token-blacklist 代表黑名单， token-finisher 代表审核者|
|value|String|是|具体的值|
|op|String|是|操作符，add,del等|
|privateKey|String|是|构造交易者的私钥|
|execer|String|是|执行器名称，联盟链是manage|


**示例：**

```java
//=========== 黑名单的例子 ==========================
// 管理合约名称
String execerName = "manage";
// 管理合约:配置黑名单KEY
String key = "token-blacklist";
// 管理合约:配置黑名单VALUE
String value = "BTC";
// 管理合约:配置操作符
String op = "add";
// 当前链管理员私钥（superManager）
String privateKey = "55637b77b193f2c60c6c3f95d8a5d3a98d15e2d42bf0aeae8e975fc54035e2f4";
// 构造并签名交易,使用链的管理员（superManager）进行签名， 
// 55637b77b193f2c60c6c3f95d8a5d3a98d15e2d42bf0aeae8e975fc54035e2f4 对应的测试地址是：1EHWKLEixvfanTHWmnF7mYMuDDXTCorZd7
String txEncode = TransactionUtil.createManage(key, value, op, privateKey, execerName);

//=========== token-finisher的例子 ==========================
// 管理合约名称
String execerName = "manage";
// 管理合约:配置KEY
String key = "token-finisher";
// 管理合约:配置VALUE，用于审核token的创建
String value = "1EHWKLEixvfanTHWmnF7mYMuDDXTCorZd7";
// 管理合约:配置操作符
String op = "add";
// 当前链管理员私钥（superManager）
String privateKey = "55637b77b193f2c60c6c3f95d8a5d3a98d15e2d42bf0aeae8e975fc54035e2f4";
// 构造并签名交易,使用链的管理员（superManager）进行签名， 
// 55637b77b193f2c60c6c3f95d8a5d3a98d15e2d42bf0aeae8e975fc54035e2f4 对应的测试地址是：1EHWKLEixvfanTHWmnF7mYMuDDXTCorZd7
String txEncode = TransactionUtil.createManage(key, value, op, privateKey, execerName);
```

**适用场景：**

|公链|联盟链|私链|平行链|
|----|----|----|----|
|√|√|√|×|

## 预创建自定义积分
#### createPrecreateTokenTx

**函数原型：**

```java
public static String createPrecreateTokenTx(String execer, String name, String symbol, String introduction,
            Long total, Long price, String owner, Integer category, String privateKey) 
```

**请求参数：**

|参数|类型|是否必填|说明|
|----|----|----|----|
|execer|String|是|执行器名称，联盟链固定为token|
|name|String|是|token名称|
|symbol|String|是|tokenSymbol，大小写字母+数字|
|introduction|String|是|token介绍|
|total|String|是|发行总量,需要乘以10的8次方，比如要发行100个币，需要100*1e8|
|price|String|是|发行该token愿意承担的费用，填0就行|
|owner|String|是|token地址拥有者|
|category|String|是|token属性类别， 0 为普通token， 1 可增发和燃烧|
|privateKey|String|是|交易发起者的私钥|


**示例：**

```java
//token总额
long total = 19900000000000000L;
//token的注释名称
String name = "DEVELOP COINS";
//token的名称，只支持大写字母，同一条链不允许相同symbol存在
String symbol = "COINSDEVX";
//token介绍
String introduction = "开发者币";
//发行token愿意承担的费用，填0就行
Long price = 0L;
//0 为普通token， 1 可增发和燃烧
Integer category = 0;
//合约名称
String execer = "token";
//token的拥有者地址
String owner = "1EHWKLEixvfanTHWmnF7mYMuDDXTCorZd7";
//链超级管理员私钥
String managerPrivateKey = "55637b77b193f2c60c6c3f95d8a5d3a98d15e2d42bf0aeae8e975fc54035e2f4";
String precreateTx = TransactionUtil.createPrecreateTokenTx(execer, name, symbol, introduction, total, price,
           owner, category, managerPrivateKey);
```

**适用场景：**

|公链|联盟链|私链|平行链|
|----|----|----|----|
|√|√|√|×|

## 完成预创建的自定义积分
#### createTokenFinishTx

**函数原型：**

```java
public static String createTokenFinishTx(String symbol, String execer, String ownerAddr, String managerPrivateKey)
```

**请求参数：**

|参数|类型|是否必填|说明|
|----|----|----|----|
|symbol|String|是|tokenSymbol，大小写字母+数字|
|execer|String|是|执行器名称，联盟链固定为token|
|ownerAddr|String|是|token地址拥有者|
|managerPrivateKey|String|是|交易发起者的私钥|


**示例：**

```java
String symbol = "COINSDEVX";
String execer = "token";
String managerPrivateKey = "55637b77b193f2c60c6c3f95d8a5d3a98d15e2d42bf0aeae8e975fc54035e2f4";
String owner = "1EHWKLEixvfanTHWmnF7mYMuDDXTCorZd7";
String hexData = TransactionUtil.createTokenFinishTx(symbol, execer, owner, managerPrivateKey);
```

**适用场景：**

|公链|联盟链|私链|平行链|
|----|----|----|----|
|√|√|√|×|


## 转自定义积分
#### createTokenTransferTx

**函数原型：**

```java
public static String createTokenTransferTx(String privateKey, String toAddress, String execer, Long amount, String coinToken, String note)

```

**请求参数：**

|参数|类型|是否必填|说明|
|----|----|----|----|
|privateKey|String|是|发起者的私钥|
|toAddress|String|是|转向地址|
|execer|String|是|执行器名称，固定为token|
|amount|Long|是|金额|
|coinToken|String|是|token的symbol|
|note|String|是|token的说明|


**示例：**

```java
// 转账说明
String note = "转账说明";
// token名
String coinToken = "COINSDEVX";
Long amount = 10000 * 100000000L;// 1 = real amount
// 转到的地址
String to = "1CbEVT9RnM5oZhWMj4fxUrJX94VtRotzvs";
// 签名私私钥，里面需要有主链币，用于缴纳手续费
String fromAddressPriveteKey = "55637b77b193f2c60c6c3f95d8a5d3a98d15e2d42bf0aeae8e975fc54035e2f4";
// 执行器名称
String execer = "token";
String createTransferTx = TransactionUtil.createTokenTransferTx(fromAddressPriveteKey, to, execer, amount, coinToken, note);
```

**适用场景：**

|公链|联盟链|私链|平行链|
|----|----|----|----|
|√|√|√|×|


## 查询已经创建的自定义积分
#### queryCreateTokens

**函数原型：**

```java
public List<TokenResult> queryCreateTokens(Integer status,String execer) 

```

**请求参数：**

|参数|类型|是否必填|说明|
|----|----|----|----|
|status|Integer|是|状态 0预创建的 1创建成功的|
|execer|String|是|执行器名称，固定为token|

**示例：**

```java
String execer = "token";
//状态 0预创建的 1创建成功的
Integer status = 1;
List<TokenResult> queryCreateTokens;
queryCreateTokens = client.queryCreateTokens(status,execer);
```

**适用场景：**

|公链|联盟链|私链|平行链|
|----|----|----|----|
|√|√|√|√|

## 查询自定义积分
#### getTokenBalance

**函数原型：**

```java
public List<AccountAccResult> getTokenBalance(List<String> addresses, String execer, String tokenSymbol)

```

**请求参数：**

|参数|类型|是否必填|说明|
|----|----|----|----|
|addresses|List<String>|是|账户地址列表|
|execer|String|是|执行器名称，固定为token|
|tokenSymbol|String|是|token symbol名|

**示例：**

```java
List<String> addressList = new ArrayList<>();
addressList.add("1EHWKLEixvfanTHWmnF7mYMuDDXTCorZd7");
addressList.add("1CbEVT9RnM5oZhWMj4fxUrJX94VtRotzvs");
List<AccountAccResult> queryBtyBalance;
queryBtyBalance = client.getTokenBalance(addressList, "token", "COINSDEVX");
```

**适用场景：**

|公链|联盟链|私链|平行链|
|----|----|----|----|
|√|√|√|√|


# 存证接口
> 包含内容存证, 哈希存证,链接存证,隐私存证,分享隐私存证几个接口


## 内容明文存证
#### contentStore

**函数原型：**

```java
public static String createOnlyNotaryStorage(byte[] content, String execer, String privateKey)
```

**请求参数：**

|参数|类型|是否必填|说明|
|----|----|----|----|
|content|byte[]|是|明文内容|
|privateKey|String|是|构造交易者的私钥|
|execer|String|是|执行器名称，固定是storage|


**示例：**

```java
// 存证智能合约的名称
String execer = "storage";
// 签名用的私钥
String privateKey = "55637b77b193f2c60c6c3f95d8a5d3a98d15e2d42bf0aeae8e975fc54035e2f4";
String content = "存证明文";
String txEncode = StorageUtil.createOnlyNotaryStorage(content.getBytes(), execer, privateKey);
String submitTransaction = client.submitTransaction(txEncode);
```

**适用场景：**

|公链|联盟链|私链|平行链|
|----|----|----|----|
|×|√|√|×|

## 哈希存证模型，推荐使用sha256哈希，限制256位得摘要值
#### createHashStorage

**函数原型：**

```java
public static String createHashStorage(byte[] hash, String execer, String privateKey)
```

**请求参数：**

|参数|类型|是否必填|说明|
|----|----|----|----|
|hash|byte[]|是|明文哈希|
|privateKey|String|是|构造交易者的私钥|
|execer|String|是|执行器名称，固定是storage|


**示例：**

```java
// 存证智能合约的名称
String execer = "storage";
// 签名用的私钥
String privateKey = "55637b77b193f2c60c6c3f95d8a5d3a98d15e2d42bf0aeae8e975fc54035e2f4";
String content = "存证明文";
byte[] contentHash = TransactionUtil.Sha256(content.getBytes());
String txEncode = StorageUtil.createHashStorage(contentHash, execer, privateKey);
```

**适用场景：**

|公链|联盟链|私链|平行链|
|----|----|----|----|
|×|√|√|×|

## 链接存证模型
#### createLinkNotaryStorage

**函数原型：**

```java
public static String createLinkNotaryStorage(byte[] link,byte[] hash, String execer, String privateKey)
```

**请求参数：**

|参数|类型|是否必填|说明|
|----|----|----|----|
|link|byte[]|是|链接|
|hash|byte[]|是|明文哈希|
|execer|String|是|执行器名称，固定是storage|
|privateKey|String|是|构造交易者的私钥|


**示例：**

```java
// 存证智能合约的名称
String execer = "storage";
// 签名用的私钥
String privateKey = "55637b77b193f2c60c6c3f95d8a5d3a98d15e2d42bf0aeae8e975fc54035e2f4";
String link = "https://cs.33.cn/product?hash=13mBHrKBxGjoyzdej4bickPPPupejAGvXr";
String content = "存证明文";
byte[] contentHash = TransactionUtil.Sha256(content.getBytes());
String txEncode = StorageUtil.createLinkNotaryStorage(link.getBytes(), contentHash, execer, privateKey);
```

**适用场景：**

|公链|联盟链|私链|平行链|
|----|----|----|----|
|×|√|√|×|

## 内容对称加密存证
#### createEncryptNotaryStorage

**函数原型：**

```java
public static String createEncryptNotaryStorage(byte[] encryptContent,byte[] contentHash,byte[] nonce, String key, String value, String execer, String privateKey)
```

**请求参数：**

|参数|类型|是否必填|说明|
|----|----|----|----|
|encryptContent|byte[]|是|对称加密的密文|
|contentHash|String|是|明文的hash值|
|nonce|String|是|加密随机数|
|key|String|是|定自义key，不传值默认就是交易hash|
|value|String|是|字符串值|
|execer|String|是|执行器名称，固定是storage|
|privateKey|String|是|构造交易者的私钥|


**示例：**

```java
// 存证智能合约的名称
String execer = "storage";
// 签名用的私钥
String privateKey = "55637b77b193f2c60c6c3f95d8a5d3a98d15e2d42bf0aeae8e975fc54035e2f4";

// 生成AES加密KEY
String aesKeyHex = "ba940eabdf09ee0f37f8766841eee763";
//可用该方法生成 AesUtil.generateDesKey(128);
byte[] key = HexUtil.fromHexString(aesKeyHex);
System.out.println("key:" + HexUtil.toHexString(key));
// 生成iv
byte[] iv = AesUtil.generateIv();
// 对明文进行加密
byte[] encrypt = AesUtil.encrypt(content, key, iv);
String decrypt = AesUtil.decrypt(encrypt, HexUtil.toHexString(key));
System.out.println("decrypt:" + decrypt);
byte[] contentHash = TransactionUtil.Sha256(content.getBytes("utf-8"));
String txEncode = StorageUtil.createEncryptNotaryStorage(encrypt,contentHash, iv, "", "", execer, privateKey);
String submitTransaction = client.submitTransaction(txEncode);
```

**适用场景：**

|公链|联盟链|私链|平行链|
|----|----|----|----|
|×|√|√|×|

## 存证结果查询
#### queryStorage

**函数原型：**

```java
public JSONObject queryStorage(String hash)
```

**请求参数：**

|参数|类型|是否必填|说明|
|----|----|----|----|
|hash|String|是|存证hash|

**示例：**

```java
JSONObject resultJson = client.queryStorage("存证hash");
JSONObject resultArray;
if (resultJson.containsKey("linkStorage")) {
	// hash及link型存证
	resultArray = resultJson.getJSONObject("linkStorage");
	String link = resultArray.getString("link");
	String hash = resultArray.getString("hash");
	byte[] linkByte = HexUtil.fromHexString(link);
	String linkresult = new String(linkByte,"UTF-8");
	System.out.println("存证link是:" + linkresult);
	System.out.println("存证hash是:" + hash);
} else if (resultJson.containsKey("hashStorage")) {
	// hash型存证解析
	resultArray = resultJson.getJSONObject("hashStorage");
	String hash = resultArray.getString("hash");
	System.out.println("链上读取的hash是:" + hash);
	byte[] contentHash = TransactionUtil.Sha256(content.getBytes());
	String result = HexUtil.toHexString(contentHash);
	System.out.println("存证前的hash是:" + result);
} else if (resultJson.containsKey("encryptStorage")) {
	 //隐私存证
	 String desKey = "ba940eabdf09ee0f37f8766841eee763";
	 resultArray = resultJson.getJSONObject("encryptStorage");
	 String content = resultArray.getString("encryptContent");
	 byte[] fromHexString = HexUtil.fromHexString(content);
	 String decrypt = AesUtil.decrypt(fromHexString, desKey);
	 System.out.println(decrypt);      
} else {
	// 内容型存证解析
	resultArray = resultJson.getJSONObject("contentStorage");
	String content = resultArray.getString("content");
	byte[] contentByte = HexUtil.fromHexString(content);
	String result = new String(contentByte,"UTF-8");
	System.out.println("存证内容是:" + result);
}
```

**适用场景：**

|公链|联盟链|私链|平行链|
|----|----|----|----|
|×|√|√|×|


# 代理重加密接口
> 包含生成对称秘钥, 生成重加密共享秘钥分片, 发送秘钥分片, 请求重加密, 重组重加密共享秘钥分片几个接口


## 生成对称秘钥
#### GenerateEncryptKey

**函数原型：**

```java
public static EncryptKey GenerateEncryptKey(byte[] pubOwner)
```

**请求参数：**

|参数|类型|是否必填|说明|
|----|----|----|----|
|pubOwner|byte[]|是|数据共享者公钥|

**返回字段：**

|返回字段|字段类型|说明|
|----|----|----|
|encryptKey|EncryptKey|对称秘钥信息，包含对称秘钥，重加密随机公钥R，重加密随机公钥U|

**示例：**

```java
EncryptKey encryptKey = PreUtils.GenerateEncryptKey(alice.getPubKey());
```

**适用场景：**

|公链|联盟链|私链|平行链|
|----|----|----|----|
|×|√|√|×|

## 生成重加密共享秘钥分片
#### GenerateKeyFragments

**函数原型：**

```java
public static KeyFrag[] GenerateKeyFragments(byte[] privOwner, byte[] pubRecipient, int numSplit, int threshold)  throws Exception
```

**请求参数：**

|参数|类型|是否必填|说明|
|----|----|----|----|
|privOwner|byte[]|是|数据共享者私钥|
|pubRecipient|byte[]|是|数据接收者公钥|
|numSplit|int|是|秘钥分片数|
|threshold|int|是|重组秘钥最小阈值，不能大于numSplit|

**返回字段：**

|返回字段|字段类型|说明|
|----|----|----|
|keyFrags|KeyFrag[]|秘钥分片信息，包含分片随机数，分片秘钥片段，重加密预置公钥|

**示例：**

```java
  KeyFrag[] kFrags = new KeyFrag[numSplit];
  try {
      kFrags = PreUtils.GenerateKeyFragments(alice.getPrivKeyBytes(), bob.getPubKey(), numSplit, threshold);
  } catch (Exception e) {
      e.printStackTrace();
  }
```

**适用场景：**

|公链|联盟链|私链|平行链|
|----|----|----|----|
|×|√|√|×|

## 发送秘钥分片
#### sendKeyFragment

**函数原型：**

```java
public boolean sendKeyFragment(String pubOwner, String pubRecipient, String pubProofR, String pubProofU, String random,
                                  String value, int expire, String dhProof, String precurPub) 
```

**请求参数：**

|参数|类型|是否必填|说明|
|----|----|----|----|
|pubOwner|String|是|数据共享者公钥|
|pubRecipient|String|是|数据接收者公钥|
|pubProofR|String|是|重加密随机公钥R|
|pubProofU|String|是|重加密随机公钥U|
|random|String|是|分片随机数|
|value|String|是|分片秘钥片段|
|expire|int|是|超时时间|
|dhProof|String|是|身份证明|
|precurPub|String|是|重加密预置公钥|


**示例：**

```java
boolean result = client[i].sendKeyFragment(alice.getPublicKeyAsHex(), bob.getPublicKeyAsHex(),
                    encryptKey.getPubProofR(), encryptKey.getPubProofU(), kFrags[i].getRandom(), kFrags[i].getValue(),
                    100, dhProof, kFrags[i].getPrecurPub());
            if (!result) {
                System.out.println("sendKeyFragment failed");
                return;
            }
```

**适用场景：**

|公链|联盟链|私链|平行链|
|----|----|----|----|
|×|√|√|×|


## 请求重加密
#### reencrypt

**函数原型：**

```java
public ReKeyFrag reencrypt(String pubOwner, String pubRecipient)
```

**请求参数：**

|参数|类型|是否必填|说明|
|----|----|----|----|
|pubOwner|String|是|数据共享者公钥|
|pubRecipient|String|是|数据接收者公钥|

**返回字段：**

|返回字段|字段类型|说明|
|----|----|----|
|reKeyFrag|ReKeyFrag|重加密处理后的信息，包含重加密秘钥R，重加密秘钥U，分片随机数，重加密预置公钥 |

**示例：**

```java
        ReKeyFrag[] reKeyFrags = new ReKeyFrag[threshold];
        for(int i = 0; i < threshold; i++) {
            reKeyFrags[i] = client[i].reencrypt(alice.getPublicKeyAsHex(), bob.getPublicKeyAsHex());
        }
```

**适用场景：**

|公链|联盟链|私链|平行链|
|----|----|----|----|
|×|√|√|×|

## 重组重加密共享秘钥分片
#### AssembleReencryptFragment

**函数原型：**

```java
public static byte[] AssembleReencryptFragment(byte[] privRecipient, ReKeyFrag[] reKeyFrags) 
```

**请求参数：**

|参数|类型|是否必填|说明|
|----|----|----|----|
|privRecipient|byte[]|是|数据接收者私钥|
|reKeyFrags|ReKeyFrag[]|是|重加密后的所有秘钥片段|

**返回字段：**

|返回字段|字段类型|说明|
|----|----|----|
|enKey|byte[]|重组后的对称秘钥|

**示例：**

```java
byte[] shareKeyBob = PreUtils.AssembleReencryptFragment(bob.getPrivKeyBytes(), reKeyFrags);
```

**适用场景：**

|公链|联盟链|私链|平行链|
|----|----|----|----|
|×|√|√|×|

# 证书服务接口
> 证书服务包含管理员权限和普通用户权限，管理员可以注册用户，注销用户，注销证书，重生效证书，普通用户可以申请证书，查询证书

## 注册用户
#### certUserRegister

**函数原型：**

```java
public boolean certUserRegister(String userName, String identity, String userPub, String adminKey)
```

**请求参数：**

|参数|类型|是否必填|说明|
|----|----|----|----|
|userName|String|是|用户名|
|identity|String|是|用户ID|
|userPub|String|是|用户公钥|
|adminKey|String|是|管理员私钥，用于身份验证|

**返回字段：**

|返回字段|字段类型|说明|
|----|----|----|
|res|boolean|注册结果|

**示例：**
```java
boolean result = certclient.certUserRegister("ycy", "101", "abcde", "edcba");
```

**适用场景：**

|公链|联盟链|私链|平行链|
|----|----|----|----|
|×|√|√|×|


## 注销用户
#### certUserRevoke

**函数原型：**

```java
public boolean certUserRevoke(String identity, String adminKey)
```

**请求参数：**

|参数|类型|是否必填|说明|
|----|----|----|----|
|identity|String|是|用户ID|
|adminKey|String|是|管理员私钥，用于身份验证|

**返回字段：**

|返回字段|字段类型|说明|
|----|----|----|
|res|boolean|注销结果|

**示例：**
```java
boolean result = certclient.certUserRevoke("101", "edcba");
```

**适用场景：**

|公链|联盟链|私链|平行链|
|----|----|----|----|
|×|√|√|×|


## 证书申请
#### certEnroll

**函数原型：**

```java
public CertObject.CertEnroll certEnroll(String identity, String key)
```

**请求参数：**

|参数|类型|是否必填|说明|
|----|----|----|----|
|identity|String|是|用户ID|
|key|String|是|用户私钥|

**返回字段：**

|返回字段|字段类型|说明|
|----|----|----|
|certEnroll|CertObject.CertEnroll|证书序列号和证书|

**示例：**
```java
CertObject.CertEnroll cert = certclient.certEnroll("101", "edcba");
```

**适用场景：**

|公链|联盟链|私链|平行链|
|----|----|----|----|
|×|√|√|×|

## 用户证书重新申请，用于用户证书被注销后
#### certReEnroll

**函数原型：**

```java
public CertObject.CertEnroll certReEnroll(String identity, String adminKey)
```
**请求参数：**

|参数|类型|是否必填|说明|
|----|----|----|----|
|identity|String|是|用户ID|
|adminKey|String|是|管理员私钥|

**返回字段：**

|返回字段|字段类型|说明|
|----|----|----|
|certEnroll|CertObject.CertEnroll|证书序列号和证书|

**示例：**
```java
CertObject.CertEnroll cert = certclient.certReEnroll("101", "edcba");
```

**适用场景：**

|公链|联盟链|私链|平行链|
|----|----|----|----|
|×|√|√|×|

## 用户证书注销
#### certRevoke

**函数原型：**

```java
public boolean certRevoke(String serial, String identity, String key)
```
**请求参数：**

|参数|类型|是否必填|说明|
|----|----|----|----|
|serial|String|否|证书序列号，通过序列化注销|
|identity|String|否|用户ID，通过用户ID注销|
|adminKey|String|是|管理员私钥|

**返回字段：**

|返回字段|字段类型|说明|
|----|----|----|
|res|boolean|注销结果|

**示例：**
```java
boolean result = certclient.certRevoke("123456", "", "edcba");
```

**适用场景：**

|公链|联盟链|私链|平行链|
|----|----|----|----|
|×|√|√|×|

## 获取crl列表
#### certGetCRL

**函数原型：**

```java
public byte[] certGetCRL(String identity, String key)
```
**请求参数：**

|参数|类型|是否必填|说明|
|----|----|----|----|
|identity|String|是|用户ID|
|key|String|是|用户私钥|

**返回字段：**

|返回字段|字段类型|说明|
|----|----|----|
|res|byte[]|crl格式化输出|

**示例：**
```java
byte[] crl = certclient.certGetCRL("101", "edcba");
```

**适用场景：**

|公链|联盟链|私链|平行链|
|----|----|----|----|
|×|√|√|×|


## 获取用户信息
#### certGetUserInfo

**函数原型：**

```java
public CertObject.UserInfo certGetUserInfo(String identity, String key)
```
**请求参数：**

|参数|类型|是否必填|说明|
|----|----|----|----|
|identity|String|是|用户ID|
|key|String|是|用户私钥|

**返回字段：**

|返回字段|字段类型|说明|
|----|----|----|
|userInfo|CertObject.UserInfo|用户信息|

**示例：**
```java
CertObject.UserInfo userInfo = certclient.certGetUserInfo("101", "edcba");
```

**适用场景：**

|公链|联盟链|私链|平行链|
|----|----|----|----|
|×|√|√|×|

## 获取证书信息
#### certGetCertInfo

**函数原型：**

```java
public CertObject.CertInfo certGetCertInfo(String serial, String key)
```
**请求参数：**

|参数|类型|是否必填|说明|
|----|----|----|----|
|serial|String|是|证书序列号|
|key|String|是|用户私钥|

**返回字段：**

|返回字段|字段类型|说明|
|----|----|----|
|certInfo|CertObject.CertInfo|证书信息|

**示例：**
```java
CertObject.CertInfo certInfo = certclient.certGetCertInfo(cert.serial, "edcba");
```

**适用场景：**

|公链|联盟链|私链|平行链|
|----|----|----|----|
|×|√|√|×|


# 国密接口

> 国密接口包含SM2签名和验证，SM2非对称加密，SM3哈希算法，SM4对称加密

## SM2生成密钥对
#### SM2Util.generateKeyPair

**函数原型：**

```java
public static SM2KeyPair generateKeyPair();
```

**返回字段：**

|返回字段|字段类型|说明|
|----|----|----|
|key | SM2KeyPair| SM2公私钥对|

**示例：**
```java
SM2KeyPair keyPair = SM2Util.generateKeyPair();
```

**适用场景：**

|公链|联盟链|私链|平行链|
|----|----|----|----|
|√|√|√|√|

## SM2签名
#### SM2Util.sign

**函数原型：**

```java
public static byte[] sign(byte[] M, byte[] IDA, SM2KeyPair keyPair) throws IOException;
```

**请求参数：**

|参数|类型|是否必填|说明|
|----|----|----|----|
|M       | byte[]   | 是  | 待签名的消息  |
|IDA     | byte[]   | 是  | 签名方唯一标识|
|keyPair | SM2KeyPair | 是  | 用户公私钥对  |

**返回字段：**

|返回字段|字段类型|说明|
|----|----|----|
|sig |byte[] | 签名|

**示例：**
```java
byte[] sign = SM2Util.sign(SRC_DATA, WITH_ID.getBytes(), keyPair);
```

**适用场景：**

|公链|联盟链|私链|平行链|
|----|----|----|----|
|√|√|√|√|

## SM2验签
#### SM2Utils.verify

**函数原型：**

```java
public static boolean verify(byte[] M, byte[] signatureByte, byte[] IDA, ECPoint aPublicKey);
```

**请求参数：**

|参数|类型|是否必填|说明|
|----|----|----|----|
|M             | byte[] | 是 | 待签名的消息   |
|signatureByte | byte[] | 是 | 签名           |
|IDA           | byte[] | 是 | 签名方唯一标识 |
|aPublicKey    | ECPoint  | 是 | 用户公钥       |

**返回字段：**

|返回字段|字段类型|说明|
|----|----|----|
|result | boolean |验签结果|

**示例：**
```java
boolean flag = SM2Util.verify(SRC_DATA, sign, WITH_ID.getBytes(), keyPair.getPublicKey());
```

**适用场景：**

|公链|联盟链|私链|平行链|
|----|----|----|----|
|√|√|√|√|

## SM2非对称加密
#### SM2Utils.encrypt

**函数原型：**

```java
public static byte[] encrypt(String input, ECPoint publicKey);
```

**请求参数：**

|参数|类型|是否必填|说明|
|----|----|----|----|
|input     |String |是|消息明文 |
|publicKey |ECPoint|是|用户公钥 |

**返回字段：**

|返回字段|字段类型|说明|
|----|----|----|
|cypher |byte[] |  密文|

**示例：**
```java
byte[] encryptedData = SM2Util.encrypt(SRC_DATA_24B, keyPair.getPublicKey());
```

**适用场景：**

|公链|联盟链|私链|平行链|
|----|----|----|----|
|√|√|√|√|

## SM2非对称解密
#### SM2Utils.decrypt

**函数原型：**

```java
public static String decrypt(byte[] encryptData, BigInteger privateKey);
```

**请求参数：**

|参数|类型|是否必填|说明|
|----|----|----|----|
| encryptData | byte[]   | 是  | 消息密文 |
| privateKey  | BigInteger | 是  | 用户私钥 |

**返回字段：**

|返回字段|字段类型|说明|
|----|----|----|
|msg | String |明文 |

**示例：**
```java
String decryptedData = SM2Util.decrypt(encryptedData, keyPair.getPrivateKey());
```

**适用场景：**

|公链|联盟链|私链|平行链|
|----|----|----|----|
|√|√|√|√|

## SM3哈希算法
#### SM3Util.hash

**函数原型：**

```java
public static byte[] hash(byte[] source) throws IOException;
```

**请求参数：**

|参数|类型|是否必填|说明|
|----|----|----|----|
|source  |byte[]   |是  |数据源 |

**返回字段：**

|返回字段|字段类型|说明|
|----|----|----|
|hash  |byte[] |哈希值|

**示例：**
```java
byte[] hash = SM3Util.hash(SRC_DATA);
```

**适用场景：**

|公链|联盟链|私链|平行链|
|----|----|----|----|
|√|√|√|√|

## SM4生成对称秘钥
#### SM4Util.generateKey

**函数原型：**

```java
public static byte[] generateKey();
```

**返回字段：**

|返回字段|字段类型|说明|
|----|----|----|
|key  |byte[] | SM4对称秘钥 |

**示例：**
```java
byte[] key = SM4Util.generateKey();
```

**适用场景：**

|公链|联盟链|私链|平行链|
|----|----|----|----|
|√|√|√|√|

## SM4对称加密
#### SM4Util.encryptECB

**函数原型：**

```java
public static byte[] encryptECB(byte[] key, byte[] data) throws InvalidKeyException;
```

**请求参数：**

|参数|类型|是否必填|说明|
|----|----|----|----|
|key | byte[]|是| 对称秘钥 |
|data| byte[]|是| 数据明文 |

**返回字段：**

|返回字段|字段类型|说明|
|----|----|----|
|cypher| byte[]|数据密文|

**示例：**
```java
cipherText = SM4Util.encryptECB(key, SRC_DATA);
```

**适用场景：**

|公链|联盟链|私链|平行链|
|----|----|----|----|
|√|√|√|√|

## SM4对称解密
#### SM4Util.encryptECB

**函数原型：**

```java
public static byte[] decryptECB(byte[] key, byte[] cipherText) throws InvalidKeyException;
```

**请求参数：**

|参数|类型|是否必填|说明|
|----|----|----|----|
|key        | byte[] | 是| 对称秘钥 |
|cipherText | byte[] | 是| 数据密文 |

**返回字段：**

|返回字段|字段类型|说明|
|----|----|----|
|data |byte[] |数据明文|

**示例：**
```java
decryptedData = SM4Util.decryptECB(key, cipherText);
```

**适用场景：**

|公链|联盟链|私链|平行链|
|----|----|----|----|
|√|√|√|√|