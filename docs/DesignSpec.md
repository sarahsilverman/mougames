# SDK Specs

## Framework

~~对appids文件进行加密, 加密方法： blowfish~~

文件名：appids.json


```
[
	{"name":"chartboost","id":"","sign":""},
	{"name":"applift","id":"","secret":""},
	{"name":"flurry","id":"","space":""},
	{"name":"vungle","id":""},
	{"name":"playhaven","token":"","secret":"","place":""},
	{"name":"nativex","id":""}
]

```

需要包含的Library：

- chartboost.framework
- applift
- flurry
- adcolony.framework
- vungle.framework
- playhaven (source code)
- nativeX
- appia

将以上库进行解包，重新打包为新的framework

目标：

- product : mousdk.framework
- universal library : arm7, arm7s, arm64
- includes original bundle

## 服务器端请求更新

每天从服务器端请求一次更新 appids.json，并存在本地。

工作顺序，先启动各个渠道的initilize方法，再更新appids.json。

## 统计

#### 广告统计

统计类型：

- request ，调用显示广告方法，发出广告展示请求
- impression ，广告成功展示
- click ，广告被用户点击

上述行为发生后，需要调用track方法向统计服务器发送报告数据。

服务器地址： `api.mougames.com/api/track`

发送统计内容

```
Type: x-www-form-urlencoded

tdata = {content}

// optional , to show debug info in response
debug = 1 

```

content 为JSON格式的string

```
{
	owner_id	: {owner id}
	platform	: { "ios" | "android" | "windows" }
	app_id 		: {app id}
	adn 		: {ads network name}
	action 		: { "request" | "impression" | "click" }
}

```


#### 基本统计

类型

- install，初次启动
- bootup，启动

content 为JSON格式的string

```
{
	owner_id	: {owner id}
	platform	: { "ios" | "android" | "windows" }
	app_id 		: {app id}
	action 		: { "install" | "bootup" }
	idfa		: {iOS IDFA}
}

```
