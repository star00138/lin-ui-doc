---
title: 底部标签栏 TabBar
---

# <H2Icon /> 底部标签栏 TabBar

> 底部标签栏适用场景：需要动态控制标签种类、数量，以及对样式自定义程度高的场景

## 介绍

底部标签栏使用微信小程序的[ 自定义 TabBar ](https://developers.weixin.qq.com/miniprogram/dev/framework/ability/custom-tabbar.html)实现。在初次切换页面时，会发生闪烁，该问题是微信小程序自定义 TabBar 底层实现方式导致，不属于 Lin UI 的问题。

## 基础使用
<p align="center">
  <img style="height:300px" src="/screenshots/tab-bar/tab-bar-1.png">
</p>

根据[微信小程序官方要求](https://developers.weixin.qq.com/miniprogram/dev/framework/ability/custom-tabbar.html)，要使用自定义 TabBar ，需进行如下配置：

- 在`app.json`中将`tabBar`的`custom`字段指定为`true`

- `tabBar`的其他字段需完整填写（**这里`list`等配置的作用仅是为了兼容，实际不生效**）

  代码示例：

    ```json
    {
      "tabBar": {
        "custom": true,
        "color": "#000000",
        "selectedColor": "#000000",
        "backgroundColor": "#000000",
        "list": [{
          "pagePath": "page/component/index",
          "text": "组件"
        }, {
          "pagePath": "page/API/index",
          "text": "接口"
        }]
      }
    }
    ```

- 在对应的**每个**`tab`页面中引入`TabBar`组件并在页面中使用，同时指定`list`属性（**该`list`会生效**）

  ```json
  {
      "usingComponents":{
          "l-tab-bar":"/miniprogram_npm/tab-bar/index"
      }
  }
  ```

  ```wxml
  <l-tab-bar list="{{list}}" />
  ```

  ```js
  Page({
      data:{
          list:[
              {
                  pagePath:"/pages/index/index",
                  text:"首页",
                  unselectedIconPath:"/icons/tab-bar/index.png",
                  selectedIconPath:"/icons/tab-bar/index-selected.png"
              },{
                  pagePath:"/pages/feed/index",
                  text:"动态",
                  unselectedIconPath:"/icons/tab-bar/feed.png",
                  selectedIconPath:"/icons/tab-bar/feed-selected.png"
              },{
                  pagePath:"/pages/my/index",
                  text:"我的",
                  unselectedIconPath:"/icons/tab-bar/my.png",
                  selectedIconPath:"/icons/tab-bar/my-selected.png"
              }
          ]
      }
  })
  ```

## 圆形标签
<p align="center">
  <img style="height:300px" src="/screenshots/tab-bar/tab-bar-2.png">
</p>
如果你想实现半圆标签，只需在`list`的对象中指定`style`为`circle`即可：

  ```js
  list:[{
      pagePath:"/pages/index/index",
      text:"首页",
      unselectedIconPath:"/icons/tab-bar/index.png",
      selectedIconPath:"/icons/tab-bar/index-selected.png",
      style:"circle"
  }]
  ```

##   底部标签栏属性（TabBar Attributes）

| 属性                  | 说明                      | 类型            | 可选值         | 必填 | 默认值  | 版本号 |
| --------------------- | ------------------------- | --------------- | -------------- | ---- | ------- | ------ |
| list                  | TabBar 绑定的页面路径     | Array\<Object\> | -              | 是   | -       | -      |
| bg-color              | TabBar 背景色             | String          | CSS 支持的颜色 | 否   | white   | -      |
| text-selected-color   | TabBar 文字选中时的颜色   | String          | CSS 支持的颜色 | 否   | 主题色  | -      |
| text-unselected-color | TabBar 文字未选中时的颜色 | String          | CSS 支持的颜色 | 否   | #666666 | -      |

## 页面列表属性（List Attributes）

`list`接收一个数组，数组中的每项都是一个对象，对象可配置属性如下表

| 属性               | 说明               | 类型    | 可选值             | 必填 | 默认值    | 版本号 |
| ------------------ | ------------------ | ------- | ------------------ | ---- | --------- | ------ |
| pagePath           | 标签对应页面路径   | String  | -                  | 是   | -         | -      |
| text               | 标签文字           | String  | -                  | 是   | -         | -      |
| unselectedIconPath | 未选中状态图标路径 | String  | -                  | 是   | -         | -      |
| selectedIconPath   | 选中状态图标路径   | String  | -                  | 是   | -         | -      |
| style              | 标签风格           | String  | `default`/`circle` | 否   | `default` | -      |
| redDot             | 是否显示红点       | Boolean | `true`/`false`     | 否   | `false`   | -      |

## 底部标签栏外部样式类（TabBar External Classes）

| 外部样式类              | 说明                       |
| ----------------------- | -------------------------- |
| l-class                 | 覆盖整体的样式             |
| l-item-class            | 覆盖标签整体的样式         |
| l-item-selected-class   | 覆盖标签整体选中时的样式   |
| l-item-unselected-class | 覆盖标签整体未选中时的样式 |
| l-icon-class            | 覆盖图标的样式             |
| l-icon-selected-class   | 覆盖图标选中时的样式       |
| l-icon-unselected-class | 覆盖图标未选中时的样式     |
| l-text-class            | 覆盖文字的样式             |
| l-text-selected-class   | 覆盖文字选中时的样式       |
| l-text-unselected-class | 覆盖文字未选中时的样式     |


## 底部标签栏事件（TabBar Events）

| 事件名称       | 说明           | 返回值       | 备注 |
| -------------- | -------------- | ------------ | ---- |
| bind:linchange | 标签切换时触发 | 当前标签信息 |      |

<RightMenu />