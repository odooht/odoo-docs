

addons/base/models/ir_cron.py  

model = 'ir.cron'  

在这个模型中插入一条记录, 即可定义一个定时服务  



model|field|String|type|note
-----|-----|------|----|----
ir.cron|ir_actions_server_id||Many2one|ir.actions.server<br>delegate=True
ir_actions_server_id|name|Name|Char|
ir_actions_server_id|model_id||Many2one|ir.model
ir_actions_server_id|state||Selection|('code', 'Execute Python Code'),
ir_actions_server_id|code||Text|python 代码:<br>model.a_mthod()
ir.cron|interval_number|Repeat every x.|Integer|
ir.cron|interval_type|Interval Unit|Selection|('minutes', 'Minutes'),<br>('hours', 'Hours'),<br>('days', 'Days'),<br>('weeks', 'Weeks'),<br>('months', 'Months')
ir.cron|numbercall|Number of Calls|Integer|default=1, <br>help='How many times the method is called,\n<br>a negative number indicates no limit.'
ir.cron|nextcall|Next Execution Date|Datetime|default=fields.Datetime.now, <br>help="Next planned execution date for this job."

继承自 ir.actions.server, 自动使用其中的字段
名称: name
定时间隔:  interval_number, interval_type
首次执行时间:  nextcall, 默认是当前
任务执行对应的模型: model_id
任务执行对应的动作: state  . 目前只掌握 code 一种方法
任务执行对应的代码: code .
  掌握一种写法,  model.a_method()
  a_method 在模型中定义

