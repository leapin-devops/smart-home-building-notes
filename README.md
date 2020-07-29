# smart-home-building-notes
记录一下智能家居改造的过程

* 需求
* 选型
* 方案设计对比
* 方案实施
* 花费
* 下一步
* FAQ

## 需求
* 最好能够支持Homekit
* 照明
* 窗帘
* 影音
* 空调
* 晾衣架
* 其它设备控制

## 选型
目前国内屋内智能家居领域的厂商众多。这里只关注一些产品易用的品牌和厂商。这类产品的好处是易上手，好配置，开箱即用，无需太多复杂的电路改造。

| 品牌 | 智能家居平台 | 语音助手 | 优点 | 缺点 | 备注 |网址|
| --- | --- | --- | --- | --- | --- | --- |
| 小米 |米家App、Homekit|小爱、Siri|价格相对较低，生态好|没有墙壁开关||
| 绿米（aqara）|米家App、Aqara App、Homekit|小爱、Siri|产品设计较好、有实体体验店|价格相对小米偏高|小米孵化企业，后来单飞，大部分产品与小米互相兼容|[官网](https://www.aqara.com/)|
| 小燕 | 小燕App, Homekit | 小爱、Siri、Alexa、Google Assistant、天猫、小度等 | 没有用过，不做评价 | 没有用过，不做评价 ||[官网](https://www.xiaoyan.io/)|
|欧瑞博|自家App|自家设备|没用过，但看官网的感觉是深耕行业多年，功能强大，产品颜值高。墙壁中控很帅|产品生态封闭，颜值很高但是不够百搭。|知名度在装修界很高|[官网](https://www.orvibo.com/)
|Yeelight|Yeelight App, Homekit, 米家App|小爱、Siri、Alexa、Google Assistant等|灯具色温亮度无极调整，显色度比较好||只做智能灯具产品|[官网](https://www.yeelight.com/)|

最后选用了绿米加yeelight的产品。原因：
* 支持米家和Homekit双平台
* 通过小米的小爱音箱(带红外遥控的)或者万能遥控器可以控制传统电器
* 产品设计较好，比较百搭
* 网络上教程资源比较丰富
* 原来装修的灯带和筒射灯不支持调色温和亮度。而且色温只有3000k，偏黄。

## 方案设计对比
### 智能家居总体架构
![总体架构图](https://github.com/kuang1987/smart-home-building-notes/blob/master/images/arch.png)
### 设备分类
#### 按照功能
|分类|设备|功能|
|---|---|---|
|家庭中枢|小爱音箱<br>HomePod<br>Apple TV<br>iPad<br>等等|主要用于远程控制。有些中枢会集成网关功能，比如小爱音箱pro自带了蓝牙Mesh网关和万能红外遥控功能|
|网关|小米多模网关<br>Aqara网关<br>其它品牌网关|主要是通讯协议转换|
|传感器|人体传感器<br>门窗传感器<br>温湿度传感器<br>烟雾传感器<br>等等|主要感知外界信息|
|控制器|智能灯<br>墙壁开关<br>窗帘电机<br>红外遥控器<br>等等||

#### 按照通信协议
|分类|优势|劣势|
|---|---|---|
|WiFi|便于连接，无需网关|信号受距离和房间结构影响较大|
|Zigbee|物联网主流协议，信号好|需要网关|
|蓝牙Mesh|主要用于智能灯具分组|传输距离短|
|红外/射频|控制传统电器|不能感知状态，只能单向控制|

### 灯光控制
|方案|优势|劣势|
|---|---|---|
|替换原开关为智能墙壁开关|无需换灯，价格相对便宜|开关造型可能与原装修不搭，需要替换原开关|
|更换智能灯具|灯具灵活分组，亮度色温可调|成本较高。成品灯具像吊灯、落地灯、吸顶灯造型较少。智能灯泡只有常规螺口。||


### 窗帘控制
|方案|优势|劣势|
|---|---|---|
|智能窗帘电机|安装简单。支持开关到某个位置，支持手动轻拉后自动开关|价格高、多数电机需要预置插座。锂电池版成本高|
|遥控窗帘点击|成本低|需要预留插座、使用红外/射频控制、难以实现开关某个位置|  

\* Tips： 如果想节省成本，在有主帘和纱帘的情况下，可以只安装一条电动轨道，然后用魔术贴连接主帘和纱帘。

### 传统电器控制
主要通过红外遥控和射频遥控进行控制，无法感知被控制设备的状态。  
\* Tips: 小爱同学pro和小米的万能遥控器本身只支持红外遥控，但可以通过加装射频板或者外界射频发射器实现对射频以及其他遥控的支持。  


### 空调控制
对于常规空调，使用红外遥控。
对于重要空调，aqara和其它品牌有专门的VRF智能控制器，可接入智能家居系统，控制全屋内机。但是价格较贵。


## 方案实施
这里按照房内的区域进行说明

### 全屋
|产品|功能|备注|
|---|---|---|
|小爱音箱pro| <ul><li>米家系智能中枢</li><li>语音助手</li><li>红外、射频遥控器</li></ul>|小爱音箱pro需加射频模块|
|Apple TV 4k|<ul><li>Homekit中枢</li></ul>|[ATV4k教程](https://github.com/kuang1987/apple-tv-tutorial) 这个之前已经入了，所以就直接用ATV做Homekit中枢。另外可以用HomePod或者iPad作为中枢。如果不需要HomeKit支持，可略过|
|Aqara网关|Zigbee网关|也可购买小米多模网关，小米和Aqara的Zigbee设备大部分兼容。小米多模网关目前不支持Aqara B1(锂电池版窗帘电机)|

### 客厅
