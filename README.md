# 利用高校IPv6免流机制实现无限流量，科学上网，不限设备

## 特别鸣谢

   **特别感谢Nginx大佬对我的指导和帮助，没有他的悉心指导，我绝对完成不了这个项目，同时他也是一位up主，大家可以去关注他的[账号](https://space.bilibili.com/501725110?spm_id_from=333.337.0.0)**

## 引言

  众所周知，在我国高校中均已普及了IPV6，而且IPV6通常拥有更快的速度，仅以我校（CAU）为例，校园网计费仅计算IPv4下行流量，不计IPv4上行流量和IPv6上行和下行流量。于是利用这个特点，我们可以通过仅上传IPv4流量而接收IPv6流量来实现免流，而且IPv6通常也意味着更快的速度[^1]同时来实现科学上网。  
  ~~**孙亏科技最新力作，致力于实现让学校亏钱的技术，谁让他byd敢在厕所里装水表。**~~  

## 原理

利用VPS[^2]技术，本地通过IPv6协议与VPS进行数据请求，VPS在网络上找到你想要的资源，然后下载到VPS，再通过IPv6把你想要的数据发给你。相当于你与互联网的数据交互完全是走IPv6的，所以就不消耗IPv4流量。同时，如果你的VPS在海外，那么你也可以通过VPS进行科学上网，相当于开了一个VPN。  

## 软件和环境准备

* [一个提供VPS服务的平台](https://my.vultr.com/)
* [一个能充当机场的软件](https://github.com/2dust/v2rayN/releases)
* [操作用软件](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html)
* 大约50min的时间

## 具体步骤

1. 有很多云服务平台都提供VPS服务，为了实现科学上网我们选择国外的平台，一个是[Google](https://cloud.google.com/)的，送300刀乐的免费额度，但是需要visa借记卡，鉴于国内大学生基本都没资格拿到卡，所以我们选择[Vultr](https://my.vultr.com/)，一是支持支付宝付款，二是便宜，宿舍六个人合租均下来每个人一个月就三块，非常划算。三是支持90天内退款，就算不成功也只有时间成本。
2. 按以下步骤进行配置，[链接](https://www.jixing.one/vps/get-a-vps/)。
3. 注：不要按网站中的链接下载V2rayN，否则可能会在接下来以下步骤出现问题，请按我提供的链接下载。

## 可能存在的问题以及解决方案

1. Q：安装软件以后无法打开微软系列所有UWP应用（包括Xbox）？  
   A：这是由于微软为了安全，把所有UWP应用都隔离起来，使用全局代理无效。解决方案如下：  
   ![打开V2R](https://s2.loli.net/2024/08/29/aPtUpi7IJgYrdsb.png)

2. Q：一些下载器（如IDM）无法正常使用？  
   A：以IDM为例，按以下步骤设置：  
   ![IDM1.png](https://s2.loli.net/2024/08/29/o2nMpZD4qSL9IsA.png)
   ![IDM2.png](https://s2.loli.net/2024/08/29/ulY7OXdjgHqzEtn.png)

3. Q：配置成功以后，可以打游戏吗？  
   A：由于数据需要走两遍，就算是距离比较近的日本，延迟也比较感人，建议在玩联机游戏时候，关掉代理，使用免费流量，或者使用路由模式（就是虚拟网卡版本的）加速器进行游玩，下面是CAU宿舍内无线网络连接的情况：  
   ~~甚至外网的访问速度比国内还快，所以推荐使用谷歌。~~
   ![speed.png](https://s2.loli.net/2024/08/29/Ht5JDLYO274QAsP.png)

4. Q：由于全局代理，海外IP对于国内一些软件比（如B站）无法访问某些信息，这个如何解决？  
   ~~**那我缺的4K番剧这方面谁给我补啊**~~  
   A:这是因为B站有些东西是只有大陆地区才能观看的，我们需要绕过B站的IP检测：  
   ~~我说B站程序员这么多的域名你们自己分得清楚哪个是干嘛的吗？让我一个一个测这么久~~
   点开V2R，按以下步骤设置，<u>记得将直连规则移动至最上层，否则设置无效。</u>  

``` html
  search.bilibili.com,
  api.bilibili.com
```

![direct1.png](https://s2.loli.net/2024/08/30/i7j5XLkPK3TONVQ.png)
![direct2.png](https://s2.loli.net/2024/08/30/KlLDZvuXB6qsYxf.png)
![direct3.png](https://s2.loli.net/2024/08/30/na7s1XMAxzqlLWO.png)
![direct4.png](https://s2.loli.net/2024/08/30/dusN9Cb5g72nQO4.png)
![direct5.png](https://s2.loli.net/2024/08/30/fKVWCHBangYqiJ2.png)

**成功**
![success.png](https://s2.loli.net/2024/08/30/VQOzt4vT3mhRekY.png)

## 暂未解决的问题

* [ ] 在使用这个方法后，校内平台有时候出现无法连接的情况，多次刷新即可解决，原因不明，推测可能是校内服务器太垃圾的缘故。

### 如果您从中受益，别忘了给我点一个star，感谢您的支持，如果您发现了某些问题，请及时向我提交issue，我会尽力解决

[^1]: CAU里有线最快为1000Mbps，无线为50Mbps。  
[^2]:VPS（Virtual Private Server 虚拟专用服务器）技术，将一台服务器分割成多个虚拟专享服务器的优质服务。在容器或虚拟机中，每个VPS都可选配独立公网IP地址、独立操作系统、实现不同VPS间磁盘空间、内存、CPU资源、进程和系统配置的隔离，为用户和应用程序模拟出“独占”使用计算资源的体验。
