### 使用Git Bash生成新的ssh key

$ cd ~  # 保证当前路径在 “~”下

$ ssh-keygen -t rsa -C "xxxxxx@yy.com" #建议填写自己真是有效的邮箱地址

Generating public/private rsa key pair.

Enter passphrase (empty for no passphrase):   #输入密码（可以为空）

Enter same passphrase again:   #再次确认密码（可以为空）

Your identification has been saved in /c/Users/xxxx_000/.ssh/id_rsa.   #生成的密钥

Your public key has been saved in /c/Users/xxxx_000/.ssh/id_rsa.pub.  #生成的公钥

The key fingerprint is:

e3:51:33:xx:xx:xx:xx:xxx:61:28:83:e2:81 xxxxxx@yy.com

*本机已完成ssh key设置，其存放路径为：c:/Users/xxxx_000/.ssh/下。

