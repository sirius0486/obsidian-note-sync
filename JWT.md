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


**JWT通常以字符串形式表示，由三部分组成，通过点号（.）分隔开，每一部份都经过base64 编码，如 `xxxxx.yyyyy.zzzzz` 下面👇是 一个JWT 的实际例子：**
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
> **Payload（负载）**：负载包含有关声明的信息。声明是关于实体（通常是用户）和其他数据的声明。通样也需要进行 base64 编码， 形成 JWT 的第二部分， 存放信息

`Playload` 是 `JWT` 的第二部分， playload 有三种类型的 `声明 (claims)`： 
- **注册声明**  registered claims
- **公共声明**  public claims
- **私有声明** private claims

```json
{
  "sub": "1234567890",
  "name": "John Doe",
  "iat": 1516239022
}
```
#### register
注册声明：这些是一组预定义的声明，不是强制性的，但建议使用，以提供一组有用、可互操作的声明。其中包括 iss（发行人）、exp（过期时间）、sub（主题）、aud（受众）等等。
#### public
这些可以由使用JWT的人自行定义。但为了避免冲突，它们应该在IANA JSON Web Token注册表中定义，或者定义为包含冲突防护命名空间的URI
#### private
这些是为了在同意使用它们的各方之间共享信息而创建的自定义声明，并且既不是已注册也不是公共声明

### Signature
> **Signature（签名）**：签名用于验证消息的完整性和验证发信人。签名的生成算法取决于头部中指定的加密算法。

要创建签名部分，您需要获取 `1.Header 编码的头部 `、`2.playload 编码的负载`、`3.一个密钥`，`4.头部中指定的算法`，并对其进行签名。

例如，如果您想使用 `HMAC SHA256` 算法，则签名将按以下方式创建：
```
HMACSHA256(
  base64UrlEncode(header) + "." +
  base64UrlEncode(payload),
  secret)
```

**签名用于验证消息在传递过程中是否被更改**，对于使用私钥签名的令牌，它还可以验证JWT的发送者是否真实可信。

将三部分放在一起，输出是 `由 . 分隔` 的三个 Base64-URL字符串，可以轻松地在HTML和HTTP环境中传递，与基于XML的标准（如SAML）相比更紧凑。

下面展示了一个JWT，其中包含前面编码过的头部和负载，并使用一个密钥进行签名
```json

eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyfQ.SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c
```

## JWT 如何工作？
> JSON Web Tokens（JWT）是如何工作的？

在身份验证中，当用户成功使用其 **凭据(如用户名+密码 )** 登录时，将返回一个JSON Web Token。由于令牌是凭证，必须非常小心以防止安全问题。一般来说，您不应该保留超过所需时间的令牌。也不应该将敏感会话数据存储在浏览器存储中，因为缺乏安全性。

每当用户想要访问受保护的路由或资源时，用户代理应该发送JWT，在通常情况下使用Bearer模式的Authorization头部。头部内容应如下所示：
```http
Authorization: Bearer <token>
```

在某些情况下，这可以是一种无状态的授权机制。服务器的受保护路由将检查Authorization头中是否存在有效的JWT，如果存在，则允许用户访问受保护资源。如果JWT包含所需数据，则可能减少对数据库进行某些操作的需要，尽管这并不总是如此。请注意，如果您通过HTTP头发送JWT令牌，请尽量防止它们变得过大。有些服务器不接受超过8 KB的头部信息。如果您试图在JWT令牌中嵌入太多信息（例如包括所有用户权限），则可能需要其他解决方案，比如Auth0 Fine-Grained


如果令牌通过Authorization头部发送，跨源资源共享（CORS）将不会成为问题，因为它不使用cookies。下面的图示展示了如何获取JWT并用于访问API或资源：
![[Pasted image 20230827220705.png]]

1. 应用程序或客户端向授权服务器请求授权。这是通过不同的授权流程之一来完成的。例如，一个典型的符合`OpenID Connect`标准的Web应用程序将使用授权码流程通过 `/oauth/authorize` 端点进行操作
2. 授权被批准后，授权服务器会向应用程序返回访问令牌。
3. 应用程序使用访问令牌来访问受保护资源（如API）。

请注意，对于已签名的令牌，所有包含在令牌中的信息都会暴露给用户或其他方，并且他们无法更改它。因此，请勿在令牌中放置机密信息。

## JWT 优缺点
### 优点

#### 无状态
JWT 自身包含了身份验证所需要的所有信息，因此，我们的服务器不需要存储 Session 信息。这显然增加了系统的可用性和伸缩性，大大减轻了服务端的压力。因此 JWT 更符合设计 RESTful API 时的「Stateless（无状态）」原则 。

#### 安全
使用 JWT 认证可以有效避免 CSRF 攻击，因为 JWT 一般是存在在 localStorage 中，使用 JWT 进行身份验证的过程中是不会涉及到 Cookie 的
JWT和SAML令牌可以使用公钥/私钥对形式的X.509证书进行签名。与将XML用XML数字签名进行签名而不引入模糊不清的安全漏洞相比，这样做非常困难；而在处理JSON时则简单得多。
### 体积小
为什么我们应该使用JSON Web Tokens？让我们谈谈与Simple Web Tokens（SWT）和Security Assertion Markup Language Tokens（SAML）相比，JSON Web Tokens（JWT）的好处。由于JSON比XML更简洁，编码后的大小也更小，使得JWT比SAML更紧凑。这使得在HTML和HTTP环境中传递JWT成为一个不错的选择。

### 缺点
#### 安全风险


## Q & A
#### 使用 JWT 进行身份验证的过程？

### JWT 是明文传输的， 如何保证安全性？

### 为什么需要JWT需要经过 base64 编码？

### JWT 如何保证签名不被篡改？
有了签名之后，即使 JWT 被泄露或者截获，黑客也没办法同时篡改 Signature、Header、Payload。

这是为什么呢？因为服务端拿到 JWT 之后，会解析出其中包含的 Header、Payload 以及 Signature 。服务端会根据 Header、Payload、密钥再次生成一个 Signature。拿新生成的 Signature 和 JWT 中的 Signature 作对比，如果一样就说明 Header 和 Payload 没有被修改。

不过，如果服务端的秘钥也被泄露的话，黑客就可以同时篡改 Signature、Header、Payload 了。黑客直接修改了 Header 和 Payload 之后，再重新生成一个 Signature 就可以了。

**密钥一定保管好，一定不要泄露出去。JWT 安全的核心在于签名，签名安全的核心在密钥。**

#### 加强使用 JWT 的安全性？
- 使用安全系数高的加密算法。
- 使用成熟的开源库，没必要造轮子。
- JWT 存放在 localStorage 中而不是 Cookie 中，避免 CSRF 风险。
- 一定不要将隐私信息存放在 Payload 当中。
- 密钥一定保管好，一定不要泄露出去。JWT 安全的核心在于签名，签名安全的核心在密钥。
- Payload 要加入 `exp` （JWT 的过期时间），永久有效的 JWT 不合理。并且，JWT 的过期时间不易过长。
- ......



## 参考资料
https://jwt.io/