- 强烈建议开启bbr加速，可大幅加快节点reality和vmess节点的速度
- 安装完成后终端输入 mianyang 可再次调用本脚本

# 12.11更新

- 全面适配sing-box1.8.0
- 新添加了warp解锁功能（默认openai和奈飞，可切换为全局warp接管解锁all），输入mianyang，查看。
- 新添加了hysteria2端口跳跃功能，输入mianyang，查看。

# 简介
- Reality Hysteria2 （vmess ws）一键安装脚本
  
## 使用教程

### reality和hysteria2 vmess ws三合一脚本

```bash
bash <(curl -fsSL https://github.com/vveg26/sing-box-reality-hysteria2/raw/main/beta.sh)
```

### reality hysteria2二合一脚本

```bash
bash <(curl -fsSL https://github.com/vveg26/sing-box-reality-hysteria2/raw/main/install.sh)
```

## 功能

- 无脑回车一键安装或者自定义安装
- 完全无需域名，使用自签证书部署hy2，（使用argo隧道支持vmess ws优选ip（理论上比普通优选ip更快））
- 支持修改reality端口号和域名，hysteria2端口号
- 无脑生成sing-box，clash-meta，v2rayN，nekoray等通用链接格式

![](https://img.mareep.net/blog/2023/12/22670b590ded0df4b5e8663878628136.jpg)
![](https://img.mareep.net/blog/2023/12/389786b320b3b0dd905b90e323483cff.png)
![](https://img.mareep.net/blog/2023/12/565952a919e87dbdcf76e2f3071562af.png)


### 关于warp解锁教程

目前加了openai和奈飞，默认使用warp v6解锁，个人测试下来解锁的很舒畅。

[warp解锁参考文章](https://github.com/chika0801/sing-box-examples/blob/main/wireguard.md)

如需添加其他分流网站，**建议手动修改配置文件**，更加灵活，搭配1.8.0的碎片geo singbox，个性化更高，教程如下：

<details>
  <summary>点击展开/折叠</summary>
  
```bash
  
nano /root/sbox/sbconfig_server.json

```

修改route 块下的内容，比如添加一个pornhub的例子：
```json
      "final": "direct", 
      "rules": [
        {
          "rule_set": ["geosite-openai","geosite-netflix"]
          "outbound": "warp-IPv6-out"
        },
        {
          "rule_set": "geosite-netflix",
          "outbound": "warp-IPv6-out" 
        },
        { //此处为添加内容********，或者在上面的数组中添加，rule_set对应下面tag
          "rule_set": "geosite-pornhub",
          "outbound": "warp-IPv6-out" 
        },
        {//域名关键字触发，包含这个关键字
          "domain_keyword": [
            "ipaddress"
          ],
          "outbound": "warp-IPv6-out" //可改为warp-IPv4-out
        }
      ],
      "rule_set": [
        { //照虎画猫，srs文件仓库推荐（https://github.com/MetaCubeX/meta-rules-dat/tree/sing/geo/geosite），只需复制下面的样式，修改xxx.srs即可
          "tag": "geosite-openai",
          "type": "remote",
          "format": "binary",
          "url": "https://testingcf.jsdelivr.net/gh/MetaCubeX/meta-rules-dat@sing/geo/geosite/openai.srs",
          "download_detour": "direct"
        },
        {
          "tag": "geosite-netflix",
          "type": "remote",
          "format": "binary",
          "url": "https://testingcf.jsdelivr.net/gh/MetaCubeX/meta-rules-dat@sing/geo/geosite/netflix.srs",
          "download_detour": "direct"
        },
        {
          "tag": "geosite-disney",
          "type": "remote",
          "format": "binary",
          "url": "https://testingcf.jsdelivr.net/gh/MetaCubeX/meta-rules-dat@sing/geo/geosite/disney.srs",
          "download_detour": "direct"
        },
        { //此处为添加内容******，tag对应上面
          "tag": "geosite-pornhub",
          "type": "remote",
          "format": "binary",
          "url": "https://testingcf.jsdelivr.net/gh/MetaCubeX/meta-rules-dat@sing/geo/geosite/pornhub.srs",
          "download_detour": "direct"
        }
      ]
      
```
</details>


## Credit
- [sing-box-example](https://github.com/chika0801/sing-box-examples)
- [sing-reality-box](https://github.com/deathline94/sing-REALITY-Box)
- [sing-box](https://github.com/SagerNet/sing-box)


## 尝鲜区
### tcp-brutal reality(双端sing-box 1.7.0及以上可用)，暂时没添加warp分流功能，~~好像没啥人需要这个功能~~

[文档](https://github.com/apernet/tcp-brutal/blob/master/README.zh.md)

```bash
bash <(curl -fsSL https://github.com/vveg26/sing-box-reality-hysteria2/raw/main/tcp-brutal-reality.sh)
```

