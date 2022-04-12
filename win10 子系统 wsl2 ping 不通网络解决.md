# win10 子系统 wsl2 ping 不通网络解决 #

在一次 win10 升级后，原有的 wsl2 Ubuntu 就连不上网络了，然后谷歌搜索找到如下解决方案：

```
=============================================================================
FIX WSL2 NETWORKING IN WINDOWS 10
=============================================================================
cmd as admin:
wsl --shutdown
netsh winsock reset
netsh int ip reset all
netsh winhttp reset proxy
ipconfig /flushdns

Windows Search > Network Reset

Restart Windows
```

或者

```
# Fix network issues
# Delete auto-generated files
[root@PC-NAME user]# rm /etc/resolv.conf || true
[root@PC-NAME user]# rm /etc/wsl.conf || true

# Enable changing /etc/resolv.conf
# Enable extended attributes on Windows drives
[root@PC-NAME user]# cat <<EOF > /etc/wsl.conf
[network]
generateResolvConf = false

[automount]
enabled = true
options = "metadata"
mountFsTab = false
EOF

# Use google nameservers for DNS resolution
[root@PC-NAME user]# cat <<EOF > /etc/resolv.conf
nameserver 8.8.8.8
nameserver 8.8.4.4
EOF

Exit Linux WSL

cmd as admin:
wsl --shutdown
netsh winsock reset
netsh int ip reset all
netsh winhttp reset proxy
ipconfig /flushdns

Windows Search > Network Reset

Restart Windows
```

我是使用第一种方法修复的。

感谢大神的分享。

参考链接

作者：ashin_l

链接：https://www.jianshu.com/p/04eaefdcc862

来源：简书

著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。