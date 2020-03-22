## 22.03.2020更新
本地，远程脚本均可用；

[仓库](https://github.com/limbopro/Script)新增加 `unblockremote.js`，以简化 QuantumultX 1.0.3 配置`设备ID`流程，最终使得  [rewrite_remote] `远程`引用`脚本配置文件`可用：(`https://raw.githubusercontent.com/NobyDa/Script/master/QuantumultX/Js.conf`)；

`unblockremote.js` 脚本内容最开始是在联萌群看见，原作者暂无出处，欢迎提醒更正。

亲测教程有效； 

以下为具体教程：

### 第一步 fork 本仓库
`fork` https://github.com/limbopro/Script ；

*如果是很久之前就已经 fork 了的小伙伴，且又不想学习 [Github进行fork后如何与原（上游仓库）仓库同步？](https://limbopro.xyz/archives/3856.html#fork后如何同步上游仓库新更新内容？) ，或者 fork 了 https://github.com/NobyDa/Script ，请务必参考：https://github.com/limbopro/Script 该仓库的内容结构，在你 Fork 后的仓库下新建 `unblockremote.js`：

![unblockremote][1]


  [1]: https://raw.githubusercontent.com/limbopro/Script/master/unblockremote.png

`unblockremote.js` 内容为：

```
var body = $response.body;
body = '\/*\n@supported 你的QuantumultX设备ID填这里\n*\/\n' + body;
$done(body);
```

### 第二步 修改 unblockremote.js

1.进入 `fork` 后的`仓库`，找到并修改 `unblockremote.js` 脚本文件； 2.填写你的`设备ID`；（`设备ID`在哪？进入QuantumltX，点击右下角三菱按钮，点击右上角 `...` 更多按钮，滑至底部`关于`，即可找到设备ID）；

```
var body = $response.body;
body = '\/*\n@supported 你的QuantumultX设备ID填这里\n*\/\n' + body;
$done(body);
```

### 第三步 使用WorkingCopy同步 fork 到本地
1. 修改好 `unblockremote.js` 脚本文件后；
2. 使用`WorkingCopy`App 将 fork 后的仓库同步到 `我的iPhone` - `Quantumult X` - `Scripts` - `NobyDa` 下；
3. 不会使用`WorkingCopy`App? 参考示例：[使用Workingcopy 同步仓库到手机本地示例](https://limbopro.xyz/archives/workingcopy.html#一个需求)；

### 第四步 配置 rewrite_local

编辑QuantumultX 配置文件（进入 `Quantumult X` App，点击右下角`三菱按钮`，找到`配置文件`模块，点击`编辑`），找到 [rewrite_local]，并在 [rewrite_local] 添加：

```
^https:\/\/(raw.githubusercontent|\w+\.github)\.(com|io)\/.*\.js$ url script-response-body NobyDa/unblockremote.js
```

添加后效果：

```
[rewrite_local]
^https:\/\/(raw.githubusercontent|\w+\.github)\.(com|io)\/.*\.js$ url script-response-body NobyDa/unblockremote.js
```

### 第五步 配置 hostname

编辑QuantumultX 配置文件（进入 `Quantumult X` App，点击右下角`三菱按钮`，找到`配置文件`模块，点击`编辑`），找到 `hostname =`，并在 `hostname =` 后面添加：`raw.githubusercontent.com, *.github.io,`

效果如下：

```
hostname = raw.githubusercontent.com, *.github.io, vsco.co, *.my10api.com, *googlevideo.com, api.termius.com, api*.tiktokv.com, api*.musical.ly, api*.amemv.com, aweme*.snssdk.com, api.weibo.cn, mapi.weibo.com, *.uve.weibo.com, mp.weixin.qq.com, api.bilibili.com, app.bilibili.com, *.zhihu.com, aweme*.snssdk.com, *.kuwo.cn, ios.xiaoxiaoapps.com, api*.tiktokv.com, *.musical.ly, *.amemv.com, mjappaz.yefu365.com, p.du.163.com, getuserinfo.321mh.com, getuserinfo-globalapi.zymk.cn, api-163.biliapi.net, ios.fuliapps.com, vsco.co, api.vnision.com, *.my10api.com, bd.4008109966.net, sp.kaola.com, r.inews.qq.com, apple.fuliapps.com, newdrugs.dxy.cn, bdapp.4008109966.net, app101.avictown.cc, api.hlo.xyz, api.ijo.xyz, www.luqijianggushi.com, account.wps.cn, u.kanghuayun.com, api.gyrosco.pe, api1.dobenge.cn, api.mvmtv.com, mitaoapp.yeduapp.com, origin-prod-phoenix.jibjab.com, www.3ivf.com, pay.guoing.com, p.doras.api.vcinema.cn, api.termius.com, mjappaz.yefu365.com, viva.v21xy.com, dida365.com, ticktick.com
```

### 第六步 引用远程JS.conf

1.复制`https://raw.githubusercontent.com/NobyDa/Script/master/QuantumultX/Js.conf`链接（或者你fork后的JS.conf也行）， 2.进入Quantumult X，点击右下角`三菱按钮`，找到`Rewrite`模块-点击` 引用`，粘贴刚刚复制的链接；

### 开玩

最后，进入 `Quantumult X` App，点击右下角`三菱按钮`，找到`Rewrite`模块，开启按钮，`MitM`模块，开启按钮
