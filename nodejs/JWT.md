# JWT概述
## JWT是什么

`JWT(Json Web Token)`是一种用户会话存储机制，其中，用户会话（`User Session`）用于追踪和管理用户的状态信息，特别是用户身份验证和登录授权等方面。
`JWT`通过传递`Token`来辨识用户信息，其工作流程如下：
1. 用户首次登录后，服务器验证成功，生成并返回`JWT`令牌
2. 客户端将`JWT`令牌存储在本地`localtorage`、`sessionStorage`、`Cookie`中
3. 用户后续登陆时将`JWT`包含在`Http`头部中，在请求时携带`JWT`令牌，后端提取`JWT`并通过验证密钥验证用户信息完整性及有效性
4. 用户登录成功后重新生成会话`token`并重新将其存放在`cookie`中
>在用户手动登出时，要清空`cookie`中的`token`

`JWT`中`token`组成：
```
Header.Payload.Signature
```
1. 头部（`Header`）：通常包含令牌类型和使用的签名算法
2. 负载（`Payload`）：包含用户的主要信息
3. 签名（`Signature`）：为了保证令牌不被篡改，使用加密算法生成

## 为什么需要JWT
`JWT`作为在现代`Web`应用中被广泛使用的技术，其本身相较于传统会话机制具有许多优势
1. **无状态身份验证：** 区别于传统的会话技术，`JWT`通过生成`token`令牌将数据存储在客户端，服务器只保存了验证密钥，从而大大减小了存储开支，在处理大用户数据系统时有很大帮助
2. **安全性：** `JWT`通过数字签名保障了数据的完整性和真实性，即使令牌被截或，也无法随意更改数据，因为会导致数字签名失效
3. **分布式系统中的应用：** `JWT`运行在分布式系统中在多个服务中传递用户信息
4. **跨域身份验证：** `JWT`可以通过`Http`请求中的`Authorization`字段解决跨域问题，如果使用传统会话机制，虽然可以使用`cors`解决跨域，但对于`cookie`来说，`session`会根据不同网站而不断改变
5. **可拓展性：** `JWT`可以包含自定义声明，增加了数据的可拓展性

# 使用JWT
## 安装依赖
`node`实现`JWT`的依赖包名字就叫`jsonwebtoken`
```
npm install jsonwebtoken
```
## 生成JWT
使用`jwt.sign(payload,secretPrivateKey,[options,callback])`生成`JWT`
其中：
1. `payload`表示`JWT`的负载
2. `secretPrivateKay`表示签名生成密钥或私钥，生成方式为`base64(header)+'.'+base64(payload), secretPrivateKey`
3. `options`表示`JWT`配置项
	- `exp`或`expiresIn`：`JWT`过期时间
	- `nbf`或`notBefore`：`JWT`生效时间
	- `aud`或`audience`：接受令牌的受众
	- `iss`或`issue`：令牌的签发者
	- 更多配置项见官方文档[JsonWebToken 中文网 (nodejs.cn)](https://jsonwebtoken.nodejs.cn/#install)
>`exp`和`nbf`类型为`NumbericDate`
```js
const jwt = require('jsonwebtoken');
// 定义一个密钥，用于签名 JWT
const secretKey = 'your-256-bit-secret';
// 用户登录时生成 JWT
function generateToken(user) {
  // 定义要包含在 JWT 中的负载（payload）
  const payload = {
    userId: user.id,
    username: user.username,
  };
  // 生成 JWT
  const token = jwt.sign(payload, secretKey, { expiresIn: '1h' }); // 令牌有效期为1小时
  return token;
}
// 示例用户
const user = { id: 1, username: 'JohnDoe' };
// 生成 JWT
const token = generateToken(user);
console.log('Generated JWT:', token);
```
## 验证JWT
使用`jwt.verify(token,secretPublicKey,[options,calback])`来验证`JWT`
其中：
1. `token：`需要验证的`JWT`
2. `secretPublicKey：`用于验证`JWT`签名的密钥或公钥
3. `options：`格外配置项对象

```js
const jwt = require('jsonwebtoken');
const secretKey = 'your-256-bit-secret';

const token = 'eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...';

const options = {
  algorithms: ['HS256'],
  issuer: 'myIssuer',
  audience: 'myAudience',
};

jwt.verify(token, secretKey, options, (err, decoded) => {
  if (err) {
    console.error('Token verification failed:', err);
  } else {
    console.log('Decoded Payload:', decoded);
  }
});

```