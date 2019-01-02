## resource

![resource](https://github.com/odooht/odoo-docs/blob/master/model/image/resource.png)



model|中文名字|note
-----|-------|----
resource.resource|资源|
resource.calendar|资源日历|
resource.calendar.attendance|资源日历工时|
resource.calendar.leave|资源日历假期|




model|field|String|type|note
-----|-----|------|----|----
resource.calendar|name||Char|
resource.calendar|company_id||Many2one|'res.company', 'Company'
resource.calendar|attendance_ids||One2many| 'resource.calendar.attendance', <br/>'calendar_id', 'Working Time'
resource.calendar|leave_ids||One2many|'resource.calendar.leaves', <br/>'calendar_id', 'Leaves'
resource.calendar|global_leave_ids||One2many|'resource.calendar.leaves',<br/> 'calendar_id', 'Global Leaves'
resource.calendar|hours_per_day||Float|Average hour per day
resource.calendar|tz|Timezone|Selection|


model|field|String|type|note
-----|-----|------|----|----
resource.calendar.attendance|name||Char|
resource.calendar.attendance|dayofweek||Selection|[('0', 'Monday'),('1', 'Tuesday'),<br/>('2', 'Wednesday'),('3', 'Thursday'),<br/>('4', 'Friday'),('5', 'Saturday'),<br/>('6', 'Sunday')]    
resource.calendar.attendance|date_from|Starting Date|Date|
resource.calendar.attendance|date_to|End Date|Date|
resource.calendar.attendance|hour_from|Work from|Float|
resource.calendar.attendance|hour_to|Work to|Float|
resource.calendar.attendance|calendar_id|Resource's Calendar|Many2one|resource.calendar
resource.calendar.attendance|day_period||Selection|[('morning', 'Morning'), <br/>('afternoon', 'Afternoon')]


model|field|String|type|note
-----|-----|------|----|----
resource.resource|name||Char|
resource.resource|active||Boolean|Active
resource.resource|company_id|Company|Many2one|res.company
resource.resource|resource_type|Resource Type|Selection|[('user', 'Human'), <br/>('material', 'Material')]       
resource.resource|user_id|User|Many2one|
resource.resource|time_efficiency||Float|Efficiency Factor
resource.resource|calendar_id|Working Time|Many2one|resource.calendar
resource.resource|tz|Timezone|Selection|


model|field|String|type|note
-----|-----|------|----|----
resource.calendar.leaves|name||Char|Reason
resource.calendar.leaves|company_id|Company|Many2one|res.company
resource.calendar.leaves|calendar_id||Many2one|'resource.calendar', 'Working Hours'
resource.calendar.leaves|date_from||Datetime|Start Date
resource.calendar.leaves|date_to||Datetime|End Date
resource.calendar.leaves|resource_id||Many2one|"resource.resource", 'Resource'
resource.calendar.leaves|time_type||Selection|[('leave', 'Leave'),<br/> ('other', 'Other')]


model|field|String|type|note
-----|-----|------|----|----
resource.mixin|resource_id||Many2one|'resource.resource', 'Resource'
resource.mixin|company_id||Many2one|'res.company', 'Company'
resource.mixin|resource_calendar_id||Many2one|'resource.calendar', 'Working Hours'
resource.mixin|tz|Timezone|Selection|


model|field|String|type|note
-----|-----|------|----|----
res.company|resource_calendar_ids||One2many|'resource.calendar',<br/> 'company_id',<br/> 'Working Hours'
res.company|resource_calendar_id||Many2one|'resource.calendar',<br/>  'Default Working Hours'

model|field|String|type|note
-----|-----|------|----|----
res.users|resource_ids||One2many|'resource.resource', <br/>'user_id', 'Resources'
res.users|resource_calendar_id||Many2one|'resource.calendar',<br/> 'Default Working Hours'
















