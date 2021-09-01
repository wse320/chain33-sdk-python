# 加密相关接口
## ed25519.py

#### generatePrivateKey()
> 用于生成私钥，返回值为：私钥字符串

 **函数原型**
 
 ```python
 def generatePrivateKey() -> str
 ```
 
 **请求参数：**

|参数|类型|是否必填|说明|
|----|----|----|----|
|null|null|null|null|

**返回字段：**

|返回字段|字段类型|说明|
|----|----|----|
|privatekey|str|返回私钥的字符串|
<br/>

---

#### publicKeyFromPrivate(priv: str)
>publicKeyFromPrivate 由私钥生成公钥，返回值为：公钥字符串

 **函数原型**
```python
def publicKeyFromPrivate(priv: str) -> str
```
 **请求参数：**

|参数|类型|是否必填|说明|
|----|----|----|----|
|priv|str|yes|私钥|

**返回字段：**

|返回字段|字段类型|说明|
|----|----|----|
|publickey|str|返回公钥的字符串
<br/>

---
#### sign(msg: bytes, priv: str)
>sign 使用传入的私钥对消息进行签名

 **函数原型**
```python
def sign(msg: bytes, priv: str) -> bytes
```
 **请求参数：**

|参数|类型|是否必填|说明|
|----|----|----|----|
|msg|str|yes|需要加密的消息|
|priv|str|yes|私钥|

**返回字段：**

|返回字段|字段类型|说明|
|----|----|----|
|msg|str|Bytes形式字符串的签名后消息|
<br/>

---
#### verify(msg: bytes, sig: bytes, pub: str)
>verify 对传入的消息使用签名进行认证

 **函数原型**
```python
def verify(msg: bytes, sig: bytes, pub: str) -> bool
```
 **请求参数：**

|参数|类型|是否必填|说明|
|----|----|----|----|
|msg|str|yes|已加密的消息|
|sig|str|yes|签名字符串|
|pub|str|yes|公钥|

**返回字段：**

|返回字段|字段类型|说明|
|----|----|----|
|result|bool|结果为真或假的布尔值|

<br/>

## coins.py

#### transfer(title: str, amount: int, toAddr: str, note: str)
>transfer 构造普通转账交易

 **函数原型**
```python
def transfer(title: str, amount: int, toAddr: str, note: str) -> tx.Transaction:
```
 **请求参数：**

|参数|类型|是否必填|说明|
|----|----|----|----|
|title|str|yes|平行链链名前缀 比如user.p.huobi.|
|amount|str|yes|转账金额|
|toAddr|str|yes|收款地址|
|note|str|yes|备注|

**返回字段：**

|返回字段|字段类型|说明|
|----|----|----|
|交易结果|tx.Transaction|交易结果的集合类型|
