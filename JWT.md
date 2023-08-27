

### token
token 就是一串随机字符串， 通常作为 鉴权凭据， 最常使用的场景是 API 鉴权。是一种表示用户身份、访问权限或其他信息的字符串。 常见的 token 类型有 
- JWT（JSON Web Token）
- Bearer Token 

### Json Web Token
JWT全称是 json web token ，它是一种网络应用之间以 JSON 对象的形式安全传输信息的开放标准 [RFC 7519 - JSON Web Token (JWT)](https://datatracker.ietf.org/doc/html/rfc7519)。。此信息可以用作验证和相互信任，因为它是经过数字签名的。
JWT 可以使用密钥（使用 **HMAC** 算法）或使用 **RSA** 或 **ECDSA** 的公钥/私钥对进行签名， 从而保证信息没有被篡改，达到安全传输的目的， 因此JWT 常用于 `授权` 和 `信息交换`

**JWT通常以字符串形式表示，由三部分组成，通过点号（.）分隔开来：**
### Header
1. **Header（头部）**：头部通常包含令牌的类型（"typ"）和使用的加密算法（"alg"）。例如：
```json
{
	"typ": "JWT", 
	"alg": "HS256"
 }

```
### Playload
**Payload（负载）**：负载包含有关声明的信息。声明是关于实体（通常是用户）和其他数据的声明。负载可以包含预定义的声明，如用户ID、到期时间等，还可以包含自定义的声明。例如：{"sub": "1234567890", "name": "John Doe", "exp": 1516239022}。

### Signature
**Signature（签名）**：签名由头部、负载和一个秘密密钥生成的哈希值，用于验证消息的完整性和验证发信人。签名的生成算法取决于头部中指定的加密算法。