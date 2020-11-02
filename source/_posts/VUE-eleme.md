---
title: VUe的动态菜单
date: 2020-05-13 09:38:11
categories: 
tags: 
    - VUE
mp3:
cover: https://pic1.zhimg.com/v2-2ad93fccf9862fe5dff82f5c7eabf82e_r.jpg
---

## 情景

vue-eleme-admin 的后台管理系统的后台返回的动态菜单


## 解决办法

网上地址做法：https://segmentfault.com/a/1190000021900731

代码地址：https://gitee.com/jason0319/go-admin

修改的文件

## router.js

## permission.js

## store -> model -> permission


## cant’t not find xxxx.vue 原因：webpack 版本问题，webpack4中动态import不支持变量方式
``` javascript 
/**
 * 路由懒加载S
 * 原因：webpack 版本问题，webpack4中动态import不支持变量方式
 * @param {路由地址}} view 
 */
export const loadView = (view) => {
  return (resolve) => require([`@/views${view}`], resolve)
}
```

``` javascript 
/**
 * 后台查询的菜单数据拼装成路由格式的数据
 * @param routes
 */
export function generaMenu(routes, data) {
  data.forEach(item => {
    // alert(JSON.stringify(item))
    const menu = {
      path: item.path,
      component: item.component === '#' ? Layout : loadView(item.component),
      // component: item.component === '#' ? Layout : () => import(`@/views/VipManage/index`),
      hidden: item.hidden,
      redirect: item.redirect,
      children: [],
      name: 'menu_' + item.id,
      meta: item.meta
      // meta: { title: item.name, id: item.id, roles: ['admin'] }
    }
    if (item.children) {
      generaMenu(menu.children, item.children)
    }
    routes.push(menu)
  })
  router.options.routes = routes   //这一段最为重要
  console.log(routes)
}
```

## 后台返回的数据格式

``` json
[{
            "children": [{
                "children": [],
                "component": "/VipManage/index",
                "hidden": false,
                "id": 2,
                "meta": {
                  "icon": "#",
                  "status": true,
                  "title": "会员列表"
                },
                "name": "会员列表",
                "path": "/VipManage",
                "pid": 1,
                "url": "VipManage"
              },
              {
                "children": [],
                "component": "/VuserManagement/index",
                "hidden": false,
                "id": 2,
                "meta": {
                  "icon": "#",
                  "status": true,
                  "title": "V等级列表"
                },
                "name": "V等级列表",
                "path": "/VuserManagement",
                "pid": 1,
                "url": "VuserManagement"
              },
              {
                "children": [],
                "component": "/partner/index",
                "hidden": false,
                "id": 2,
                "meta": {
                  "icon": "#",
                  "status": true,
                  "title": "合伙人等级列表"
                },
                "name": "合伙人等级列表",
                "path": "/partner",
                "pid": 1,
                "url": "partner"
              },
              {
                "children": [],
                "component": "/partnerUpdate/index",
                "hidden": false,
                "id": 2,
                "meta": {
                  "icon": "#",
                  "status": true,
                  "title": "合伙人升级列表"
                },
                "name": "合伙人升级列表",
                "path": "/partnerUpdate",
                "pid": 1,
                "url": "partnerUpdate"
              },
              {
                "children": [],
                "component": "/statistics/index",
                "hidden": false,
                "id": 2,
                "meta": {
                  "icon": "#",
                  "status": true,
                  "title": "拼团统计"
                },
                "name": "拼团统计",
                "path": "/statistics",
                "pid": 1,
                "url": "statistics"
              }
            ],
            "component": "#",
            "hidden": false,
            "id": 1,
            "meta": {
              "icon": "fafa-adjust",
              "status": true,
              "title": "会员管理"
            },
            "name": "会员管理",
            "path": "/",
            "pid": 0,
            "url": "/"
          },
          {
            "children": [
              {
                "children": [],
                "component": "/wallet/index",
                "hidden": false,
                "id": 2,
                "meta": {
                  "icon": "#",
                  "status": true,
                  "title": "会员资产列表"
                },
                "name": "会员列表",
                "path": "/VipMenuList",
                "pid": 1,
                "url": "VipMenuList"
              },
              {
                "children": [],
                "component": "/VipManage/records/Diamond",
                "hidden": false,
                "id": 2,
                "meta": {
                  "icon": "#",
                  "status": true,
                  "title": "钻石明细"
                },
                "name": "钻石明细",
                "path": "/Diamond",
                "pid": 1,
                "url": "Diamond"
              },
              {
                "children": [],
                "component": "/VipManage/records/YuanDiamond",
                "hidden": false,
                "id": 2,
                "meta": {
                  "icon": "#",
                  "status": true,
                  "title": "原钻明细"
                },
                "name": "原钻明细",
                "path": "/YuanDiamond",
                "pid": 1,
                "url": "YuanDiamond"
              }
            ],
            "component": "#",
            "hidden": false,
            "id": 11,
            "meta": {
              "icon": "fafa-adjust",
              "status": false,
              "title": "会员资产管理"
            },
            "name": "会员资产管理",
            "path": "/VipMenu",
            "pid": 0,
            "url": "/VipMenu"
          },
          {
            "children": [
              {
                "children": [],
                "component": "/midAccount/list",
                "hidden": false,
                "id": 2,
                "meta": {
                  "icon": "#",
                  "status": true,
                  "title": "子账号列表"
                },
                "name": "子账号列表",
                "path": "/midAccountList",
                "pid": 1,
                "url": "midAccountList"
              },
              {
                "children": [],
                "component": "/midAccount/index",
                "hidden": false,
                "id": 2,
                "meta": {
                  "icon": "#",
                  "status": true,
                  "title": "子账号抽奖配置列表"
                },
                "name": "子账号抽奖配置列表",
                "path": "/midAccountAward",
                "pid": 1,
                "url": "midAccountAward"
              },
              {
                "children": [],
                "component": "/midAccount/record",
                "hidden": false,
                "id": 2,
                "meta": {
                  "icon": "#",
                  "status": true,
                  "title": "子账户抽奖明细"
                },
                "name": "子账户抽奖明细",
                "path": "/midAccountDetail",
                "pid": 1,
                "url": "midAccountDetail"
              }
            ],
            "component": "#",
            "hidden": false,
            "id": 12,
            "meta": {
              "icon": "fafa-adjust",
              "status": true,
              "title": "子账号管理"
            },
            "name": "子账号管理",
            "path": "/midAccount",
            "pid": 0,
            "url": "/midAccount"
          },
          {
            "children": [
              {
                "children": [],
                "component": "/group/index",
                "hidden": false,
                "id": 2,
                "meta": {
                  "icon": "#",
                  "status": true,
                  "title": "拼团类型列表"
                },
                "name": "拼团类型列表",
                "path": "/groupList",
                "pid": 1,
                "url": "groupList"
              },
              {
                "children": [],
                "component": "/group/ConfigIndex",
                "hidden": false,
                "id": 2,
                "meta": {
                  "icon": "#",
                  "status": true,
                  "title": "拼团基本配置列表"
                },
                "name": "拼团基本配置列表",
                "path": "/groupConfigList",
                "pid": 1,
                "url": "groupConfigList"
              },
              {
                "children": [],
                "component": "/GroupRecords/open",
                "hidden": false,
                "id": 2,
                "meta": {
                  "icon": "#",
                  "status": true,
                  "title": "开团记录"
                },
                "name": "开团记录",
                "path": "/OpenGroupRecord",
                "pid": 1,
                "url": "OpenGroupRecord"
              },
              {
                "children": [],
                "component": "/GroupRecords/join",
                "hidden": false,
                "id": 2,
                "meta": {
                  "icon": "#",
                  "status": true,
                  "title": "参团记录"
                },
                "name": "参团记录",
                "path": "/OpenGroupRecordjoin",
                "pid": 1,
                "url": "OpenGroupRecordjoin"
              },
              {
                "children": [],
                "component": "/GroupDetail/index",
                "hidden": false,
                "id": 2,
                "meta": {
                  "icon": "#",
                  "status": true,
                  "title": "当前团明细"
                },
                "name": "当前团明细",
                "path": "/GroupDetail",
                "pid": 1,
                "url": "GroupDetail"
              }
            ],
            "component": "#",
            "hidden": false,
            "id": 13,
            "meta": {
              "icon": "fafa-adjust",
              "status": true,
              "title": "拼团管理"
            },
            "name": "拼团管理",
            "path": "/group",
            "pid": 0,
            "url": "/group"
          },
          {
            "children": [
              {
                "children": [],
                "component": "/record/day",
                "hidden": false,
                "id": 2,
                "meta": {
                  "icon": "#",
                  "status": true,
                  "title": "日结列表"
                },
                "name": "日结列表",
                "path": "/record/day",
                "pid": 1,
                "url": "/record/day"
              },
              {
                "children": [],
                "component": "/record/month",
                "hidden": false,
                "id": 2,
                "meta": {
                  "icon": "#",
                  "status": true,
                  "title": "月结列表"
                },
                "name": "月结列表",
                "path": "/record/month",
                "pid": 1,
                "url": "/record/month"
              }
            ],
            "component": "#",
            "hidden": false,
            "id": 14,
            "meta": {
              "icon": "fafa-adjust",
              "status": true,
              "title": "结算列表"
            },
            "name": "结算列表",
            "path": "/record",
            "pid": 0,
            "url": "/record"
          },
          {
            "children": [],
            "component": "/parameter/index",
            "hidden": false,
            "id": 15,
            "meta": {
              "icon": "fafa-adjust",
              "status": true,
              "title": "参数列表"
            },
            "name": "参数列表",
            "path": "/parameter",
            "pid": 0,
            "url": "/parameter"
          },
          {
            "children": [],
            "component": "/messagePage/index",
            "hidden": false,
            "id": 16,
            "meta": {
              "icon": "fafa-adjust",
              "status": true,
              "title": "说明信息列表"
            },
            "name": "说明信息列表",
            "path": "/messagePage",
            "pid": 0,
            "url": "/messagePage"
          }
        ]
```