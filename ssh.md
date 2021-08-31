```shell
ssh-keygen -t rsa
```

生成两个文件 id_rsa（私钥）、id_rsa.pub（公钥）

```
ssh-copy-id #分发
```

.ssh文件下的解释

| known_hosts     | 记录 ssh 访问过计算机的公钥（public key） |
| --------------- | ----------------------------------------- |
| id_rsa          | 生成的私钥                                |
| id_rsa.pub      | 生成的公钥                                |
| authorized_keys | 存放授权过的无密登录服务器公钥            |

  


 
  