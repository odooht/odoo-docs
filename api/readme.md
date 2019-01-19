
* 所有的请求均为 post 方法
* 请求协议为 jsonrpc 2.0
* 只有两个 api,   
  登录接口为 /json/user/login  
  数据接口为 /json/api

* 更多的功能通过数据接口的不同参数来搞定  
* 登录接口的参数为 {db:'database_name', 'login':'my_account', 'password':'my_password'}
* 数据接口的参数 {'model': 'res.users', method: 'read', args: [1], kwargs: {}}  
  其中 model 为 odoo 模型名  
  method 为方法名 有search, search_read, read, write, create, unlink   
  args, kwargs 是参数,   


功能|方法名|参数|返回值|返回
---|-----|---|------|---
查找|search|domain, fields=[], <br>offset=0, limit=None, order=None|ids|查找到到所有记录到id列表
查找并读取|search_read|domain=[], fields=[], <br>offset=0, limit=None, order=None |records|查找到到所有记录列表
读取|read|id或ids,fields|records|对应到所有到记录列表
创建|create|vals|id|新创建的记录的id
更新|write|id, vals|boolean|true或false
删除|unlink|id|boolean|true或false


参数名|数据类型|举例|说明
-----|-------|---|----
domain|list|[('name','like','smith')]|查询条件, 自定义的格式, 后续详细说明
id|int|2|记录的id, 整型数
ids|list|[1,2,3]|记录的id列表, 列表, 其中的元素是id
fields|list|['name','login','email']|查询的哪些字段, 列表, 其中的元素是字段名
offset|int|0|被忽略跳过的记录数,默认为0
limit|int|0|限制返回的记录数,默认为0,不限制
order|char|id desc,name|排序条件
vals|dict|{'name':'smith',<br>'email':'smith@odooht.com'}|创建或修改时, 各字段的值
records|list|[record]|查询到到结果, 列表, 其中的元素是record
record|dict|[{'id':1, 'name':'smith',<br>'email':'smith@odooht.com'}]|记录, 字典, key-value键值对, key是字段, value是字段的值


domain 的格式  
domain 是列表, 这个列表构成一个“前缀表达式顺序的逻辑运算”
该逻辑运算, 由 &, |, !, (与或非), 及表达式组成.
与运算符 & 可以省略

例如:  
[['name','like','smith']]  
[['name','like','smith'],['age','>',30]]  
[|, ['age','<',12],['age','>',60]]  


逻辑运算  

符号|含义|例子
---|----|---
&|与|
\||或|
!|非|
expression|比较表达式|

比较表达式的格式  
比较表达式是一个列表, 三个元素   
第一个元素是字段名
第二个元素是比较运算符  
第三个元素是被比较的值  

比较运算符  

符号|说明
---|---
=|等于
!=|不等于
\>|等于
\>=|大于等于
<|小于
<=|小于等于
=?|未设置或等于
=like|模糊匹配,从头开始
like|模糊匹配,任意位置
not like|
ilike|不分大小写的like
not ilike|
=ilike|不分大小写的ilike
in|包含于
not in|不包含于
child\_of| 是...的儿子
parent\_of| 是...的父亲


字段的数据类型

类型名|中文名|说明
-----|-----|---
Integer|整型数|
Float|浮点数|
Char|字符串|
Date|日期|
Datetime|时间|
Selection|选择项|数据库中是Char型,   其值必须是有限的几个可选固定值
Many2one|多对一|数据库中是Integer,   对应另外一个模型的id
One2many|一对多|对应另外一个模型的多个id,   对应模型中必须有一个相应的Many2one字段.   数据库中不存储. 
Many2many|多对多|对应另外一个模型的多个id.   数据库中以关系表的方式存储,   关系表中存储两个模型的id


字段读取时的格式

类型名|格式|例子
-----|---|----
Integer||2
Float||-23.23
Char||'smith'
Date|'YYYY-MM-DD'|'2018-10-10'
Datetime|'YYYY-MM-DD hh-mm-ss'|'2018-10-10 10:10:10'
Selection||'customer'
Many2one|键值对,key是id,  value是对应模型的name字段的值|[1,'apple']
One2many|列表,元素为id|[1,2,3]
Many2many|同One2many|

字段写入时的格式

类型名|格式|例子
-----|---|----
Integer||2
Float||-23.23
Char||'smith'
Date|'YYYY-MM-DD'|'2018-10-10'
Datetime|'YYYY-MM-DD hh-mm-ss'|'2018-10-10 10:10:10'
Selection|写入时,必须是有效的值|'customer'
Many2one|整型 id|1
One2many|列表,元素是特殊格式,  见下表|[(4,,1),(4,,2)]
Many2many|同One2many|


One2many Many2many字段写入时的格式  
列表list, 其元素是一个三元素的列表,  定义了对 One2many或Many2many字段的具体操作  

对One2many或Many2many字段的具体操作  
是一个三元素的列表,   
第一个元素定义了操作类型, 整型数,  值域: 0,1,2,3,4,5,6  
第二个元素是参数1  
第三个元素是参数2  

操作|功能|参数1|参数2|例子|不适用于|不适用于|说明
--|---|----|----|----|---|----|---
0|create||vals|(0,None,{'name':'smith'})|||以参数2做vals,在对应模型中新增记录 
1|write|id|vals|(1,1,{'name':'smith'})|||以参数1为id,参数2做vals,在对应模型中修改记录 
2|unlink|id||(2,1,)||create|以参数1为id,在对应模型中删除记录. 
3|remove relation|id||(3,1,)|One2many|create|以参数1为id,删除与对应模型的关联关系. 
4|add relation|id||(4,1,)|One2many||以参数1为id,将对应模型中的记录, 加到关系表中. 
5|remove all relation|||(5,)|One2many|create|删除所有的与对应模型的关联关系
6|replace all relation||ids|(6,,[1,2,3])|One2many||以参数2为ids, 替换与对应模型的所有关联关系



```
import requests
import json

import random

def jsonrpc(url, data=None, params=None, sid=None):
    """ 
    odoo jsonrpc 请求
    
    参数: 
    url:  api地址, 例如,登录地址为: 'http://192.168.1.10:8069/json/user/login'
    data: 请求的数据包, 如 登录的数据包为 {'login':'myaccount', 'password':'mypassword'}
    params: 请求的参数
    sid: session id, 如果该请求需要登录后才可以访问, 则提供 session id.
         session id 通过调用登录请求获取
    
    请求响应:
    response.status_code 为请求状态码, 200 表示请求被正确响应
    response.content 为响应的内容, json 类型
    
    content 的详细格式为: 
    {   "result": {uid:1}, 
        "error": {"code": 100,  "data": {},  "message": "" }
        "id": 123, 
        "jsonrpc": "2.0"
    }
    
    其中: 
       "jsonrpc": "2.0"  为固定格式
       "id" 为发送请求时在data中所传的id
       "error" 为服务器返回的error消息
       "result" 为 服务器返回的结果, 具体格式依赖于发送请求时的 data
       
       result 与 error 二者只有一个
    
    """

    headers = {"content-type": "application/json"  }
    data = {
        "jsonrpc":"2.0",
        "method":"call",
        "id":random.randint(0, 1000000000),
        "params":data and data or {}
    }

    params = params and params or {}
    if sid:                      
        params.update( {'session_id':usid} )

    response = requests.post(
        url,
        headers=headers,
        params=params,
        data=json.dumps(data)
    )
    
    content = json.loads(response.content)
    return content

HOST = 'http://192.168.1.10:8069'
DB = 'TT'

def login(login,password):
    """
    参数:  
    login: 登录账号
    password: 登录密码
    
    返回result:
    sid: session id
    uid: 用户id
    
    登录成功后, 将sid保存 备用. 
    
    """
    
    url = HOST + '/json/user/login'
    return jsonrpc(url, {'db': DB, 'login': login, 'password': password})

def call(model,method, args=[], kwargs={}):
    """
    参数:  
    model: 模型名
    method: 方法名
    args: 参数列表
    kwargs: 参数字典
    kwargs['context']['token']: session id
    
    返回result:
    方法不同, 返回的 result 格式不同
    
    """
    
    token = kwargs['context']['token']
    url = HOST + '/json/api?session_id=' + token
    return jsonrpc(url, {'model': model, 'method': method, 'args': args, kwargs: kwargs})
    
```

