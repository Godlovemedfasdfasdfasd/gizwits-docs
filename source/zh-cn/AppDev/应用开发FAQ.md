title:  应用开发FAQ
---


# 1、概述
本文列举了开发者在使用机智云app、开源框架、app自动生成或者进行SDK集成的时候所遇到的一些问题以及解答方案。

# 2、FAQ

**Q：配置失败，设备配不上网，App显示配置超时**
A： 设备配网涉及到App以及设备端，以下列出会导致该问题发生的情况或解决方案。
- 1、使用机智云app进行配置（机智云app下载地址：https://download.gizwits.com/zh-cn/p/98/99）。
- 2、配置时确认将要配置的网络和手机所链接的网络是否为同一个，确认路由器SSID和密码是否输入正确，确认配置时所选用的模组型号正确。
- 3、将要配置的路由器不能是5G频段的wifi，不能有链接登陆限制、不可开启ap隔离，尝试更换wifi路由器，或用手机热点作为路由器，不建议使用公共或进行了端口限制的路由器进行配置。
- 4、判断设备是否进入了相应的配置模式，通过模组的debug口的输出日志，查看模组是否进入配网模式（抓取日志链接：http://docs.gizwits.com/zh-cn/deviceDev/%E9%80%9A%E8%AE%AF%E6%A8%A1%E7%BB%84%E8%B0%83%E8%AF%95%E6%97%A5%E5%BF%97%E6%8A%93%E5%8F%96%E6%95%99%E7%A8%8B.html）

**Q：App配置成功了，但是设备没有显示**
A：使用开源框架、App自动生成所编译出来的App，确认App工程目录中的assets/UIConfig.json，product key是否与自己设备一致。

**Q：使用开源框架或自动生成出来的App，注册账号显示“未知错误”**
A：那是因为注册的时候采用了弱密码导致的，注册需要采用强密码注册，密码由大写，小写，数字和特殊符号组成，四个条件至少满足三个即可

**Q：为什么在机智云App上注册的账户，不能在开源框架或自动生成出来的App登陆，登陆显示账号密码错误**
A：那是因为机智云App和开源框架还有自动生成的app不具备同一个appid，用户系统也不同，如需要在各自的App上登陆，同时也要在该App上注册用户。

**Q：机智云App显示“未知设备\不支持该设备\下载配置文件失败”是什么？怎么处理？**
A：IOE Demo加载了设备列表以后，会自动下载设备的配置文件，SDK通过该配置文件进行JSON和二进制数据的解析，这样才能正确的控制设备和获取设备状态。如果IOE Demo因为网络问题未下载到对应设备的配置文件，或者云端无法找到该设备的配置文件，就会出现该句提示，或者提示“下载配置文件失败”。

**Q：开源App要怎样改动才能控制我的设备？**
A：关键步骤有三步，推荐采用自动生成App，可以省略前两步：
- 1、修改源码的ProductKey和AppID与自己的设备一致。
- 2、修改源码的数据点标识名与自己的设备一致。
- 3、根据自己的设备功能修改UI。

**Q：Demo App如何下载？是通用的吗？**
A：Demo App可通过机智云下载中心下载或者是在手机应用商店搜索“机智云”。因为Demo App做了界面空间和通讯协议自适应，所以机智云平台上的所有产品用的都是同一个Demo App，不需要另外下载。

**Q：微信开发要用个人公众号还是企业公众号？**
A：微信公众号分为服务号、订阅号、企业号。设备功能目前是微信服务号的一个插件功能，开通设备功能前需要先申请开通服务号。未认证的服务号也可以开通设备功能，但对接入设备的数量有严格限制。因此， 未认证的服务号开通设备功能后，需要尽快通过服务号认证，以提高接入设备限额。因为服务号目前不向个人开放申请，个人开发者可以使用测试账号来完成开发调试。详情可参考微信官方说明

**Q：机智云怎样判断当前模块和终端是局域网还是广域网，要理论** 
A：手机SDK里面是这样判断的：SDK每隔1秒会在局域网发出广播包，模组如果在局域网的话，收到了广播包就会给SDK回复passcode，这时候SDK就能通过passcode来登录设备了。如果SDK收不到回复，就会判断设备列表里面的设备是远程的，会通过广域网查询设备状态。
