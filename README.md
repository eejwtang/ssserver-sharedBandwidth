# ssserver-sharedBandwidth

> 共享带宽，加速实验室网络

突破实验室Dr.com环境下给每个IP只分配4M带宽的限速

shadowsocks、shadowsocks-libqss、winsw。

# 服务端和客户端安装配置

## 配置服务端
1. 快捷键win+q输入cmd以管理员身份运行,进入希望存放的目录后输入如下命令
2. git clone https://github.com/eejwtang/ssserver-sharedBandwidth.git
3. cd ssserver-sharedBandwidth
4. ssserversw install 
5. ssserversw start
6. 设置shadowsocks-libqss防火墙：
	控制面板-->系统和安全-->Windows Defender 防火墙-->允许应用或功能通过 Windows Defender 防火墙-->更改设置-->找到shadowsocks-libqss将专用公用的勾打上-->确定即可

## 配置客户端

1. 打开shadowsocks客户端，添加局域网内已经搭建好的ss服务器地址
2. 右击shadowsocks客户端，选择服务器负载均衡。

### URL List
ss://cmM0LW1kNTpiYXJmb28hQDEwLjEyLjE0LjIxOjEyMTk5#21
ss://cmM0LW1kNTpiYXJmb28hQDEwLjEyLjEzLjE4ODoxMjE5OQ==#fws
ss://cmM0LW1kNTpiYXJmb28hQDEwLjEyLjEzLjE5OToxMjE5OQ==#yzh
ss://cmM0LW1kNTpiYXJmb28hQDEwLjEyLjEzLjc1OjEyMTk5#jwtang
ss://cmM0LW1kNTpiYXJmb28hQDEwLjEyLjEzLjE3NToxMjE5OQ==#yeq
ss://cmM0LW1kNTpiYXJmb28hQDEwLjEyLjEzLjE5OjEyMTk5#zham

# 实现过程

## 思路
学校实验室通过Dr.com的方式认证上网，并且给每个账号只分配了独立的4Mb的带宽，实验室有25个人就有25个4M带宽，浏览网页、简单的下载都只有500Kb/s左右的速度，和寝室里的百兆带宽比起来真的是捉襟见肘。我们想能不能吧这20条4Mbps的小溪并到一起，合成一条所有人可以共享的100Mbps的大江，愉快地科研。

shadowsocks是一种基于Socks5代理方式的加密传输协议，不仅仅可以科学上网，用作Socks5代理也很实用。因为局域网内每台PC都可以相互连通，给每台电脑都搭一个ss服务端开启socks5代理，同时安装客户端设置负载均衡，可以很方便明显地实现带宽提速。

## 工具
- libQtShadowsocks:
	windows下搭建ss服务端,这个项目非常棒——[libQtShadowsocks](https://github.com/shadowsocks/libQtShadowsocks)。这是一个轻量级的shadowsocks库，不用搭建Python环境
- WinSW:
	WinSW可以让任何Windows程序都能运行为服务，方便管理及稳定运行，配置服务端的[3-5]就是讲winsw注册为服务。

## TODO
- 目前科学上网的流量还不能代理提速
- 还存在安全性的问题

## Reference：
- [Windows下三分钟搭建Shadowoscks服务器端](https://www.librehat.com/three-minutes-to-set-up-shadowsocks-server-on-windows/)
- [GitHub-libQtShadowsocks](https://github.com/shadowsocks/libQtShadowsocks)
- [GitHub-WinSW](https://github.com/kohsuke/winsw)
