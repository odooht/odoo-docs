源码 

http://nightly.odoo.com/12.0/nightly/src/odoo_12.0.latest.zip  

@[TOC]目录

## 10 base-res
base 模块缺省自动安装,
res 资源类, 包括 partner, users, company 等.
ir 内部资源类, 包括 model, module, view, menu, action 等.

[[11 base\_address\_city]] 城市

[[20 bus]] bus 模块是消息总线

[[21 mail]] mail 模块, 依赖bus模块

[[30 sale_team]] 销售团队 模块, 依赖 mail模块.
   sale 模块 与 crm 模块, 共享

[[32 crm]] CRM 模块, 依赖 销售团队, mail模块. 管理商机, 线索.

[[40 project]] 项目管理 模块, 依赖 mail模块. 管理项目 任务 等.

[[51 uom]] 度量单位 模块. 
从 产品模块中拆分出来, 在分析模块中 有使用.

[[52 product]] 产品 模块.  依赖 mail模块, uom 模块

[[60 analytic]] 分析 模块.  依赖 mail模块, uom 模块
从财务模块拆分出来 服务于 财务 和 hr_timesheet 模块

[[70 account]] 财务 模块.  依赖 产品模块, 分析模块
[[71 account.account]] 科目
[[72 account.move]]    会计凭证
[[73 account.invoice]] 发票
[[74 account.payment]] 收付款
[[75 account.bank.statement]] 银行对账单

[[80 l10n\_multilang]] 多语言科目
[[81 l10n\_cn]] 中国会计科目 及 省数据
[[83 l10n\_cn\_city]]

[[90 payment.md]]  payment 模块, 依赖 财务模块

[[101 sale.md]] 销售 模块, 依赖 销售团队 和 payment模块

[[102 sale_crm.md]] 管理商机转销售, 依赖 销售模块 和 CRM模块

