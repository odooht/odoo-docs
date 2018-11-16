jsonrpc

三个接口:
+ /jsonrpc/common
+ /jsonrpc/db
+ /jsonrpc/object

不能跨域访问, 
后端用 python 通过 request 等插件可以访问. 
前端用 js 不能访问, ------ 未严格测试

odoo 11 在这里  
odoo.http.CommonController

odoo 12 在这里  
odoo.addons.base.controllers.rpc.RPC

  odoo.http.dispatch_rpc
    /jsonrpc/common: odoo.service.common.dispatch
    /jsonrpc/db:     odoo.service.db.dispatch
    /jsonrpc/object: odoo.service.model.dispatch
    
odoo.service.common
  method in [login, authenticate, version, about, set_loglevel]
  
  uid = login(db, login, password)
  uid = authenticate(db, login, password, context) 带本地化参数
  
odoo.service.db
  method in [create_database, duplicate_database, drop, dump, restore, 
             rename, change_admin_password, migrate_databases
             db_exist, list, list_countries, server_version]

odoo.service.model
  method in [excute, 'execute_kw']  两种传参数的方式
  execute_kw(db, uid, password, model, method, args, kw=None)
  execute(   db, uid, password, model, method, *args, **kw)


