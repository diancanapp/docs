# api

- **接口**
  - [ ] [推送用户信息UserInfo](#user-info)
  - [Event: 'close'](#event-close)

## 说明

> 所有接口返回格式(json)：

```
{
  "success": false | true,
  "data": String | Object // 成功时返回数据，失败时返回错误信息
}
```

## weapp接口 

### UserInfo

推送用户信息,后端保存

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

### Event: 'close'

// 当前用户
GET /currentUser"
// 获取我的红包
GET /userBonus"
// 下单
POST /order"
// 支付订单
POST /pay"
// 获取我的订单
GET /orders"
// 获取我的订单
GET /order/:id"
// 提交反馈
POST /feedback"

## 通用接口

/api
// 上传文件至七牛云
POST /upload"
// wx登录，code换token
POST /wxlogin"
// 后台登录
POST /login"
// 获取商品
GET /goods"
// 获取商品
GET /goods/:id"
// 获取Banner
GET /banners"
// 获取Banner
GET /banner/:id"
// 获取分类
GET /categories"
// 获取分类
GET /category/:id"
// 获取配置
GET /configs"
// 获取配置
GET /config/:id"

## admin接口

/admin
// 新增Banner
POST /banner"
// 删除Banner
DELETE /banner/:id"
// 修改Banner
PUT /banner/:id"
// 获取红包
GET /bonuses"
// 获取红包
GET /bonus/:id"
// 新增红包
POST /bonus"
// 删除红包
DELETE /bonus/:id"
// 修改红包
PUT /bonus/:id"
// 新增分类
POST /category"
// 删除分类
DELETE /category/:id"
// 修改分类
PUT /category/:id"
// 新增配置
POST /config"
// 删除配置
DELETE /config/:id"
// 修改配置
PUT /config/:id"
// 获取反馈
GET /feedbacks"
// 获取反馈
GET /feedback/:id"
// 删除反馈
DELETE /feedback/:id"
// 修改反馈
PUT /feedback/:id"
// 新增商品
POST /goods"
// 删除商品
DELETE /goods/:id"
// 修改商品
PUT /goods/:id"
// 获取订单
GET /orders"
// 获取订单
GET /order/:id"
// 删除订单
DELETE /order/:id"
// 修改订单
PUT /order/:id"

