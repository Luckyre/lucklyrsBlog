---
title: promise
tags: 
- ES6
- Promise

date: 2019-10-19 15:36:12
permalink:
categories:
description:
image:
---
<p class="description"></p>
<!-- more -->

###  Promise结构
  ```javascript
   new Promise((resolve, reject)=>{
     $.ajax({
          url: 'http://www.kaoyaya.com/api/v1/login/isLogin',
          type: 'post',
         success(res){
            resolve(res);
         },
         error(res){
            reject(res)
         }
     })
   }).then(()=>{
      console.log('success', res)
   },(err)=>{
      console.log('error',res)
   })
```
###  链式Promise

  ```javascript
  var PromiseOne =  new Promise((resolve, reject)=>{
     $.ajax({
          url: 'http://www.kaoyaya.com/api/v1/login/isLogin',
          type: 'post',
         success(res){
            resolve(res);
         },
         error(res){
            reject(res)
         }
     })
   }).then(()=>{
      console.log('success')
   },(err)=>{
      console.log('error')
   })
   
     var PromiseTwo =  new Promise((resolve, reject)=>{
        $.ajax({
             url: 'http://www.kaoyaya.com/api/v1/login/isLogin',
             type: 'post',
            success(res){
               resolve(res);
            },
            error(res){
               reject(res)
            }
        })
      }).then(()=>{
         console.log('success')
      },(err)=>{
         console.log('error')
      })
      
      PromiseOne.then(()=>{
        console.log('PromiseOne success ')
        return PromiseTwo
      }).then(()=>{
           console.log('PromiseTwo success ')
      })
```
<hr />