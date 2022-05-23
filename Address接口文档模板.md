# Address接口文档模板

## 通过id获得地址信息

### 简要描述

**地址信息接口**

### 请求URL

`http://localhost:8080/MySMBMS/getaddressbyid`

### 请求方式

**POST**

### 参数

| 参数名       | 必选 | 类型   | 说明     |
| ------------ | ---- | ------ | -------- |
| id           | 是   | int    | 地址id   |
| contact      | 是   | String | 联系地址 |
| addressdesc  | 是   | String | 详细地址 |
| postcode     | 是   | String | 邮政编码 |
| tel          | 是   | String | 电话     |
| createby     | 是   | int    | 创建人id |
| creationdate |      | date   | 创建时间 |
| modifyby     |      | int    | 修改人id |
| modifydate   |      | date   | 修改时间 |
| userid       | 是   | int    | 用户id   |
| status       | 是   | int    | 状态     |

### 返回实例

![image-20220519164139556](C:\Users\SaoLinSiDaShiXiong\AppData\Roaming\Typora\typora-user-images\image-20220519164139556.png)

```json
{
 "id":1,
 "createby":1,
 "creationdate":"2022-05-18 09:58:24",
 "modifyby":1,
 "modifydate":"2022-05-18 09:58:29",
 "status":0,
 "contact":"陕西",
 "addressdesc":"陕西西安莲湖区",
 "postcode":"70001",
 "tel":"15539876830",
 "userid":1
}
```

### 返回参数说明

| 参数名       | 类型   | 说明                                                     |
| ------------ | ------ | -------------------------------------------------------- |
| id           | int    | 唯一值，表示一个地址列的id                               |
| contact      | String | 所处的地址                                               |
| addressdesc  | String | 更加详细的地址描述                                       |
| postcode     | String | 邮政编码                                                 |
| tel          | String | 电话号码，可以是座机                                     |
| createby     | int    | 创建该信息的员工的id号                                   |
| creationdate | date   | 创建的时间                                               |
| modifyby     | int    | 最后一次修改信息的员工id                                 |
| modifydate   | date   | 最后一次修改信息的时间                                   |
| userid       | int    | 对应用户表（user）的id，该表信息对应用户表中的一个用户。 |
| status       | int    | 使用状态 0：正常使用。1：删除状态                        |

### 备注

该Servlet的作用主要是用于通过id返回响应的地址信息，如果传入的id在数据库中不存在，则向前端返回一个`“null”`字符串。