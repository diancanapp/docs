# diancan api

- **API**
  - [ ] [Save user info](#save-user-info)
  - [ ] [Current user](#current-user)
  - [ ] [My bonus](#my-bonus)
  - [ ] [Make order](#make-order)
  - [ ] [Pay order](#pay-order)
  - [ ] [My orders](#my-orders)
  - [ ] [Order detail](#order-detail)
  - [ ] [Submit feedback](#submit-feedback)
  - [X] [Weapp upload to qiniu](#weapp-upload-to-qiniu)
  - [ ] [Wechat login](#wechat-login)
  - [ ] [Login](#login)
  - [ ] [Goods list](#goods-list)
  - [ ] [Goods detail](#goods-detail)
  - [ ] [Banner list](#banner-list)
  - [ ] [Banner detail](#banner-detail)
  - [ ] [Categories list](#categories-list)
  - [ ] [Category detail](#category-detail)
  - [ ] [Configs list](#configs-list)
  - [ ] [Config detail](#config-detail)
  - [ ] [Upload to qiniu](#upload-to-qiniu)
  - [ ] [Add banner](#add-banner)
  - [ ] [Delete banner](#delete-banner)
  - [ ] [Modify banner](#modify-banner)
  - [ ] [Bonuses list](#bonuses-list)
  - [ ] [Bonus detail](#bonus-detail)
  - [ ] [Add bonus](#add-bonus)
  - [ ] [Delete bonus](#delete-bonus)
  - [ ] [Modify bonus](#modify-bonus)
  - [ ] [Add category](#add-category)
  - [ ] [Delete category](#delete-category)
  - [ ] [Modify category](#modify-category)
  - [ ] [Add config](#add-config)
  - [ ] [Delete config](#delete-config)
  - [ ] [Modify config](#modify-config)
  - [ ] [Feedbacks list](#feedbacks-list)
  - [ ] [Feedbacks detail](#feedbacks-detail)
  - [ ] [Delete feedback](#delete-feedback)
  - [ ] [Modify feedback](#modify-feedback)
  - [ ] [Add goods](#add-goods)
  - [ ] [Delete goods](#delete-goods)
  - [ ] [Modify goods](#modify-goods)
  - [ ] [Orders list](#orders-list)
  - [ ] [Order detail](#order-detail)
  - [ ] [Delete order](#delete-order)
  - [ ] [Modify order](#modify-order)


  管理后台要有角色的概念，区分运营人员和管理员，以便鉴权用户能否执行特定操作。

## 说明

> 所有接口返回格式(json)：

```
{
  "success": false | true,
  "data": String | Object 成功时返回数据，失败时返回错误信息
}
```

## weapp接口，主要给小程序使用，接口前缀**/wx**，需要验证token，后台服务通过请求带的token，辨析用户

### Save user info

推送用户信息,后端保存。小程序登录后，通过小程序API，拿到加密的用户信息，再在后台解密后根据OpenID找到对应的数据库用户记录，更新用户信息。

  POST /wx/userinfo

Json Data:

| Field | Description | Optional | Remarks |
| ----- | ----------- | -------- | ------- |
| encryptedData  | 包括敏感数据在内的完整用户信息的加密数据         | no       |         |
| iv  | 加密算法的初始向量         | no       |         |

Return Example:

```
{
  success: true,
  data: "Save userinfo successfully"
}
```

### Current user

获取当前用户，小程序登录后，可以向后台服务请求当前用户信息

  GET /currentUser

### My bonus

获取我的红包，向后台服务查询当前用户的红包数据。

  GET /myBonus

### Make order

下单，用户完成商品选购后，向后台服务提交订单数据。

  POST /order

### Pay order

支付订单，用户使用微信支付来支付订单。

  POST /pay

### My orders

获取我的订单，用户查看自己的订单，可以看到订单的状态，金额等

  GET /orders

### Order detail

获取我的订单详情，用户查看一个订单的详情，包含订单所有信息。

  GET /order/:id

### Submit feedback

提交反馈，用户提交一个对程序的反馈，需要选择问题的类型和手机号，可选上传图片。

  POST /feedback

### Weapp upload to qiniu

在小程序中上传文件至七牛云

  POST /upload

## 共公接口，不程序及后台管理程序都有使用，接口前缀**/api**，主要是一些资源的获取，不需要验证token

### Wechat login   

wx登录，code换token，小程序登录，使用小程序和微信的接口，将code换取sessionKey，并拿到用户的OpenID，根据sessionKey构造一个token，在后续请求中带上这个token，以完成鉴权。最后将这些信息作为用户的基本信息在数据库中创建用户记录。

  POST /wxlogin

### Login

后台登录，管理后台登录接口，成功后返回jwt token，并在后续请求中带上这个token，后台验证这个token，以区分是否请求合法。

  POST /login

### Goods list

获取商品，在小程序和后台管理页面，请求分类下的商品列表数据，可以省略分类，以请求所有商品数据，在后期商品数多时，要考虑分页。

  GET /goods

### Goods detail

获取商品详情，在小程序和管理页面，请求商品的详情数据，包含商品所有信息。

  GET /goods/:id

### Banner list

获取Banner，在小程序和管理页面，请求Banner数据。

  GET /banners

### Banner detail

获取Banner，在小程序和管理页面，请求Banner的详情数据。此接口可能不需要，优先级低。

  GET /banner/:id

### Categories list

获取分类，在小程序和管理页面，请求商品分类数据。

  GET /categories

### Category detail

获取分类详情，在小程序和管理页面，请求商品分类详情数据。此接口可能不需要，优先级低。

  GET /category/:id

### Configs list

获取配置，在小程序和管理页面，请求程序配置信息。用来对小程序和系统的一些参数提供无需修改代码的功能实现。

  GET /configs

### Config detail

获取配置，在小程序和管理页面，请求配置的详情数据。此接口可能不需要，优先级低。

  GET /config/:id

## 管理后台接口，主要给管理后台使用，接口前缀**/admin**，需要验证jwt token

### Upload to qiniu

在后台管理端，上传文件至七牛云，将小程序要用到的图片，上传至七牛云，七牛云已配置CDN。

  POST /upload

### Add banner

新增Banner，新增一个Banner，图片暂时使用统一大小的图片，不在网页端提供图片截剪功能，图片上传至七牛云，并使用CDN。

  POST /banner

### Delete banner

删除Banner，删除一个Banner，软删除。

  DELETE /banner/:id

### Modify banner

修改Banner，修改Banner的数据，包括Banner的图片，指向的url等。

  PUT /banner/:id

### Bonuses list

获取红包，获取红包列表。

  GET /bonuses

### Bonus detail

获取红包详情，在管理后台查看红包详情数据。

  GET /bonus/:id

### Add bonus

新增红包，新增一个红包，根据红包的类型，最终生成用户红包，在订单中使用。

  POST /bonus

### Delete bonus

删除红包，删除红包，软删除。

  DELETE /bonus/:id

### Modify bonus

修改红包，红包不能更改，只能删除（软删除），不需要此接口。

  PUT /bonus/:id

### Add category

新增分类，新增一个商品分类。

  POST /category

### Delete category

删除分类，删除一个商品分类，软删除，当分类下有商品时，不能删除此分类。

  DELETE /category/:id

### Modify category

修改分类，修改分类的数据。

PUT /category/:id

### Add Config

新增配置，新增一个配置。

  POST /config

### Delete config

删除配置，删除一个配置，软删除。

  DELETE /config/:id

### Modify config

修改配置，修改一个配置的数据。

  PUT /config/:id

### Feedbacks list

获取反馈，查看用户的反馈记录。

  GET /feedbacks

### Feedbacks detail

获取反馈详情，查看反馈的详情。此接口可能不需要，优先级低。

  GET /feedback/:id

### Delete feedback

删除反馈，删除反馈。此接口可能不需要，优先级低。

  DELETE /feedback/:id

### Modify feedback

修改反馈。此接口可能不需要，优先级低。

PUT /feedback/:id

### Add goods

新增商品，在管理后台，新增一个商品。

  POST /goods

### Delete goods

删除商品，在管理后台，删除一个商品，软删除，当有订单含有此商品时，商品不能删除，但商品可以下架。

  DELETE /goods/:id

### Modify goods

修改商品，修改商品的数据，要考虑已经生成的订单中的商品数据如何保留不被变更。

  PUT /goods/:id

### Orders list

获取订单，在管理后台，查看订单列表。

  GET /orders

### Order detail

获取订单，在管理后台，查看订单的详情。

  GET /order/:id

### Delete order  

删除订单，软删除订单。

  DELETE /order/:id

### Modify order

修改订单，修改订单的数据。

  PUT /order/:id

