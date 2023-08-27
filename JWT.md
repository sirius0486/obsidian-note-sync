## token
token 就是一串随机字符串， 通常作为 鉴权凭据， 最常使用的场景是 API 鉴权。是一种表示用户身份、访问权限或其他信息的字符串。 常见的 token 类型有 
- JWT（JSON Web Token）
- Bearer Token 

### sessionID + token

## Json Web Token
> 上文简单介绍了 Token ， JWT 本身也是 Token，它是一种规范化之后的 JSON 结构的 Token。

JWT全称是 json web token ，它是一种网络应用之间以 JSON 对象的形式安全传输信息的开放标准 [RFC 7519 - JSON Web Token (JWT)](https://datatracker.ietf.org/doc/html/rfc7519)。。此信息可以用作验证和相互信任，因为它是经过数字签名的。
JWT 可以使用密钥（使用 **HMAC** 算法）或使用 **RSA** 或 **ECDSA** 的公钥/私钥对进行签名， 从而保证信息没有被篡改，达到安全传输的目的， 

因此JWT 常用于 `授权` 和 `信息交换` 
• 授权：这是使用JWT最常见的情况。一旦用户登录成功，每个后续请求都会包含JWT，允许用户访问受该令牌允许的路由、服务和资源。单点登录是一个广泛使用JWT的功能，因为它具有较小的开销，并且可以轻松地在不同域之间使用。
• 信息交换：JSON Web Tokens是安全传输信息给各方的好方法。因为JWT可以进行签名（例如，使用公钥/私钥对），您可以确保发送者就是他们所声称的身份。此外，由于签名是通过头部和负载计算得出的，您还可以验证内容是否被篡改。


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
```json
{
  "sub": "1234567890",
  "name": "John Doe",
  "iat": 1516239022
}
```
### Signature
**Signature（签名）**：签名由头部、负载和一个秘密密钥生成的哈希值，用于验证消息的完整性和验证发信人。签名的生成算法取决于头部中指定的加密算法。



## JWT 优缺点
### 优点

#### 无状态
JWT 自身包含了身份验证所需要的所有信息，因此，我们的服务器不需要存储 Session 信息。这显然增加了系统的可用性和伸缩性，大大减轻了服务端的压力。因此 JWT 更符合设计 RESTful API 时的「Stateless（无状态）」原则 。

#### 安全
使用 JWT 认证可以有效避免 CSRF 攻击，因为 JWT 一般是存在在 localStorage 中，使用 JWT 进行身份验证的过程中是不会涉及到 Cookie 的

### 缺点
#### 体积大

## Q & A

### JWT 是明文传输的， 如何保证安全性？

### 为什么需要JWT需要经过 base64 编码？

### JWT 如何保证签名不被篡改？

### JWT的优缺点分析？


## 参考资料
https://jwt.io/