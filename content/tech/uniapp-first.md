+++
title = "uniapp 初识"
date = "2022-08-30 10:17:25"
tags = ["uniapp"]
categories = ["uniapp"]
gitinfo = true
dropCap = false
toc = true
+++


### uniapp

> uni-app是一个Vue.js开发所有前端应用的框架，开发者通过开发一套代码，然后打包适配、发布到IOS、Android、Web(响应式)、以及现在各大平台的小程序、快应用等多个平台。

 时间线拉到19年，我记得当时去上海的交大徐汇校区参加了VUECONF，参加技术分享大会看到了Winter、蒋豪群、尤雨溪等大佬的分享。  
 当时也第一次听到了DCloud前端架构师以“vue开发小程序之性能优化”的主题来介绍了uni-app、当时基于微信平台，很多公司也有基于微信开源特有的框架、如wepy、mpvue、Megalo、mpx等。所以眼球上没有很大去注意。当时都放在了尤大大身上、去追签名照😄

---
![2019.jpg](/images/2019.jpg "参会")

![v.jpg](/images/v.jpg "尤大大签名照")

---

### uniapp 使用体验

- uniapp的开发工具也是官方推荐的HBuilder、工具内部也继承了相关基本构建、打包多平台机制，其他需要特殊配置的[插件](https://ext.dcloud.net.cn/search?q=icons&plguin%3Fid=28)也有点相似与VSCode一样，安装相应插件包

- 语法层面很多都是vue的语法，但是生命周期与微信开发的生命周期类似

- uniapp 可以通过 uniCloud整合后台业务

`uniClound` 目前是可以在阿里云与腾讯云为开发者基于serverless模式和JS编程的云开发平台，简单来说就是前端可以使用JS开发后端的业务，而不用去学习后台一些语言  


#### uniClound

1、通过注册账号，选择相应的服务商、连接对应的[uniClound 数据库](https://unicloud.dcloud.net.cn/cloud-database?provider=aliyun)

2、通过创建服务空间，关联相应的项目。然后就可以通过在uniClound云数据库中建立数据表、通过建立本地建立云函数api去获取云数据表,如下的
```js
// 获取数据库的引用
'use strict';
const db = uniCloud.database()
const $ = db.command.aggregate
exports.main = async (event, context) => {
	const {
		user_id
	} = event
	// author_likes_ids
	let userinfo = await db.collection('user').doc(user_id).get() //获取user表数据
	userinfo = userinfo.data[0]

	let lists = await db.collection('user')
		.aggregate()
		.addFields({
			is_like: $.in(['$id', userinfo.author_likes_ids])
		})
		.match({
			is_like: true
		})
		.end()

	//返回数据给客户端
	return {
		code: 200,
		msg: '数据获取成功',
		data: lists.data
	}
};

// 前台通过调用相应的云函数名关联
	uniCloud.callFunction({
			name: url, //封装的云函数名
			data //请求参数
		})
```

####  uni组件

> uni组件存在基础组件与自定义扩展封装组件

- 1、基础组件内部有一些官方定义的view、scroll-view、progress、navigator等原生组件、直接使用

```html
<scroll-view class="list-scroll" scroll-y @scrolltolower="loadmore">
			<view>
				<slot></slot>
			</view>
		</scroll-view>
```
- 2、外部组件通过[插件市场](https://ext.dcloud.net.cn/) 下载安装，即会在uni_modules目录显示，可直接在相关业务场景使用,无需import环节，开箱即用的感觉。对比与传统的安装、引用、注册，三个步骤后才能使用组件流程确实精简。

- 3、组件的通用性，难免存在二次封装，在uni中可直接在components目录下创建或者全局创建、挂载在Vue.component上

``` js
│─components            	符合vue组件规范的uni-app组件目录
│  └─componentA         	符合‘components/组件名称/组件名称.vue’目录结构，easycom方式可直接使用组件
│  		└─componentA.vue    可复用的componentA组件
│  └─component-a.vue      可复用的component-a组件
```

