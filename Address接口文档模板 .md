# Address接口文档模板

## 通过id获得地址信息

### 简要描述

**地址信息接口**

### 请求URL

`http://localhost:8080/MySMBMS/address/findonebyid`

### 请求方式

**POST**

### 传入参数

| 参数名 | 必选 | 类型 | 说明                 |
| ------ | ---- | ---- | -------------------- |
| id     | 是   | int  | 需要进行查询的地址id |

#### GET请求连接

`http://localhost:8080/MySMBMS/address/findonebyid?id=1`

该请求会返回id为1的地址信息列表的json对象

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

**使用该Servlet必须要传入一个int类型的参数，该参数为需要查询的id**

该Servlet的作用主要是用于通过id返回相应的地址信息的json数据，如果传入的id在数据库中不存在，则向前端返回一个`“null”`字符串。

****

## 获得所有地址信息

### 简要描述

**地址信息接口**

### 请求URL

`http://localhost:8080/MySMBMS/address/findall`

### 请求方式

**POST**

### 传入参数

**该请求不需要传入参数**

#### GET请求连接

`http://localhost:8080/MySMBMS/address/findall`

该请求会返回address列表中所有信息对象的json数据

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

![image-20220520093804597](C:\Users\SaoLinSiDaShiXiong\AppData\Roaming\Typora\typora-user-images\image-20220520093804597.png)

```json
[
    {
        "id":1,
        "createby":1,
        "creationdate":"2022-05-18 09:58:24",
        "modifyby":1,
        "modifydate":"2022-05-18 09:58:29",
        "status":0,"
        contact":"陕西",
        "addressdesc":"陕西西安莲湖区",
        "postcode":"70001",
        "tel":"15539876830",
        "userid":1
    },{
        "id":2,
        "createby":1,
        "creationdate":"2022-05-20 09:35:45",
        "modifyby":1,
        "modifydate":"2022-05-20 09:35:49",
        "status":0,
        "contact":"广西",
        "addressdesc":"广西银滩",
        "postcode":"530000",
        "tel":"164864651364",
        "userid":2
    }
]
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

该Servlet的作用主要是用于返回address表中所有的信息集合，最终返回结果会是一个json类型的二维数组，如果表中没有任何数据，则返回一个`“null”`的字符串。

****

## 获得地址信息的总记录数

### 简要描述

**地址信息接口**

### 请求URL

`http://localhost:8080/MySMBMS/address/conunt`

### 请求方式

**POST**

### 传入参数

**该请求不需要传入参数**

#### GET请求连接

`http://localhost:8080/MySMBMS/address/count`

该请求会返回address表中的所有记录数。

### 参数

| 参数名 | 必选 | 类型 | 说明     |
| ------ | ---- | ---- | -------- |
| count  | 是   | int  | 总记录数 |



### 返回实例

![image-20220522164945625](C:\Users\SaoLinSiDaShiXiong\AppData\Roaming\Typora\typora-user-images\image-20220522164945625.png)

```json
•{count:2}
```

### 返回参数说明

**一个数字，如果数据库表中没有记录为空，则返回0。**

### 备注

该Servlet的作用主要是用于返回address表中所有信息的总记录数，表中若没有记录则返回0。

****

## 通过条件地址信息的模糊查询

### 简要描述

通过在连接中给入需要查询的字段名，和查询条件来进行模糊查询，最终会响应满足条件的所有信息的json数据

**地址信息接口**

### 请求URL

`http://localhost:8080/MySMBMS/address/findbycondition`

### 请求方式

**POST**

### 传入参数

| 参数      | 必选 | 类型   | 说明                                           |
| --------- | ---- | ------ | ---------------------------------------------- |
| column    | 是   | String | 字段名，数据库表中对应的列名。                 |
| condition | 是   | String | 字段信息，最通过该信息在指定列中进行模糊查询。 |

**该请求不需要传入参数**

#### GET请求连接

`http://localhost:8080/MySMBMS/address/findbycondition?column=id&condition=1`

该请求会返回address表中所有列名为`column`指定的列中包含`condition`指定参数的地址信息。**即通过筛选条件在指定列中进行模糊查询**。

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

![image-20220522175548044](C:\Users\SaoLinSiDaShiXiong\AppData\Roaming\Typora\typora-user-images\image-20220522175548044.png)

```json
[
    {
        "id":1,
        "createby":1,
        "creationdate":"2022-05-18 09:58:24",
        "modifyby":1,
        "modifydate":"2022-05-18 09:58:29",
        "status":0,"
        contact":"陕西",
        "addressdesc":"陕西西安莲湖区",
        "postcode":"70001",
        "tel":"15539876830",
        "userid":1
    },{
        "id":2,
        "createby":1,
        "creationdate":"2022-05-20 09:35:45",
        "modifyby":1,
        "modifydate":"2022-05-20 09:35:49",
        "status":0,
        "contact":"广西",
        "addressdesc":"广西银滩",
        "postcode":"530000",
        "tel":"164864651364",
        "userid":2
    }
]
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

该Servlet的作用主要是用于进行模糊查询，<font color="#F00">**发送请求时，必须进行需要查询的字段名（column参数）的指定**</font>**如果没有指定查询条件（condition参数）的指定，如果condition参数为空，响应会返回数据库表中所有信息的json数据。**

****

## 添加地址信息

### 简要描述

通过form来提交地址信息，提交的信息会被添加进数据库

**地址信息接口**

### 请求URL

`http://localhost:8080/MySMBMS/address/add`

### 请求方式

**POST**

### 传入参数

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

#### <font color="#F00">**注意：**</font>

传入的参数中，id，createby，userid，status等类型为int的参数，不能由用户进行传入，<font color="#F00">该参数必须为数字，“且不能带有`空格`”</font>。

#### GET请求连接

`http://localhost:8080/MySMBMS/address/add?column=id&condition=1&......&status=0`

该请求会将传入的信息添加进数据库中的address表中

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

```json
{number:1}
```

### 返回参数说明

| 参数名 | 类型 | 说明                                          |
| ------ | ---- | --------------------------------------------- |
| number | int  | 数据库受影响的列数，正常情况下，添加成功返回1 |

### 备注

该Servlet的作用主要是用于进行地址信息的添加，信息添加成功则返回数据库中受影响的列数即返回`1`，添加失败则返回`0`

****

## 通过id进行地址信息的编辑

### 简要描述

通过form来提交地址信息，提交的信息会通过对应id找到数据库中对应的信息字段，并且会将传入的信息覆盖掉原有的信息。

**地址信息接口**

### 请求URL

`http://localhost:8080/MySMBMS/address/editbyid`

### 请求方式

**POST**

### 传入参数

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

#### <font color="#F00">**注意：**</font>

传入的参数中，id，createby，userid，status等类型为int的参数，不能由用户进行传入，<font color="#F00">该参数必须为数字，“且不能带有`空格`”</font>。

#### GET请求连接

`http://localhost:8080/MySMBMS/address/editbyid?column=id&condition=1&......&status=0`

该请求会通过id来将查找对应的信息，并进行修改。

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

```json
{number:1}
```

### 返回参数说明

| 参数名 | 类型 | 说明                                          |
| ------ | ---- | --------------------------------------------- |
| number | int  | 数据库受影响的列数，正常情况下，添加成功返回1 |

### 备注

该Servlet的作用主要是用于进行地址信息的修改，信息修改成功则返回数据库中受影响的列数即返回`1`，修改失败则返回`0`，如果传入的id在数据库中不存在，或者status（处于删除状态）同样会返回`0`。

****

## 通过id删除地址信息

### 简要描述

通过form来提交地址信息，提交的信息会通过对应id找到数据库中对应的信息字段，并且会将传入的信息覆盖掉原有的信息。

**地址信息接口**

### 请求URL

`http://localhost:8080/MySMBMS/address/editbyid`

### 请求方式

**POST**

### 传入参数

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

#### <font color="#F00">**注意：**</font>

传入的参数中，id，createby，userid，status等类型为int的参数，不能由用户进行传入，<font color="#F00">该参数必须为数字，“且不能带有`空格`”</font>。

#### GET请求连接

`http://localhost:8080/MySMBMS/address/ondeletebyid?id=1`

该请求会将address表中id列为`1`的字段信息调整为删除状态。

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

```json
{number:1}
```

### 返回参数说明

| 参数名 | 类型 | 说明                                          |
| ------ | ---- | --------------------------------------------- |
| number | int  | 数据库受影响的列数，正常情况下，添加成功返回1 |

### 备注

该Servlet的作用主要是用于进行地址信息的删除，信息删除成功则返回数据库中受影响的列数即返回`1`，删除失败则返回`0`，如果传入的id在数据库中不存在，或者status（处于删除状态）同样会返回`0`。

****