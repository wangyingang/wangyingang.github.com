---
layout: post
title: goagent及浏览器配置
description: 
category: others
tags: [goagent]
pretty_print: true
---
## 写在前面的话 <small>关于goagent、<abbr title="Google App Engine">GAE</abbr></small>
说几句啰嗦的话，主要是为了让不太懂电脑的童鞋更容易理解。没兴趣可以直接跳到**[配置步骤](#configurations)**一节。

### 关于[goagent][]
> goagent是使用Python和Google Appengine SDK编写的网络软件，
> 可以运行在Windows/Mac/Linux/[Android][]/[iTouch][IOS]/[iPhone][IOS]/
> [iPad][IOS]/[webOS][]/[OpenWRT][]/[Maemo][]上
> <small><cite>goagent</cite>作者</small>

**这一看就知道是程序员写的话，太那个什么了。俺来通俗的解释一下。**

goagent就好比是由一个负责干活的民工和一个负责发号施令的助理组成的两人team。民工在一个国外叫<abbr title="Google App Engine">GAE</abbr>的工地上干活，而助理则根据Boss的意图对民工远程的发号施令。

**雇佣goagent team之前，Boss做事情是这样的：**

1. 干每件事情之前都必须向一个叫<abbr title="The Great FireWall of China">GFW</abbr>的安全监理打申请，说我想干吗干吗。
2. <abbr title="The Great FireWall of China">GFW</abbr>这丫比较操蛋，批不批准申请完全依据一个叫有关部门颁发的神秘飘忽行为规范手册，他有可能：
   * 这事儿没啥，批准放行。
   * 这事儿没戏，让你歇菜。
   * 这事儿尴尬，不能放明面儿说行还是不行。表面装傻充愣，暗地里使坏黄了你的好事。
   * 这事儿昨天行，今天不行了。因为早上有关部门有口头交代。
   * 这事儿看起来没啥，但保不齐和某事儿有关系，没功夫琢磨细想，直接让你歇菜。
3. Boss:"......"

**雇佣goagent team之后，Boss想干什么事情就变成：**

1. 有什么事情交代给小助理去办。
2. 助理跑去给<abbr title="The Great FireWall of China">GFW</abbr>打申请：我想给在<abbr title="Google App Engine">GAE</abbr>工地上干活的亲戚打个电话。
3. <abbr title="The Great FireWall of China">GFW</abbr>一听就皱眉头，丫知道<abbr title="Google App Engine">GAE</abbr>是个大工地，干活的中国乡亲太多了   ，要是明令禁止牵扯太大，何况就是打个电话也不违反有关部门的规定，只好准了。
4. 助理给民工电话：“Boss要这样那样”。
5. 民工在国外。人家那地界自由，想干嘛就干嘛，不需要打报告等审批什么的，一趟功夫就把事情干完了。
6. 民工打电话给助理，把结果告诉助理。
7. 助理再把结果告诉Boss。

聪明如你一定猜到了，助理就是运行在电脑/平板/手机上的`goagent客户端`，而民工就是运行在<abbr title="Goole App Engine">GAE</abbr>上的`goagent服务端`了。那么Boss是谁？别到处看啦，就是你。

可能你还有疑问，<abbr title="The Great FireWall of China">GFW</abbr>不会监听电话内容吗？要是内容敏感他一样可以掐了电话啊。没错，他的确可以这么干，不过监控电话内容是需要额外财力和精力的。只要不是知名人士，平时他也懒得管，睁眼闭眼就过去了。

你要真是知名人士，或者你就是小心谨慎帝怎么办？别急，goagent也有办法。助理和监工之间除了用普通电话以外，还可以用卫星电话，无非就是通话时间慢点而已。你需要做的就是吩咐助理用`HTTPS`给民工打电话，助理自然心领神会的使用`SSL`江湖切口与民工对话。<abbr title="The Great FireWall of China">GFW</abbr>监听时发现通话内容全是些“脸为什么这么黄？防风涂的蜡。为什么又变红了？精神焕发！”之类的话，这`公钥`跟`私钥`，哦，也就是解密的小本子只有助理和民工才有，他哪能搞得懂？登时傻了眼，只好悻悻然作罢。

### 关于[GAE][]
这个就好理解了，云概念已经深入人心。<abbr title="Google App Engine">GAE</abbr>是Google提供的一个`Paas`风格的云平台，你可以在之上部署基于`Java`、`Python`的应用程序，免费版的每天限定1G下行流量。我们之前一直在说的**民工**，即`goagent服务端`就是运行在之上的`Python`程序。

<div class="alert alert-block alert-info">
  <a class="close" data-dismiss="alert" href="#">×</a>
  <h4 class="alert-heading">请注意！</h4>
  未设密码的<strong>goagent服务端</strong>默认是开放的，也就是说只要有人知道该服务地址就可以使用。网上有些嗅探goagent服务的无聊程序，其行为有点类似于“蹭网”。为杜绝此类情况，所以我要求大家设置自己的密码并保管好，设置后只有知道其密码的客户端才能使用。
</div>
#<span id="configurations"/>
## 配置步骤 <small>安装部署goagent、配置浏览器</small>
终于说到正题了，回头一看，写了一堆blabla......难怪儿子老说我啰嗦，看来是真的。-_-!

其实配置真不怎么麻烦，概括起来也就三步：

### 1. 部署goagent服务端
这步我帮童鞋们已经做好，图懒省事的可以无视了。直接跳到[安装goagent客户端](#install_goagent_client)一节。

如果喜欢DIY，也可以自己来做。不过最好告诉我一声，我好释放相应的资源。推荐参考网易最近出的文章[iPad翻墙记][iPad_cross_wall]。唉，有点担心，连网易都出翻墙文章，<abbr title="The Great FireWall of China">GFW</abbr>不会对<abbr title="Google App Engine">GAE</abbr>和goagent加大打击力度吧？不管了，用一天是一天吧。

<div class="alert alert-block">
  <a class="close" href="#" data-dismiss="alert">×</a>
  <h4 class="alert-heading">请注意！</h4>
  <ul>
    <li>iPad翻墙记中goagent程序的下载地址不是官方地址，我建议不要轻易使用不被信任的下载源，推荐用<a href="https://code.google.com/p/goagent/">官方下载</a>。</li>
    <li>iPad翻墙记中上传goagent服务端一节没有提及设置密码，这样上传的服务端是有可能会被盗用的。设置密码需要进入解压目录下编辑<code>server\python\wsgi.py</code>文件的第<code>8</code>行，即<code>__password__</code>配置项。如图所示：<p><img src="/images/wsgi_password_setup.png"/></p></li>
  </ul>
</div>

如果你选择DIY，那么服务端客户端想必都已安好，直接跳到[配置浏览器](#configure_browsers)一节即可。

<span id="install_goagent_client"/>
### 2. 安装goagent客户端
1. 下载我在私信中告诉你的就行了，解压密码与你自己设定的goagent密码相同。

    <span class="label label-info">注意！</span>rar解压密码是很容易破解的，有些无聊程序能扫描到此链接。所以请尽快下载并在下载完毕后私信告知我，我会第    一时间删除此链接以确保密码安全。
2. 解压到任意目录后进入，找到`local\goagent.exe`文件，`Windows XP`的用户直接双击运行即可。`Windows7`的用户在第一次运行此程序时需使用管理员权限。点击    右键，选择“以管理员身份运行”。如图所示：
    
   ![win7第一次运行goagent](/images/win7_run_goagent.png)
3. 让goagent客户端程序每次开机后自动运行。找到`local\addto-startup.vbs`文件，双击后会出现一个确认窗口，点击确定即可。如图所示：
   
   ![开机自动运行goagent](/images/goagent_autorun.png)

   当然，如果不喜欢自动启动也可以不运行这个脚本，不过每次翻墙之前要记得双击运行`goagent.exe`启动客户端。

OK，安装完成，很简单不是？

<span id="configure_browsers" />
### 3. 配置浏览器
配置浏览器是为了让浏览器与goagent客户端一起协同工作。除此之外，我们还希望浏览器足够智能，能自动分辨出那些网站需要使用goagent代理，哪些则不需要，使翻墙无须人工干预实现自动化，上网体验更好。
#### Chrome浏览器
1. `Chrome`是使用goagent的首选浏览器，推荐[官方下载][Chrome]。
2. 安装完成后打开Chrome，安装[SwitchySharp][]插件。如图所示：

   ![安装SwitchySharp](/images/install_switchysharp.png)
3. 点击`ADDED TO CHROME`之后，`Chrome`会弹出确认对话框：

   ![安装SwitchySharp确认](/images/install_switchysharp_confirm.png)
4. 点击`添加`，`Chrome`安装`SwitchySharp`插件完成后会弹出一个选项标签页：

   ![第一次运行SwitchySharp](/images/switchysharp_first_run.png)
5. 不要急着设置`SwitchySharp`，先下载goagent官网提供的[配置文件][SwitchyOptions]，保存到本地。
6. 回到`SwitchySharp`选项标签页，选择`导入/导出`选项卡，再选择`从文件恢复`，选择上一步中下载的`SwitchyOptoins.bak`文件。如图所示：

   ![SwichySharp设置1](/images/switchysharp_setup_1.png)
7. 之后会弹出确认对话框，提示你是否需要恢复SwitchySharp配置，选择`确定`。
8. 导入完成后，你会发现`情景模式`中多了三种模式，你只需要确保`goAgent`模式处于选中状态即可。如图所示：

   ![SwichySharp设置2](/images/switchysharp_setup_2.png)
9. 切换到`切换规则`选项卡，注意下方的`在线规则列表`以及`AutoProxy 兼容列表`保持勾选状态，点`保存`。

   ![SwichySharp设置3](/images/switchysharp_setup_3.png)
   `在线规则列表`会动态更新，里面包含了<arrb title="The Great FireWall of China">GFW</abbr>最新的屏蔽网站列表。
10. 最后，点击在浏览器右上角地址栏后面跟着的一个`地球`按钮，将`SwitchySharp`设为`自动切换模式`，让浏览器自动选择是否采用`goagent`翻墙。如图所示：

   ![SwichySharp设置4](/images/switchysharp_setup_4.png)

至此，配置完成，快来试试[Youtube][]、[Twitter][]、[Facebook][]这些网站吧！
#### Firefox浏览器
[Firefox][]推荐[官方下载][Firefox_download]，安装完成之后推荐安装[FoxyProxy][]插件。

我机器上没装`Firefox`，就不给大家演示安装步骤了，请自行Google相关教程。这里只说几点注意事项：

* `Firefox`需导入证书，否则无法登录[Twitter][]/[Facebook][]。

   <span class="label label-info">导入方法</span> 打开`Firefox`->`选项`->`高级`->`加密`->`查看证书`->`证书机构`->`导入证书`，选择`local\ca.crt`，勾选所有项，导入。
* `Firefox`访问敏感网站链接被重置是因为`DNS劫持`，具体方法是使用远程`DNS`。

   <span class="label label-info">使用远程DNS</span> 打开`Firefox`->在地址栏输入`about:config`->搜索`network.proxy.socks.remote_dns`->将值修改为`true`。

#### IE浏览器
好吧，如果你坚持用`IE`浏览器，我也就写写怎么配置。`IE`没有插件机制，有两种配置方式，一种针对直接拨号，也就是电脑直接通过<abbr title="Asymmetric digital subscriber line">ADSL</abbr> Modem上网；另一种针对局域网，也就是电脑通过在局域网内通过`集线器`或`路由器`上网。

* 直接拨号上网方式。
  1. 打开`IE`浏览器->`工具`->`Internet选项`->`连接`选项卡->`拨号和虚拟专用网络设置`，选中<abbr title="Asymmetric digital subscriber line">ADSL</abbr>
     类型的拨号连接，这个拨号连接有可能叫`我的宽带`，也可能叫`宽带我世界`，还有可能与你的上网账号有关，总之不要弄错。如图所示：

     ![ie拨号上网配置1](/images/ie_directly_dial_setup1.png)
  2. 点击`设置`之后，弹出对话框，按图中所示进行设置。

     ![ie拨号上网配置2](/images/ie_directly_dial_setup2.png)

* 局域网上网方式。
  1. 打开`IE`浏览器->`工具`->`Internet选项`->`连接`选项卡->`局域网设置`，如图所示：

     ![ie局域网上网配置1](/images/ie_lan_setup1.png)
  2. 点击`局域网设置`之后，弹出`局域网(LAN)设置`对话框，设置内容与`直接拨号上网方式`中的第`2`步类似，不再复述。

     ![ie局域网上网配置2](/images/ie_lan_setup2.png)

至此，`IE`配置完成。

<div class="alert alert-block">
  <a class="close" href="#" data-dismiss="alert">×</a>
  <h4 class="alert-heading">IE浏览器启用代理服务的缺点</h4>
  <ul>
    <li>访问的所有站点都通过代理，甚至是国内合法站点。这样肯定没有直接访问快，还浪费goagent流量。暂停使用代理时需手动进入原来配置的地方取消勾选，要实现自动切换需编写较为复杂的<code>pac</code>脚本，实在是不值当。</li>
    <li>有些通讯软件默认使用<code>IE</code>的上网设置，例如<code>MSN</code>/<code>QQ</code>等，当启用代理时，这些软件可能不能正常工作。</li>
  </ul>
</div>

[goagent]: https://code.google.com/p/goagent/
[Android]: http://code.google.com/p/gaeproxy "goagent Android客户端"
[IOS]: https://code.google.com/p/goagent/wiki/GoAgent_IOS "goagent IOS客户端"
[webOS]: https://code.google.com/p/goagent/wiki/GoAgent_webOS "goagent webOS客户端"
[OpenWRT]: https://code.google.com/p/goagent/wiki/GoAgent_OpenWRT "goagent OpenWRT客户端"
[Maemo]: https://code.google.com/p/goagent/wiki/GoAgent_Maemo "goagent Maemo客户端"
[GAE]: https://developers.google.com/appengine/ "Google App Engine"
[iPad_cross_wall]: http://digi.163.com/photoview/4R7Q0016/184040.html "iPad翻墙记"
[Chrome]: https://www.google.com/intl/en/chrome/browser/ "Chrome浏览器"
[Firefox]: http://firefox.com.cn/ "火狐浏览器"
[Firefox_download]: http://download.firefox.com.cn/releases/webins3.0/official/zh-CN/Firefox-latest.exe "Firefox官方下载地址"
[SwitchySharp]: https://chrome.google.com/webstore/detail/dpplabbmogkhghncfbfdeeokoefdjegm "SwitchySharp插件"
[SwitchyOptions]: http://goagent.googlecode.com/files/SwitchyOptions.bak "SwitchySharp配置文件"
[FoxyProxy]: https://addons.mozilla.org/zh-cn/firefox/addon/foxyproxy-standard/
[Youtube]: https://www.youtube.com
[Twitter]: https://twitter.com
[Facebook]: https://facebook.com
