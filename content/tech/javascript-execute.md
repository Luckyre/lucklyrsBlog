---
title: javascript小记
tags: 
- JavaScript
date: 2019-03-18 22:12:18
permalink:
categories: 
- Javascript
description:
image:
---
<p class="description"></p>

<img src="https://i.loli.net/2019/03/18/5c8fa8c0ee200.jpg" alt="" style="width:100%" />

<!-- more -->

#### javascript执行:(Promise里的代码为什么比setTimeout先执行)

    我们把宿主发起的任务称为宏观任务, 把javascript引擎发起的任务称为微观任务👀 
   
   ```javascript
       var r = new Promise(function(resolve, reject){
           console.log("a");
           resolve()
       });
       setTimeout(()=>console.log("d"), 0)
       r.then(() => console.log("c"));
       console.log("b")
```
   以上执行结果可自行尝试运行（abcd😝），d 必定发生在 c 之后，因为 Promise 产生的是javascript引擎内部的微任务，而setTimeout是浏览器的API,它产生宏任务
 ,微任务始终先于宏任务 （微观任务不执行完成不会进行宏观任务）
 
 ```javascript
    setTimeout(()=>console.log("d"), 0)
    var r1 = new Promise(function(resolve, reject){
        resolve()
    });
    r.then(() => { 
        var begin = Date.now();
        while(Date.now() - begin < 1000);
        console.log("c1") 
        new Promise(function(resolve, reject){
            resolve()
        }).then(() => console.log("c2"))
    });
```

                 
## javascript的闭包和执行上下文
<img src="https://i.loli.net/2019/03/20/5c917cf3be0a7.png"   alt=""  />

## javascript

<hr />