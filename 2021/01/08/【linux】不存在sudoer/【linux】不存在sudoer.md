# 【linux】不存在sudoer

用户 不在 sudoers 文件中。此事将被报告。

普通linux用户使用sudo命令执行只有root用户才可以执行的命令时出现了该错误，如下图示：

![](不存在sudoer\20190712095902322.png)

简单说明一下操作。命令$ ll /etc/sudoers表示查看文件的属性，属性包括有：文件拥有者、文件所属组以及其他用户组对该文件拥有的读写权限和文件的类型等，上图的/etc/sudoers文件表示拥有者和所属组都是root且只能读取，其他用户组的没有任何读写权限。

命令$ sudo cat /etc/sudoers表示当前登录用户是普通用户zouqi，我想使用该用户查看/etc/sudoers文件的内容，由于需要有root权限才能查看该文件的内容，于是使用sudo命令来让普通用户临时拥有root权限来执行查看内容命令，但是后面输入密码后发现命令无法成功执行（查看失败了），报错标题所诉zouqi 不在 sudoers 文件中。此事将被报告。错误。

解决方案
根据错误提示，只需将当前登录用户，图中所示用户是zouqi加入到sudoers文件中即可。

切换至root用户
$ su - root
![](不存在sudoer\20190712102620727.png)

给root用户添加可写权限
chmod 640 /etc/sudoers
![](不存在sudoer\20190712102855624.png)


修改sudoers文件
```bash
# vim /etc/sudoers
```
![](不存在sudoer\20190712103601971.png)

如上图所示位置加上zouqi ALL=(ALL) ALL后，按下esc键，输入:wq保存修改并退出编辑。

查看是否修改成功
```bash
# cat /etc/sudoers
```
![](不存在sudoer\20190712103947180.png)

可以看到已经成功添加了用户zouqi到sudoers文件中。

修改sudoers文件：只读权限（原有权限）
```bash
	chmod 440 /etc/sudoers
```

普通用户继续使用sudo命令验证
# exit
![](不存在sudoer\20190712104509383.png)
exit表示返回普通用户zouqi

```bash
sudo cat /etc/sudoers
```


sudo命令继续查看sudoers文件内容验证结果。如下图示：

![](不存在sudoer\20190712104814766.png)

根据图示可知问题已经解决。