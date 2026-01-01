# 参考文档：

靠谱文档：https://github.com/zzhenghua/agsb

微信文档：https://mp.weixin.qq.com/s?__biz=MzkyNzYzNTQ2Nw==&mid=2247485335&idx=1&sn=d30c23d7bca7fd87041f341ca9855ef2&chksm=c333fb35624866db3cc61a814efa8d4ec36c002ee82bfa3bbeca2ba38c9ac9a7df493a3ffa70&mpshare=1&scene=1&srcid=12313y2ZHvqVmigWKoT09eWG&sharer_shareinfo=30e6475b8361f328a67e108c19775430&sharer_shareinfo_first=13d59c798426649b498fcb9b4667b23d#rd

# 操作文档：

```
歇斯底里Hy2防墙一键脚本，nginx伪装、加密混淆、BBR加速一键部署
✨核心特性：
特性
描述
🎯 一键部署
单命令完成所有配置
🔄 多端口配置
支持生成100个不同端口的节点配置
🔒 Salamander混淆
自动生成混淆密码，防DPI检测
🌐 nginx Web伪装
TCP端口显示正常企业网站
⚡ BBR优化
启用BBR拥塞控制算法，提升网络性能
GitHub项目地址：
https://github.com/zhumengkang/agsb
顺便给作者点个“Star”。
本篇文章防失联：
歇斯底里Hy2防墙一键脚本，nginx伪装、加密混淆、BBR加速一键部署 - W不懂安全的文章 - 知乎
https://zhuanlan.zhihu.com/p/1959282983593830205
📥 一键部署

cd ~ && curl -O https://raw.githubusercontent.com/zhumengkang/agsb/main/nginx-hysteria2.py && python3 nginx-hysteria2.py install --simple --port-range 28888-29999 --enable-bbr
如果你想让线路少点，就修改部署命令中的端口即可，差数越大，数量越多，差数越小数量越少。

安装完成之后，你可以看到它给出了5个配置文件的下载地址，防护特性也给出了总结，端口跳跃都指向443，也就是说这些端口其中一个被封了，也不会影响其他端口。

图片
这里我访问V2的地址，访问成功之后页面显示的是一大堆hy2的配置链接，Ctrl+A全部复制下来，然后到V2软件里粘贴进去，这里我就展示一部分。

图片
如果说你们粘贴进去之后测试延迟是-1，那么看接下来的步骤。

执行以下命令：

ss -u -lpn | grep hysteria
如果显示如图的内容，证明443端口只负责监听，我们需要手动启动多端口随机转发到443，再自动转发到443端口。（提高抗封锁）

图片
执行以下命令：

apt install iptables-persistent -y
netfilter-persistent save
for port in $(seq 28888 29999); do
  iptables -t nat -A PREROUTING -p udp --dport $port -j REDIRECT --to-port 443
done
之后重新测试一下延迟，就可以正常有延迟了。

我们访问以下地址：

http://服务器IP/
你会看到一个页面，这个页面就是用来伪装的页面，不要修改。

图片
如何删除、查看历史的线路信息？

在终端输入：

kk
因为在执行脚本的时候，脚本中已经创建了全局命令。

图片
图片
本期内容到此结束。

三连加关注，追文不迷路。
```



# 节点（在终端输入:kk查看节点信息）

📄 端口跳跃JSON配置已保存到：/root/.hysteria2/client-config.json
📄 v2rayN配置已保存到：/root/.hysteria2/v2rayn-config.yaml
📄 Clash配置已保存到：/root/.hysteria2/clash-config.yaml
📄 官方客户端配置已保存到：/root/.hysteria2/hysteria-official-config.yaml
📄 客户端端口跳跃配置已保存到：/root/.hysteria2/hysteria-client-hopping.yaml
🌐 设置配置文件下载服务...
🔧 启动Python HTTP服务器...
HTTP服务器已启动，端口: 8080
✅ Python HTTP服务器启动成功