
## calendar

![calendar](https://github.com/odooht/odoo-docs/blob/master/model/image/calendar.png)

model|中文名字|note
-----|-------|----
calendar.contacs|通讯录|
calendar.event|事件|
calendar.event.type|事件标签|
calendar.event.attendee|听众|
calendar.alarm|提醒|

## 说明
* 这个模块可以玩待办事项?


model|field|String|type|note
-----|-----|------|----|----
calendar.contacts|user_id||Many2one|'res.users', 'Me'
calendar.contacts|partner_id||Many2one|'res.partner', 'Employee'
calendar.contacts|active||Boolean|Active


model|field|String|type|note
-----|-----|------|----|----
calendar.attendee|state|Status|Selection|STATE_SELECTION
calendar.attendee|common_name||Char|Common name
calendar.attendee|partner_id||Many2one|'res.partner', 'Contact'
calendar.attendee|email||Char|Email
calendar.attendee|availability||Selection|[('free', 'Free'), ('busy', 'Busy')]
calendar.attendee|access_token||Char|Invitation Token
calendar.attendee|event_id||Many2one|'calendar.event', 'Meeting linked'


model|field|String|type|note
-----|-----|------|----|----
calendar.alarm|name||Char|Name
calendar.alarm|type||Selection|[('notification', 'Notification'), <br/>('email', 'Email')]
calendar.alarm|duration||Integer|Remind Before
calendar.alarm|interval||Selection|
calendar.alarm|duration_minutes||Integer|Duration in minutes


model|field|String|type|note
-----|-----|------|----|----
calendar.event.type|name||Char|Name


model|field|String|type|note
-----|-----|------|----|----
calendar.event|name||Char|Meeting Subject
calendar.event|state|Status|Selection|[('draft', 'Unconfirmed'), <br/>('open', 'Confirmed')]
calendar.event|is_attendee||Boolean|Attendee
calendar.event|attendee_status|Attendee Status|Selection|Attendee.STATE_SELECTION
calendar.event|display_time||Char|Event Time
calendar.event|display_start||Char|Date
calendar.event|start||Datetime|Start
calendar.event|stop||Datetime|Stop
calendar.event|allday||Boolean|All Day
calendar.event|start_date||Date|Start Date
calendar.event|start_datetime||Datetime|Start DateTime
calendar.event|stop_date||Date|End Date
calendar.event|stop_datetime||Datetime|End Datetime
calendar.event|duration||Float|Duration
calendar.event|description||Text|Description
calendar.event|privacy||Selection|[('public', 'Everyone'), <br/>('private', 'Only me'), <br/>('confidential', 'Only internal users')]
calendar.event|location||Char|Location
calendar.event|show_as||Selection|[('free', 'Free'), ('busy', 'Busy')]
calendar.event|res_id||Integer|Document ID
calendar.event|res_model_id||Many2one|'ir.model', 'Document Model'
calendar.event|res_model||Char|Document Model Name
calendar.event|activity_ids|Activities|One2many|'mail.activity', 'calendar_event_id'
calendar.event|message_ids||One2many|
calendar.event|rrule||Char|Recurrent Rule
calendar.event|rrule_type|Recurrence|Selection|[('daily', 'Day(s)'),('weekly', 'Week(s)'),<br/>('monthly', 'Month(s)'),('yearly', 'Year(s)') ]
calendar.event|recurrency||Boolean|Recurrent
calendar.event|recurrent_id||Integer|Recurrent ID
calendar.event|recurrent_id_date||Datetime|Recurrent ID date
calendar.event|end_type|Recurrence Termination|Selection|[('count', 'Number of repetitions'),<br/>('end_date', 'End date') ]
calendar.event|interval|Repeat Every|Integer|
calendar.event|count|Repeat|Integer|
calendar.event|mo||Boolean|Mon
calendar.event|tu||Boolean|Tue
calendar.event|we||Boolean|Wed
calendar.event|th||Boolean|Thu
calendar.event|fr||Boolean|Fri
calendar.event|sa||Boolean|Sat
calendar.event|su||Boolean|Sun
calendar.event|month_by|Option|Selection|[('date', 'Date of month') , <br/>('day', 'Day of month')]
calendar.event|day||Integer|Date of month
calendar.event|week_list|Weekday|Selection|[('MO', 'Monday'),('TU', 'Tuesday'), <br/>('WE', 'Wednesday'),('TH', 'Thursday'), <br/>('FR', 'Friday'),('SA', 'Saturday'), <br/>('SU', 'Sunday')]
calendar.event|byday|By day|Selection|[('1', 'First'),('2', 'Second'),<br/>('3', 'Third'),('4', 'Fourth'),<br/>('5', 'Fifth'),('-1', 'Last')]
calendar.event|final_date||Date|Repeat Until
calendar.event|user_id||Many2one|'res.users', 'Owner'
calendar.event|partner_id|Responsible|Many2one|res.partner
calendar.event|active||Boolean|Active
calendar.event|categ_ids||Many2many|
calendar.event|attendee_ids||One2many|
calendar.event|partner_ids|Attendees|Many2many|
calendar.event|alarm_ids|Reminders|Many2many|'calendar.alarm', <br/>'calendar_alarm_calendar_event_rel'
calendar.event|is_highlighted|Is the Event Highlighted|Boolean|_compute_is_highlighted


