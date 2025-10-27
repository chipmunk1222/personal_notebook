*配置ssh密钥流程：*
- 1、创建ssh键值对：ssh-keygen
- 2、配置ssh密钥存储地址(默认为C://user/.ssh)
- 3、配置ssh密钥密码(为保护安全存在，可以不配)
- 4、在github的ssh界面将生成的公钥复制进去，创建标题，即可配置公钥
- 5、查看公钥连接是否成功(公钥与私钥是否匹配)： ssh -T <span>git@github.com</span>
- 6、使用ssh创建远程仓库连接


创建密钥：`ssh-keygen -t rsa -b 4096`
在C://user/.ssh中找公钥私钥，其中，其中`~/.ssh/id_rsa`就是你的私钥, 一定要保护好它不要和任何人分享. `~/.ssh/id_rsa.pub`就是你的公钥内容.