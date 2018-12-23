源码 

http://nightly.odoo.com/12.0/nightly/src/odoo_12.0.latest.zip  


## 010 base-res
base 模块缺省自动安装,
res 资源类, 包括 partner, users, company 等.
ir 内部资源类, 包括 model, module, view, menu, action 等.

## 011 base\_address\_city
 城市

## 020 bus
 bus 模块是消息总线

## 021 mail
 mail 模块, 依赖bus模块

## 030 sale_team
 销售团队 模块, 依赖 mail模块.
   sale 模块 与 crm 模块, 共享

## 032 crm
 CRM 模块, 依赖 销售团队, mail模块. 管理商机, 线索.

## 040 project
 项目管理 模块, 依赖 mail模块. 管理项目 任务 等.

## 051 uom
 度量单位 模块. 
从 产品模块中拆分出来, 在分析模块中 有使用.

## 052 product
 产品 模块.  依赖 mail模块, uom 模块

## 060 analytic
 分析 模块.  依赖 mail模块, uom 模块
从财务模块拆分出来 服务于 财务 和 hr_timesheet 模块

## 070 account
 财务 模块.  依赖 产品模块, 分析模块  
* 071 account.account 科目
* 072 account.move    会计凭证
* 073 account.invoice 发票
* 074 account.payment 收付款
* 075 account.bank.statement 银行对账单

## 80 中国本地 财务 城市
* l10n\_multilang 多语言科目
* l10n\_cn 中国会计科目 及 省数据
* l10n\_cn\_city 中国城市
* l10n\_cn\_standard      中国企业会计准则
* l10n\_cn\_small\_business  中国小企业会计制度

## 090 payment.md
  payment 模块, 依赖 财务模块

## 101 sale
 销售 模块, 依赖 销售团队 和 payment模块

## 102 sale_crm
 管理商机转销售, 依赖 销售模块 和 CRM模块

