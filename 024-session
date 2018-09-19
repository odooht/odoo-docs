odoo.http.Root
  setup_session
  
几种传 session_id 的方式
/url?session_id=xxx--here.is.session.string--xxx

sid = httprequest.args.get('session_id')
sid = httprequest.headers.get("X-Openerp-Session-Id")
sid = httprequest.cookies.get('session_id')
httprequest.session = self.session_store.new()
httprequest.session = self.session_store.get(sid)
explicit_session

session 超期 出什么提示？

