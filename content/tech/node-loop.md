---
title: node-loop
tags: 
- JavaScript
date: 2019-04-11 21:58:03
permalink:
categories: 
- Javascript
description:
image:
---
<p class="description">处理章节等同级数据节点</p>

<!-- more -->

#### 当章节课时这种本属于三层类型数据传入一维数组数据处理时👀  
    下列为三层同级的一维数组数据
```javascript
  const lessonsList = [
    {id: '15941', type: 'chapter', title: '第一章 总论'},
    {id: '22183', type: 'unit', title: '法律基础'},
    {id: '15949', type: 'lesson', title: '第1讲-法的入门'},
    {id: '15950', type: 'lesson', title: '第2讲-法律关系'},
    {id: '15951', type: 'lesson', title: '第3讲-法律事实'},
    {id: '15952', type: 'lesson', title: '第4讲-法的形式与分类'},
    {id: '15953', type: 'lesson', title: '第5讲-法律部门与法律体系'},
    {id: '22184', type: 'unit', title: '经济纠纷解决途径'},
    {id: '15954', type: 'lesson', title: '第1讲-经济纠纷解决途径入门'},
    {id: '22218', type: 'lesson', title: '第2讲-仲裁'},
    {id: '25602', type: 'lesson', title: '第3讲 民事诉讼'},
    {id: '22220', type: 'lesson', title: '第4讲-行政复议'},
    {id: '22221', type: 'lesson', title: '第5讲-行政诉讼'},
    {id: '22186', type: 'unit', title: '法律责任'},
    {id: '22222', type: 'lesson', title: '第1讲-法律责任'},
    {id: '15942', type: 'chapter', title: '第二章 会计法律制度'},
    {id: '22222', type: 'lesson', title: '第1讲-法律责任'},
  ];
```
   
####    当前台展示需要从一维数组转换为三维数组（章节课时等三层级父子级别关系型数据）(ˇˍˇ) 想～
   封装以下函数进行数据处理
```javascript
/**
 * 将章节课时同级，改为章->节、课时
 * @param courseLessonLists
 * @returns {Array}
 */
function filterLessonLists(courseLessonLists) {
  const chapterList = lessonListFlatToArry(courseLessonLists, 'chapter');
  chapterList.map((val,item) =>{
    val.children = lessonListFlatToArry(val,children, 'unit'); // 分离节和课时
  })
}

function lessonListFlatToArry(list,nodeType){
  let indexArray = []; //章或节的索引
  let filterTemplateLessonLists = [];
  list.forEach((valItem,index)=> {
    if(valItem.type === nodeType) indexArray.push(index);
  });
  indexArray.map((chapterIndex, index, arry)=>{
    let obj ={};
    if(arry[index +1]) {
      //章后一个index存在、截取后一个章/节之间 index 
      obj = list[chapterIndex];
      obj.isShow = 0;  //为了后续控制层级收缩拉升状态
      obj.children = list.slice(chapterIndex + 1, arry[index + 1]);
    }else {
      // 章后一个index不存在， 截取到最后
      obj = list[chapterIndex];
      obj.isShow = 0;
      obj.children = list.slice(0, indexArray[0]); //indexArray[0]为undefined，slice也会截取到末尾
      filterTemplateLessonLists[index] = obj;
    }
    return filterTemplateLessonLists;
  })
}
```


------------------------------------------   我是分割线------------------------------------------ 
```javascript
数据结构由此 [{}]  ===> 
                       [{ 
                         title:'chapter',
                         children:[{
                           title:'unit',
                           children: [{
                            title: 'lesson',
                            children:[]}]}
                         ]}]
```

   
<hr />