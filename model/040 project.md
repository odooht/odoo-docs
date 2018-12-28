## Project

![project](https://github.com/odooht/odoo-docs/blob/master/model/image/project.project.png)

## Project Task

![project](https://github.com/odooht/odoo-docs/blob/master/model/image/project.task.png)


model|中文名字|note
-----|-------|----
project.project|项目|
project.task|任务|
project.task.type|任务类型|
project.tags||


初始安装
* mail.message.subtype 增加几个类型
* mt\_task\_new, mt\_project\_task\_new 等



TBD 2018-12-22


model|field|String|type|note
-----|-----|------|----|----
res.partner|task_ids|Tasks|One2many|'project.task', 'partner_id'
res.partner|task_count|# Tasks|Integer|compute


model|field|String|type|note
-----|-----|------|----|----
project.task.type|name|Stage Name|Char|required=True
project.task.type|description||Text|
project.task.type|sequence||Integer|
project.task.type|project_ids|Projects|Many2many|project.project
project.task.type|legend_priority|Starred Explanation|Char|
project.task.type|legend_blocked||Char|Red Kanban Label
project.task.type|legend_done||Char|Green Kanban Label
project.task.type|legend_normal||Char|Grey Kanban Label
project.task.type|mail_template_id|Email Template|Many2one|mail.template
project.task.type|fold|Folded in Kanban|Boolean|
project.task.type|rating_template_id|Rating Email Template|Many2one|mail.template
project.task.type|auto_validation_kanban_state||Boolean|default=False


model|field|String|type|note
-----|-----|------|----|----
project.project|name||Char|Name
project.project|active||Boolean|default=True
project.project|sequence||Integer|default=10
project.project|partner_id|Customer|Many2one|res.partner
project.project|company_id|Company|Many2one|res.company
project.project|currency_id|Currency|Many2one|res.currency
project.project|favorite_user_ids|Members|Many2many|
project.project|is_favorite|Show Project on dashboard|Boolean|compute
project.project|label_tasks|Use Tasks as|Char|
project.project|tasks|Task Activities|One2many|'project.task', 'project_id'
project.project|resource_calendar_id|Working Time|Many2one|resource.calendar
project.project|type_ids|Tasks Stages|Many2many|'project.task.type',<br/>'project_task_type_rel', 'project_id'
project.project|task_count|Task Count|Integer|compute
project.project|task_ids|Tasks|One2many|'project.task', 'project_id'
project.project|color|Color Index|Integer|
project.project|user_id|Project Manage|Many2one|res.users
project.project|alias_id|Alias|Many2one|mail.alias
project.project|privacy_visibility|Privacy|Selection|default='portal'
project.project|doc_count|Number of documents attached|Integer|compute
project.project|date_start|Start Date|Date|
project.project|date|Expiration Date|Date|index=True
project.project|subtask_project_id|Sub-task Project|Many2one|project.project
project.project|percentage_satisfaction_task|Happy % on Task|Integer|store=True
project.project|rating_request_deadline||Datetime|
project.project|rating_status||Selection|
project.project|rating_status_period||Selection|
project.project|portal_show_rating||Boolean|Rating visible publicly


model|field|String|type|note
-----|-----|------|----|----
project.task|active||Boolean|default=True
project.task|name|Title|Char|required=True
project.task|description|Description|Html|
project.task|priority|Priority|Selection|default='0'
project.task|sequence|Sequence|Integer|
project.task|stage_id|Stage|Many2one|project.task.type
project.task|tag_ids|Tags|Many2many|project.tags
project.task|kanban_state|Kanban State|Selection|[('normal', 'Grey'),<br/>('done', 'Green'),<br/>('blocked', 'Red')]                        
project.task|kanban_state_label|Kanban State Label|Char|
project.task|create_date||Datetime|Created On
project.task|write_date||Datetime|Last Updated On
project.task|date_start|Starting Date|Datetime|
project.task|date_end|Ending Date|Datetime|index=True
project.task|date_assign|Assigning Date|Datetime|
project.task|date_deadline|Deadline|Date|index=True, copy=False
project.task|date_last_stage_update|Last Stage Update|Datetime|
project.task|project_id|Project|Many2one|project.project
project.task|notes|Notes|Text|
project.task|planned_hours||Float|Planned Hours
project.task|subtask_planned_hours||Float|Subtasks
project.task|user_id|Assigned to|Many2one|res.users
project.task|partner_id|Customer|Many2one|res.partner
project.task|manager_id|Project Manager|Many2one|res.users
project.task|company_id|Company|Many2one|res.company
project.task|color|Color Index|Integer|
project.task|user_email|User Email|Char|readonly=True
project.task|attachment_ids|Main Attachments|One2many|ir.attachment
project.task|displayed_image_id|Cover Image|Many2one|ir.attachment
project.task|legend_blocked|Kanban Blocked Explanation|Char|
project.task|legend_done|Kanban Valid Explanation|Char|readonly=True, related_sudo=False
project.task|legend_normal|Kanban Ongoing Explanation|Char|
project.task|parent_id|Parent Task|Many2one|index=True
project.task|child_ids|Sub-tasks|One2many|'project.task', 'parent_id'
project.task|subtask_project_id|Sub-task Project|Many2one|project.project
project.task|subtask_count||Integer|Sub-task count
project.task|email_from|Email|Char|index=True
project.task|email_cc|Watchers Emails|Char|
project.task|working_hours_open|Working hours to assign|Float|compute
project.task|working_hours_close|Working hours to close|Float|compute
project.task|working_days_open|Working days to assign|Float|compute
project.task|working_days_close|Working days to close|Float|compute
project.task|website_message_ids||One2many|


model|field|String|type|note
-----|-----|------|----|----
project.tags|name||Char|required=True
project.tags|color|Color Index|Integer|




