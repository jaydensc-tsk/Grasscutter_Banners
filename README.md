# Grasscutter_Banners|割草机卡池文件

Json file collection for Grasscutter gacha Banners

收集各版本割草机的卡池Json文件。

使用说明：

下载一个你想要使用的卡池文件，把它放在`grasscutter/data`文件夹里并将其重命名为`Banners.json`，然后在游戏中使用`/reload`指令即可重新加载卡池文件使其生效。

欢迎提交pr！

to use the banners, select the one you want to use and place it inside "grasscutter/data" folder on your server installation.

Remember to rename it to "Banners.json"

Use "/reload" command in game to reload the banners.

You're all welcome to submit a pull request and make a change on the project.

---

### 文件命名说明：
正常来说都以`Banners` + `大版本名称` + `.` + `这个大版本内的卡池序号` + `.json`来命名。

一般来说原神每个版本分上半和下半两个卡池，所以这种情况下.1代表上半卡池，.2则代表下半卡池。比如4.0上半卡池叫做`Banners4.0.1.json`，下半卡池叫做`Banners4.0.2.json`

当然也存在特殊情况，比如原神1.3版本就有三个角色卡池，所以他们分别叫做`Banners1.3.1.json`、`Banners1.3.2.json`和`Banners1.3.3.json`。

`BannersFull.json`是全卡池文件*，汇总了包括新手祈愿、两个常驻祈愿和所有版本的角色和武器活动祈愿的卡池，由于一个卡池文件中`scheduleId`不能重复否则只会加载其中的一个，所以里面的`scheduleId`都按顺序排号了，其它的信息都和单独版本的卡池文件一致。

*注意：为确保卡池数据的稳定性，全卡池文件`BannersFull.json`仅会在游戏中验证完成可用性和正确性之后才会更新，由于Grasscutter可能不会每个版本都更新，所以全卡池文件可能不包含最新的卡池数据。
您可以手动从对应版本的卡池文件里复制到全卡池文件里手动添加。

---

### 卡池文件内容说明
正常情况下卡池是json文件格式，里面包含了一个由`[` `]`方括号括起来的列表。列表里包含了几个用一对`{` `}`大括号框起来的卡池对象，他们之间用`,`逗号隔开。

以下是每一个卡池对象中属性字段的说明。

**`comment`**: 

注释，通常来说我会写上版本号加上这一个卡池的五星角色的英文名字以便我合并卡池的时候加以区分。武器池我会直接写版本号。`Standard Wish`表示这是常驻池，`Beginner's Banner`是新手池。

**`gachaType、prefabPath、titlePath`**:

分别代表卡池类型代号、卡池界面图片代号和卡池标题代号，可以查阅下面后记中的表格获得。其中有一些规律推测未来的卡池代号也写在了后记里，可以看看下面的内容。


**`scheduleId`**:

同一个卡池文件里`scheduleId`必须唯一，否则相同`scheduleId`的卡池只会加载其中的一个。

**`sortId`**:

和卡池在界面上显示的左右顺序（或者手机上是上下顺序）有关系，可以重复。

**`costItemId`**:

抽卡所消耗的物品的id，粉球纠缠之缘是223，蓝球相遇之缘是224。
当然你也可以试着改成摩拉风之印原石之类的id。

**`endTime`**:

卡池的结束时间的时间戳，可以在某些在线时间戳转换网站上转换为年月日时分秒的日期时间的形式。
默认为1924992000也就是2031年1月1日0点0分0秒（0时区|国际标准时间）或者当天8点（东八区|北京时间）

**`rateUpItems4、rateUpItems5`**:

分别为四星up的id列表和五星up的id列表，角色一般为4位数字，武器一般为5位数字。
似乎可以改成普通物品或者圣遗物的id。

**`fallbackItems`**:

（我还没搞明白）似乎是可能歪到的角色或者武器的id列表，删掉这些字段之后卡池应该也可以正常使用。

**`weights4、weights5`**:

分别代表四星和五星的权重（抽卡概率相关）。
```json
  "weights4":[[1,510],[8,510],[10,10000]],
  "weights5":[[1,80],[73,80],[90,10000]],
```
比如五星的权重，上述片段表示1-73抽中每一抽你都有0.8%的概率抽到五星角色，73-90抽概率从0.8%逐渐上升到100%，直到你抽出来了五星角色为止。

**`poolBalanceWeights4、poolBalanceWeights5`**:

和`weights`类似，用于实现保底机制的另一个概率参数，如果是四星的话表示如果你一发十连没抽到up的四星的话下一发十连的四星一定会有一个up的四星。
同时也实现了五星的大保底，如果90抽出金歪了那么到180抽一定会抽到up的五星。

**`"costItemAmount10": 8`**:

新手池的特殊字段，表示十连抽只消耗8抽的东西。

**`"gachaTimesLimit": 20`**:

新手池的特殊字段，表示新手池最多只能抽20发。

---

## Thanks|鸣谢:

[https://github.com/davidbeltrane01/grasscutters_banners_json](https://github.com/davidbeltrane01/grasscutters_banners_json)

[https://github.com/KeyPJ/genshin-gacha-banners](https://github.com/KeyPJ/genshin-gacha-banners)

[https://github.com/Grasscutters/Grasscutter](https://github.com/Grasscutters/Grasscutter)

[https://github.com/jie65535/GrasscutterCommandGenerator](https://github.com/jie65535/GrasscutterCommandGenerator)

## 后记：

修卡池的时候发现了一些经验。

如果卡池出现类似A022的字样不正常的时候，可能是gachaType写错了，需要修改正确之后才能显示。

以下是我尝试之后的可能结果，可能不一定准确但是这样确实外表看上去就是对的

（后来参考了[https://github.com/sunfkny/genshin-gacha-export/blob/main/gacha_metadata.py](https://github.com/sunfkny/genshin-gacha-export/blob/main/gacha_metadata.py)里面确认了就是这几个代号）

| gachaType | 卡池类型 |
|-----------|-----------|
|100 |初行祈愿|
|200 |常驻祈愿|
|301 |角色活动祈愿1|
|302 |武器活动祈愿|
|400| 角色活动祈愿2|


另外gachaType写对之后还可能出现卡池的标题消失的情况，这时候可能是titlePath的编号不对导致的。

比如2.1上半

"prefabPath":"GachaShowPanel_A054",

"titlePath":"UI_GACHA_SHOW_PANEL_A020_TITLE",

这里的titlePath里面必须是A020才能正确显示出“神铸赋形”这个武器池的标题，如果惯性思维还是填A054的话会导致标题区域空白

（众所周知prefabPath是控制卡池封面的，titlePath是控制卡池标题的）

### 后续发现了一些规律：
关于卡池prefabPath代号和titlePath的规律：

A016初行祈愿，A017原神1.0常驻池，A022常驻池

除了这三个卡池外大致遵循以下规律：

①每个大版本的卡池为连续的prefabPath编号，prefabPath编号和上一个版本的最后一个prefabPath编号是接着的

②2.3版本之前编号按照上半角色-下半角色-上半武器-下半武器的顺序。2.3版本第一次加入角色活动祈愿2，大致也是之前的规律，
2.3之后的版本顺序变成了上半角色-上半武器-下半角色-下半武器。如果有两个角色up则先为角色活动祈愿1再编号角色活动祈愿2

③有关titlePath，如果是武器池的titlePath都是一样的A020（武器池的标题全都是神铸赋形），角色池看是不是第一次up，如果是第一次up则与prefabPath的编号保持一致，如果是复刻则与该角色第一次up的prefabPath保持一致
此外，如果编号大于100，titlePath需要多加一个0，比如妮露的prefabPath是A100，那她的titlePath是A0100而不是A100

以下是总结出的表格：
titlePath留空表示是首次up，值与prefabPath一致（100以后的编号需要在前面加一个0）
| prefabPath | titlePath | 五星up          | 卡池类型 | gachaType | 版本号   |
|------------|-----------|-----------------|----------|-----------|-------|
| Default    | Default   |                 |  施工中  |           |       |
| A016       |           | 初行祈愿          | 初行   | 100       | 1.0.1 |
| A017       |           | 常驻卡池          | 常驻   | 200       | 1.0.1 |
| A018       |           | 可莉            | 角色1  | 301       | 1.0.2 |
| A019       |           | 温迪            | 角色1  | 301       | 1.0.1 |
| A020       | A020      | 阿莫斯/风鹰剑       | 武器   | 302       | 1.0.1 |
| A021       | A020      | 四风原典/狼末       | 武器   | 302       | 1.0.2 |
| A022       |           | 常驻卡池          | 常驻   | 200       | 1.1.1 |
| A023       |           | 达达利亚          | 角色1  | 301       | 1.1.1 |
| A024       |           | 钟离            | 角色1  | 301       | 1.1.2 |
| A025       | A020      | 天空之翼/尘世之锁     | 武器   | 302       | 1.1.1 |
| A026       | A020      | 贯虹/无工         | 武器   | 302       | 1.1.2 |
| A027       |           | 阿贝多           | 角色1  | 301       | 1.2.1 |
| A028       |           | 甘雨            | 角色1  | 301       | 1.2.2 |
| A029       | A020      | 斫峰之刃/天空之卷     | 武器   | 302       | 1.2.1 |
| A030       | A020      | 阿莫斯/天空之傲      | 武器   | 302       | 1.2.2 |
| A031       |           | 魈             | 角色1  | 301       | 1.3.1 |
| A032       |           | 刻晴            | 角色1  | 301       | 1.3.2 |
| A033       |           | 胡桃            | 角色1  | 301       | 1.3.3 |
| A034       | A020      | 磐岩结绿/和璞鸢      | 武器   | 302       | 1.3.1 |
| A035       | A020      | 护摩/狼末         | 武器   | 302       | 1.3.3 |
| A036       | A019      | 温迪            | 角色1  | 301       | 1.4.1 |
| A037       | A023      | 达达利亚          | 角色1  | 301       | 1.4.2 |
| A038       | A020      | 终末/天空之刃       | 武器   | 302       | 1.4.1 |
| A039       | A020      | 天空之翼/四风原典     | 武器   | 302       | 1.4.2 |
| A040       | A024      | 钟离            | 角色1  | 301       | 1.5.1 |
| A041       |           | 优菈            | 角色1  | 301       | 1.5.2 |
| A042       | A020      | 斫峰之刃/尘世之锁     | 武器   | 302       | 1.5.1 |
| A043       | A020      | 松籁/风鹰剑        | 武器   | 302       | 1.5.2 |
| A044       | A018      | 可莉            | 角色1  | 301       | 1.6.1 |
| A045       |           | 万叶            | 角色1  | 301       | 1.6.2 |
| A046       | A020      | 四风原典/天空之傲     | 武器   | 302       | 1.6.1 |
| A047       | A020      | 天空之卷/苍古       | 武器   | 302       | 1.6.2 |
| A048       |           | 神里绫华          | 角色1  | 301       | 2.0.1 |
| A049       |           | 宵宫            | 角色1  | 301       | 2.0.2 |
| A050       | A020      | 雾切/天空之脊       | 武器   | 302       | 2.0.1 |
| A051       | A020      | 飞雷/天空之刃       | 武器   | 302       | 2.0.2 |
| A052       |           | 雷电将军          | 角色1  | 301       | 2.1.1 |
| A053       |           | 珊瑚宫心海         | 角色1  | 301       | 2.1.2 |
| A054       | A020      | 无工/薙刀         | 武器   | 302       | 2.1.1 |
| A055       | A020      | 月华/磐岩结绿       | 武器   | 302       | 2.1.2 |
| A056       | A023      | 达达利亚          | 角色1  | 301       | 2.2.1 |
| A057       | A033      | 胡桃            | 角色1  | 301       | 2.2.2 |
| A058       | A020      | 冬极/尘世之锁       | 武器   | 302       | 2.2.1 |
| A059       | A020      | 护摩/终末         | 武器   | 302       | 2.2.2 |
| A060       | A027      | 阿贝多           | 角色1  | 301       | 2.3.1 |
| A061       |           | 荒泷一斗          | 角色1  | 301       | 2.3.2 |
| A062       | A041      | 优菈            | 角色2  | 400       | 2.3.1 |
| A063       | A020      | 苍古/松籁         | 武器   | 302       | 2.3.1 |
| A064       | A020      | 赤角石溃杵/天空之翼    | 武器   | 302       | 2.3.2 |
| A065       |           | 申鹤            | 角色1  | 301       | 2.4.1 |
| A066       | A031      | 魈             | 角色2  | 400       | 2.4.1 |
| A067       | A020      | 息灾/和璞鸢        | 武器   | 302       | 2.4.1 |
| A068       | A024      | 钟离            | 角色1  | 301       | 2.4.2 |
| A069       | A028      | 甘雨            | 角色2  | 400       | 2.4.2 |
| A070       | A020      | 贯虹/阿莫斯        | 武器   | 302       | 2.4.2 |
| A071       |           | 八重神子          | 角色1  | 301       | 2.5.1 |
| A072       | A020      | 神乐/磐岩结绿       | 武器   | 302       | 2.5.1 |
| A073       | A052      | 雷电将军          | 角色1  | 301       | 2.5.2 |
| A074       | A053      | 珊瑚宫心海         | 角色2  | 400       | 2.5.2 |
| A075       | A020      | 薙刀/月华         | 武器   | 302       | 2.5.2 |
| A076       |           | 神里绫人          | 角色1  | 301       | 2.6.1 |
| A077       | A019      | 温迪            | 角色2  | 400       | 2.6.1 |
| A078       | A020      | 终末/月白         | 武器   | 302       | 2.6.1 |
| A079       | A048      | 神里绫华          | 角色1  | 301       | 2.6.2 |
| A080       | A020      | 雾切/无工         | 武器   | 302       | 2.6.2 |
| A081       |           | 夜兰            | 角色1  | 301       | 2.7.1 |
| A082       | A031      | 魈             | 角色2  | 400       | 2.7.1 |
| A083       | A020      | 若水/和璞鸢        | 武器   | 302       | 2.7.1 |
| A084       | A061      | 荒泷一斗          | 角色1  | 301       | 2.7.2 |
| A085       | A020      | 赤角石溃杵/尘世之锁    | 武器   | 302       | 2.7.2 |
| A086       | A045      | 万叶            | 角色1  | 301       | 2.8.1 |
| A087       | A018      | 可莉            | 角色2  | 400       | 2.8.1 |
| A088       | A020      | 苍古自由之誓/四风原典   | 武器   | 302       | 2.8.1 |
| A089       | A049      | 宵宫            | 角色1  | 301       | 2.8.2 |
| A090       | A020      | 飞雷之弦振/斫峰之刃    | 武器   | 302       | 2.8.2 |
| A091       |           | 提纳里           | 角色1  | 301       | 3.0.1 |
| A092       | A024      | 钟离            | 角色2  | 400       | 3.0.1 |
| A093       | A020      | 猎人之径/贯虹之槊     | 武器   | 302       | 3.0.1 |
| A094       | A028      | 甘雨            | 角色1  | 301       | 3.0.2 |
| A095       | A053      | 心海            | 角色2  | 400       | 3.0.2 |
| A096       | A020      | 阿莫斯之弓/不灭月华    | 武器   | 302       | 3.0.2 |
| A097       |           | 赛诺            | 角色1  | 301       | 3.1.1 |
| A098       | A019      | 温迪            | 角色2  | 400       | 3.1.1 |
| A099       | A020      | 终未嗟叹之诗/赤沙之杖   | 武器   | 302       | 3.1.1 |
| A100       |           | 妮露            | 角色1  | 301       | 3.1.2 |
| A101       | A027      | 阿贝多           | 角色2  | 400       | 3.1.2 |
| A102       | A020      | 圣显之钥/磐岩结绿     | 武器   | 302       | 3.1.2 |
| A103       |           | 纳西妲           | 角色1  | 301       | 3.2.1 |
| A104       | A049      | 宵宫            | 角色2  | 400       | 3.2.1 |
| A105       | A020      | 千夜浮梦/飞雷之弦振    | 武器   | 302       | 3.2.1 |
| A106       | A071      | 八重神子          | 角色1  | 301       | 3.2.2 |
| A107       | A023      | 达达利亚          | 角色2  | 400       | 3.2.2 |
| A108       | A020      | 神乐之真意/冬极白星    | 武器   | 302       | 3.2.2 |
| A109       |           | 流浪者           | 角色1  | 301       | 3.3.1 |
| A110       | A061      | 荒泷一斗          | 角色2  | 400       | 3.3.1 |
| A111       | A020      | 图莱杜拉的回忆/赤角石溃杵 | 武器   | 302       | 3.3.1 |
| A112       | A052      | 雷电将军          | 角色1  | 301       | 3.3.2 |
| A113       | A076      | 神里绫人          | 角色2  | 400       | 3.3.2 |
| A114       | A020      | 波乱月白经津/薙草之稻光  | 武器   | 302       | 3.3.2 |
| A115       |           | 艾尔海森          | 角色1  | 301       | 3.4.1 |
| A116       | A031      | 魈             | 角色2  | 400       | 3.4.1 |
| A117       | A020      | 裁叶萃光/和璞鸢      | 武器   | 302       | 3.4.1 |
| A118       | A033      | 胡桃            | 角色1  | 301       | 3.4.2 |
| A119       | A082      | 夜兰            | 角色2  | 400       | 3.4.2 |
| A120       | A020      | 若水/护摩之杖       | 武器   | 302       | 3.4.2 |
| A121       |           | 迪希雅           | 角色1  | 301       | 3.5.1 |
| A122       | A097      | 赛诺            | 角色2  | 400       | 3.5.1 |
| A123       | A020      | 苇海信标/赤沙之杖     | 武器   | 302       | 3.5.1 |
| A124       | A065      | 申鹤            | 角色1  | 301       | 3.5.2 |
| A125       | A048      | 神里绫华          | 角色2  | 400       | 3.5.2 |
| A126       | A020      | 雾切之回光/息灾      | 武器   | 302       | 3.5.2 |
| A127       | A0103     | 纳西妲       | 角色1   | 301       | 3.6.1 |
| A128       | A0100     | 妮露      | 角色2   | 400       | 3.6.1 |
| A129       | A020      | 千夜浮梦/圣显之钥      | 武器   | 302       | 3.6.1 |
| A130       |           | 白术      | 角色1   | 301       | 3.6.2 |
| A131       | A028      | 甘雨      | 角色2   | 400       | 3.6.2 |
| A132       | A020      | 碧落之珑/阿莫斯之弓      | 武器   | 302       | 3.6.2 |
| A133       | A049      | 宵宫          | 角色1   | 301       | 3.7.1 |
| A134       | A071      | 八重神子      | 角色2   | 400       | 3.7.1 |
| A135       | A020      | 飞雷之弦振/神乐之真意      | 武器   | 302       | 3.7.1 |
| A136       | A0115     | 艾尔海森      | 角色1   | 301       | 3.7.2 |
| A137       | A045      | 枫原万叶      | 角色2   | 400       | 3.7.2 |
| A138       | A020      | 苍古自由之誓/裁叶萃光      | 武器   | 302       | 3.7.2 |
| A139       | A041      | 优菈      | 角色1   | 301       | 3.8.1 |
| A140       | A018      | 可莉      | 角色2   | 400       | 3.8.1 |
| A141       | A020      | 松籁响起之时/四风原典      | 武器   | 302       | 3.8.1 |
| A142       | A053      | 珊瑚宫心海      | 角色1   | 301       | 3.8.2 |
| A143       | A0109     | 流浪者      | 角色2   | 400       | 3.8.2 |
| A144       | A020      | 不灭月华/图莱杜拉的回忆      | 武器   | 302       | 3.8.2 |
| A145       |           | 林尼      | 角色1   | 301       | 4.0.1 |
| A146       | A081      | 夜兰      | 角色2   | 400       | 4.0.1 |
| A147       | A020      | 最初的大魔术/若水      | 武器   | 302       |4.0.1|
| A148       | A024      | 钟离      | 角色1   | 301       | 4.0.2 |
| A149       | A023      | 公子     | 角色2   | 400       |4.0.2 |
| A150       | A020      | 贯虹之槊/冬极白星      | 武器   | 302       | 4.0.2 |
| A151       |           | 那维莱特      | 角色1   | 301       | 4.1.1 |
| A152       | A033      | 胡桃     | 角色2   | 400       |4.1.1 |
| A153       | A020      | 万世流涌大典/护摩之杖      | 武器   | 302       | 4.1.1 |
| A154       |           | 莱欧斯利      | 角色1   | 301       | 4.1.2 |
| A155       | A019      | 温迪     | 角色2   | 400       |4.1.2 |
| A156       | A020      | 金流监督/终未嗟叹之诗      | 武器   | 302       | 4.1.2 |
| A157       |           | 芙宁娜      | 角色1   | 301       | 4.2.1 |
| A158       | A0130     | 白术     | 角色2   | 400       |4.2.1 |
| A159       | A020      | 静水流涌之辉/碧落之珑      | 武器   | 302       | 4.2.1 |
| A160       | A097      | 赛诺      | 角色1   | 301       | 4.2.2 |
| A161       | A076      | 神里绫人     | 角色2   | 400       |4.2.2 |
| A162       | A020      | 波乱月白经津/赤沙之杖      | 武器   | 302       | 4.2.2 |
| A163       |           | 娜维娅      | 角色1   | 301       | 4.3.1 |
| A164       | A048      | 神里绫华    | 角色2   | 400       |4.3.1 |
| A165       | A020      | 裁断/雾切之回光      | 武器   | 302       | 4.3.1 |
| A166       | A052      | 雷电将军      | 角色1   | 301       | 4.3.2 |
| A167       | A049      | 宵宫     | 角色2   | 400       |4.3.2 |
| A168       | A020      | 薙草之稻光/飞雷之弦振      | 武器   | 302       | 4.3.2 |

>以下为预测内容

| prefabPath | titlePath | 五星up        | 卡池类型 | gachaType | 版本号   |
|------------|-----------|---------------|------|-----------|-------|
| A169       |           | 闲云      | 角色1   | 301       | 4.4.1 |
| A170       | A0103     | 纳西妲     | 角色2   | 400       |4.4.1 |
| A171       | A020      | 鹤鸣余音/千夜浮梦      | 武器   | 302       | 4.4.1 |
| A172       | A031      | 魈      | 角色1   | 301       | 4.4.2 |
| A173       | A071      | 八重神子     | 角色2   | 400       |4.4.2 |
| A174       | A020      | 和璞鸢/神乐之真意      | 武器   | 302       | 4.4.2 |

附每个角色第一次up的代号
```shell
Venti:019
Klee:018
Tartaglia:023
Zhongli:024
Albedo:027
Ganyu:028
Xiao:031
Keqing:032
Hu Tao:033
Eula:041
Kaedehara Kazuha:045
Kamizato Ayaka:048
Yoimiya:049
Raiden Shogun:052
Sangonomiya Kokomi:053
Arataki Itto:061
Shenhe:065
Yae Miko:071
Kamisato Ayato:076
Yelan:081
Tighnari:091
Cyno:097
Nilou:100
Nahida:103
Wanderer:109
Alhaitham:115
Dehya:121
Baizhu:130
Lyney:145
Neuvllette:151
Wriothesley:154
Furina:157
Navia:163
Xianyun:169
```

## 关于测试服卡池：
最近测试CBT2的时候就在想正式服的卡池是从A016开始编号的，那之前的编号是不是就是测试服的？
果不其然，我在CBT2中发现了一些影子。
以下是在CBT2（0.7.1版本）中测试好的卡池。

其中有一些`扭蛋预览Prefab路径`是可以直接填角色的英文名的，比如`UI_Tab_GachaShowPanel_Xiao`和`UI_Tab_GachaShowPanel_A003`都能正常显示魈的卡池预览

| 扭蛋Prefab路径 | 扭蛋预览Prefab路径 | 五星up          | 四星up | 备注 |
|------------|-----------|---------------|------|-----|
|GachaShowPanel_A008|	UI_Tab_GachaShowPanel_Diluc | | | 奔行世间（常驻）|
|GachaShowPanel_A007|	UI_Tab_GachaShowPanel_Noel |  | 诺艾尔 | 新手祈愿 |
|GachaShowPanel_A006| | | | 卡池和预览都是空的 |
|GachaShowPanel_A005|	UI_Tab_GachaShowPanel_A005 | | | 迪卢克头像但是没卡池|
|GachaShowPanel_A004|	UI_Tab_GachaShowPanel_A004 | 钟离 | 凝光 | 斗转星移 |
|GachaShowPanel_A003|	UI_Tab_GachaShowPanel_Xiao | 魈 | 北斗 | 靖妖降魔 |
|GachaShowPanel_A002|	UI_Tab_GachaShowPanel_Venti | 温迪 | 雷泽 | 北风的诗篇 |
|GachaShowPanel_A001|	UI_Tab_GachaShowPanel_A001 | 琴/迪卢克 | | 新的旅程 普通祈愿（内测） |

