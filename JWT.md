## token
token 就是一串随机字符串， 通常作为 鉴权凭据， 最常使用的场景是 API 鉴权。是一种表示用户身份、访问权限或其他信息的字符串。 常见的 token 类型有 
- JWT（JSON Web Token）
- Bearer Token 

### sessionID + token

## Json Web Token
JWT全称是 json web token ，它是一种网络应用之间以 JSON 对象的形式安全传输信息的开放标准 [RFC 7519 - JSON Web Token (JWT)](https://datatracker.ietf.org/doc/html/rfc7519)。。此信息可以用作验证和相互信任，因为它是经过数字签名的。
JWT 可以使用密钥（使用 **HMAC** 算法）或使用 **RSA** 或 **ECDSA** 的公钥/私钥对进行签名， 从而保证信息没有被篡改，达到安全传输的目的， 因此JWT 常用于 `授权` 和 `信息交换` 

**JWT通常以字符串形式表示，由三部分组成，通过点号（.）分隔开，每一部份都经过base64 编码， 一个JWT的例子是：**
`eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyfQ.SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c
`

### Header
>   **Header（头部）**：

头部通常包含令牌的类型（"typ"）和使用的加密算法（"alg"）。例如：
```json
{
	"typ": "JWT", 
	"alg": "HS256"
 }
```

- `typ` 其实就是 `type` 的简写， **标识令牌的类型**
- alg 其实就是  `algorithm` 的简写。 **标识使用的加密算法**

当然 header 还包含很多字段， 如
- **`jku`（JWK Set URL）**：指向包含JWT验证密钥的JWK（JSON Web Key）集合的URL
- **`cty`（Content Type）**：表示JWT的内容类型。这个字段通常用于指定嵌入的内容，如JWS（JSON Web Signature）或JWE（JSON Web Encryption）
- **`kid`（Key ID）**：表示用于签名或解码JWT的密钥的唯一标识符。
- **`zip`（Compression Algorithm）**：表示用于JWT有效载荷的压缩算法。
- 自定义字段： 根据需要，可以添加自定义字段来传递特定的元数据

### Playload
> **Payload（负载）**：负载包含有关声明的信息。声明是关于实体（通常是用户）和其他数据的声明。

Playload 是 JWT 的 第二部分， playload 有两种类型的声明：预定义声明和自定义声明

### Signature
**Signature（签名）**：签名由头部、负载和一个秘密密钥生成的哈希值，用于验证消息的完整性和验证发信人。签名的生成算法取决于头部中指定的加密算法。



## JWT 优缺点
### 优点

#### 无状态
#### 安全
### 缺点
#### 体积大

## Q & A

### JWT 是明文传输的， 如何保证安全性？

### 为什么需要JWT需要经过 base64 编码？

### JWT 如何保证签名不被篡改？

### JWT的优缺点分析？


## 参考资料
https://jwt.io/