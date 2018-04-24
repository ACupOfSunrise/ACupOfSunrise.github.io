---
layout:     post
title:      FreeMarker
subtitle:   FreeMarker简介
date:       2018-04-24
author:     Lou xiansen
header-img: img/post-bg-coffee.jpeg
catalog: true
tags:
    - FreeMarker
---

# 正文

## 1. XXXList表示查询一个没有分页的list
```javascript
    //attr属性名称 ,limit表示显示条数，isIncludeChildren是否包含子集
    //node节点名称属性（菜单名称）,nodeId节点代码（菜单Id）,parent父节点属性,parentId父节点ID
    [@InfoList attr='focus' limit='4';list]

      [#list list as info]
      循环的内容  exp: ${info.url} //文章路径
      //url表示路径,attrImageUrl表示属性图片路径，title表示标题
      //${substring(info.title,10,'...')}free marker自定义的substring
      [/#list]

    [/@InfoList]
```

## 2. XXXPage表示查询一个分页的list
```js
    //attr属性名称 ,limit表示显示条数，isIncludeChildren是否包含子集
    //node节点名称属性（菜单名称）,nodeId节点代码（菜单Id）,parent父节点属性,parentId父节点ID
    [@InfoPage attr='focus' limit='4';list]

      [#list list as info]
      循环的内容  exp: ${info.url} //文章路径
      //url表示路径,attrImageUrl表示属性图片路径，title表示标题
      //${substring(info.title,10,'...')}free marker自定义的substring
      //${info.customs['price']}后台自定义字段 'price'
      [/#list]

    [/@InfoPage]
```
## 3. 带导航的信息列表

```js

    [@InfoPage nodeId=node.id sort=sort pageSize='10';pagedList]

      //循环导航二级菜单
      [@NodeList parentId=node.parent.id;list]
        [#list list as n]
          <a href="${n.url}"class="[#if node.id==n.id]ap-curr[#else]ap[/#if]">${n.name}</a>
        [/#list]
      [/@NodeList]

      //循环列表
      [#list pagedList.content as info]
        context...
      [/#list]

      //分页组件
      [#include 'page.html'/]
    [/@InfoPage]
  ```
