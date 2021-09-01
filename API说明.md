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

#### publicKeyFromPrivate(priv: str)
>publicKeyFromPrivate 由私钥生成公钥，返回值为：公钥字符串

 **函数原型**
```python
def publicKeyFromPrivate(priv: str) -> str:
```
 **请求参数：**

|参数|类型|是否必填|说明|
|----|----|----|----|
|priv|str|yes|私钥|

**返回字段：**

|返回字段|字段类型|说明|
|----|----|----|
|publickey|str|返回公钥的字符串|

#### sign(msg: bytes, priv: str)
>sign 使用传入的私钥对消息进行签名

 **函数原型**
```python
def sign(msg: bytes, priv: str) -> bytes:
```
 **请求参数：**

|参数|类型|是否必填|说明|
|----|----|----|----|
|msg|str|yes|需要加密的消息|
|priv|str|yes|私钥|

**返回字段：**

|返回字段|字段类型|说明|
|----|----|----|
|msg|str|Bytes形式字符串的加密后消息|
