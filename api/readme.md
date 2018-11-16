
* 所有的请求均为 post 方法
* 请求协议为 jsonrpc 2.0
* 只有两个 api,   
  登录接口为 /json/user/login
  数据接口为 /json/api

* 更多的功能通过数据接口的不同参数来搞定  
* 登录接口的参数为 {'login':'my_account', 'password':'my_password'}
* 数据接口的参数 {'model': 'res.users', method: 'read', args: [1], kwargs: {}}
  其中 model 为 odoo 模型名
  method 为方法名 有search, search_read, read, write, create, unlink 
  args, kwargs 是参数, 


功能|方法名|参数|返回值|返回
---|-----|---|------|---
查找|search|domain|ids|查找到到所有记录到id列表
查找并读取|search_read|domain, fields|records|查找到到所有记录列表
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
vals|dict|{'name':'smith', 'email':'smith@odooht.com'}|创建或修改时, 各字段的值


domain 的格式


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
    
    """
    
    url = HOST + '/json/user/login'
    return jsonrpc(url, {'db': DB, 'login': login, 'password': password})
    
```

{'db': db,'login':user, 'password':psw, 'type':'account'}



其他接口雷同  
所有接口的 方法 都是 post




# 登录
/json/user/login

