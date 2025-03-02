`bcrypt.js`是一种对密码进行`hash`加密的技术，它可以帮助我们在存储密码时增加安全性
>`bcrypt.js`最大输入长度为`72`字节，生成的`hash`值长度为`60`个字符

# 使用bcrypt.js
## 安装依赖
```
npm install bcrypt.js
```
## 同步加密
使用`bcrypt.js`的步骤如下：
1. 引入`bcript.js`依赖
2. 生成盐（`salt`），使用`genSaltSync`生成盐
3. 通过盐生成`hash`加密的`password`，使用`hashSync`方法
4. 使用`comparaSync(password,hash)`来验证密码和`hash`值的一致性
```js
const bcrypt = require('bcryptjs');

// 原始密码
const password = 'mySuperSecretPassword';

// 同步生成盐
const salt = bcrypt.genSaltSync(10);
// 同步哈希加密
const hash = bcrypt.hashSync(password, salt);

console.log('Hashed Password:', hash);

// 同步验证密码
const isMatch = bcrypt.compareSync(password, hash);
console.log('Password is', isMatch ? 'valid' : 'invalid');
```

## 异步加密
`bcript.js`异步加密过程如下：
1. 引入`bcript.js`依赖
2. 使用`genSalt(num,callback(err,salt))`生成盐，回调函数带有`err`、`salt`两个默认参数
3. 使用`genhash(password,salt,callback(err,hash))`生成`hash`密码，回调函数具有`err`、`hash`两个参数
4. 使用`compare(password,hash,callback(err,isMatch))`进行校验，回调函数带有`err`、`isMatch`两个参数
```js
const bcrypt = require('bcryptjs');

// 要加密的原始密码
const password = 'mySuperSecretPassword';

// 生成盐并对密码进行哈希加密
bcrypt.genSalt(10, (err, salt) => {
  if (err) throw err;
  
  bcrypt.hash(password, salt, (err, hash) => {
    if (err) throw err;
    
    console.log('Hashed Password:', hash);

    // 验证密码
    bcrypt.compare(password, hash, (err, isMatch) => {
      if (err) throw err;

      if (isMatch) {
        console.log('Password is valid');
      } else {
        console.log('Password is invalid');
      }
    });
  });
});
```
>使用异步方法的优势：异步方法在整个过程中使用回调函数进行过程串联，解决了同步过程导致的阻塞，在处理大量数据时具有更大优势
