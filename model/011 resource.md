## resource

![resource](https://github.com/odooht/odoo-docs/blob/master/model/image/resource.png)

## 说明
* 员工是一种资源
* 项目管理模块使用这个模块
* 其他的工时管理, 生成模块等 可能会使用这个模块


model|中文名字|note
-----|-------|----
resource.resource|资源|
resource.calendar|资源日历|
resource.calendar.attendance|资源日历工时|
resource.calendar.leave|资源日历假期|




model|field|String|type|note
-----|-----|------|----|----
resource.calendar|name||Char|
resource.calendar|company_id|Company|Many2one|'res.company'
resource.calendar|attendance_ids|Working Time|One2many|resource.calendar.attendance, <br/>calendar_id
resource.calendar|leave_ids|Leaves|One2many|resource.calendar.leaves, <br/>calendar_id
resource.calendar|global_leave_ids|Global Leaves|One2many|resource.calendar.leaves,<br/>calendar_id
resource.calendar|hours_per_day|Average hour per day|Float|
resource.calendar|tz|Timezone|Selection|


model|field|String|type|note
-----|-----|------|----|----
resource.calendar.attendance|name||Char|
resource.calendar.attendance|dayofweek|Day of Week|Selection|[('0', 'Monday'),('1', 'Tuesday'),<br/>('2', 'Wednesday'),('3', 'Thursday'),<br/>('4', 'Friday'),('5', 'Saturday'),<br/>('6', 'Sunday')]    
resource.calendar.attendance|date_from|Starting Date|Date|
resource.calendar.attendance|date_to|End Date|Date|
resource.calendar.attendance|hour_from|Work from|Float|
resource.calendar.attendance|hour_to|Work to|Float|
resource.calendar.attendance|calendar_id|Resource's Calendar|Many2one|resource.calendar
resource.calendar.attendance|day_period||Selection|[('morning', 'Morning'), <br/>('afternoon', 'Afternoon')]


model|field|String|type|note
-----|-----|------|----|----
resource.resource|name||Char|
resource.resource|active|Active|Boolean|
resource.resource|company_id|Company|Many2one|res.company
resource.resource|resource_type|Resource Type|Selection|[('user', 'Human'), <br/>('material', 'Material')]       
resource.resource|user_id|User|Many2one|
resource.resource|time_efficiency|Efficiency Factor|Float|
resource.resource|calendar_id|Working Time|Many2one|resource.calendar
resource.resource|tz|Timezone|Selection|


model|field|String|type|note
-----|-----|------|----|----
resource.calendar.leaves|name|Reason|Char|
resource.calendar.leaves|company_id|Company|Many2one|res.company
resource.calendar.leaves|calendar_id|Working Hours|Many2one|resource.calendar
resource.calendar.leaves|date_from|Start Date|Datetime|
resource.calendar.leaves|date_to|End Date|Datetime|
resource.calendar.leaves|resource_id|Resource|Many2one|resource.resource
resource.calendar.leaves|time_type||Selection|[('leave', 'Leave'),<br/> ('other', 'Other')]


model|field|String|type|note
-----|-----|------|----|----
resource.mixin|resource_id|Resource|Many2one|resource.resource
resource.mixin|company_id|Company|Many2one|res.company
resource.mixin|resource_calendar_id|Working Hours|Many2one|resource.calendar
resource.mixin|tz|Timezone|Selection|


model|field|String|type|note
-----|-----|------|----|----
res.company|resource_calendar_ids|Working Hours|One2many|resource.calendar,<br/>company_id
res.company|resource_calendar_id|Default Working Hours|Many2one|resource.calendar

model|field|String|type|note
-----|-----|------|----|----
res.users|resource_ids|Resources|One2many|resource.resource, <br/>user_id
res.users|resource_calendar_id|Default Working Hours|Many2one|resource.calendar
















