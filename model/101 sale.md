TBD 2018-12-22

model|field|String|type|note
-----|-----|------|----|----
sale.order|name|Order Reference|Char|
sale.order|origin|Source Document|Char|
sale.order|client_order_ref|Customer Reference|Char|
sale.order|reference|Payment Ref.|Char|
sale.order|state|Status|Selection|
sale.order|date_order|Order Date|Datetime|
sale.order|validity_date|Validity|Date|
sale.order|is_expired|Is expired|Boolean|
sale.order|require_signature||Boolean|Online Signature
sale.order|require_payment||Boolean|Online Payment
sale.order|remaining_validity_days|Remaining Validity Days|Integer|
sale.order|create_date|Creation Dat|Datetime|
sale.order|confirmation_date|Confirmation Date|Datetime|res.users
sale.order|user_id|Customer|Many2one|res.partner
sale.order|partner_id|Customer|Many2one|res.partner
sale.order|partner_invoice_id|Invoice Address|Many2one|res.partner
sale.order|partner_shipping_id|Delivery Address|Many2one|res.partner
sale.order|pricelist_id|Pricelist|Many2one|product.pricelist
sale.order|currency_id|Currency|Many2one|res.currency
sale.order|analytic_account_id||Many2one|'account.analytic.account', 'Analytic Account'
sale.order|order_line|Order Lines|One2many|'sale.order.line', 'order_id'
sale.order|invoice_count|Invoice Count|Integer|
sale.order|invoice_ids|Invoices|Many2many|account.invoice
sale.order|invoice_status|Invoice Status|Selection|
sale.order|note||Text|Terms and conditions
sale.order|amount_untaxed|Untaxed Amount|Monetary|store=True, readonly=True
sale.order|amount_by_group|Tax amount by group|Binary|
sale.order|amount_tax|Taxes|Monetary|store=True, readonly=True
sale.order|amount_total|Total|Monetary|store=True, readonly=True
sale.order|currency_rate||Float|Currency Rate
sale.order|payment_term_id|Payment Terms|Many2one|account.payment.term
sale.order|fiscal_position_id|Fiscal Position|Many2one|account.fiscal.position
sale.order|company_id||Many2one|'res.company', 'Company'
sale.order|team_id||Many2one|'crm.team', 'Sales Team'
sale.order|signature||Binary|Signature
sale.order|signed_by||Char|Signed by
sale.order|commitment_date||Datetime|Commitment Date
sale.order|expected_date||Datetime|"Expected Date"
sale.order|amount_undiscounted||Float|'Amount Before Discount'
sale.order|type_name||Char|Type Name
sale.order|transaction_ids|Transactions|Many2many|'payment.transaction', 'sale_order_transaction_rel', 'sale_order_id', 'transaction_id'
sale.order|authorized_transaction_ids|'Authorized Transactions'|Many2many|payment.transaction


model|field|String|type|note
-----|-----|------|----|----
sale.order.line||||

model|field|String|type|note
-----|-----|------|----|----
res.partner|order_id|Order Reference|Many2one|sale.order
res.partner|name|Description|Text|
res.partner|sequence|Sequence|Integer|
res.partner|invoice_lines|Invoice Lines|Many2many|'account.invoice.line', 'sale_order_line_invoice_rel', 'order_line_id', 'invoice_line_id'
res.partner|invoice_status|Invoice Status|Selection|
res.partner|price_unit||Float|Unit Price
res.partner|price_subtotal|Subtotal|Monetary|readonly=True, store=True
res.partner|price_tax|Total Tax|Float|readonly=True, store=True
res.partner|price_total|Total|Monetary|readonly=True, store=True
res.partner|price_reduce||Float|Price Reduce
res.partner|tax_id|Taxes|Many2many|account.tax
res.partner|price_reduce_taxinc|Price Reduce Tax inc|Monetary|readonly=True, store=True
res.partner|price_reduce_taxexcl|Price Reduce Tax excl|Monetary|readonly=True, store=True
res.partner|discount|Discount (%)|Float|
res.partner|product_id|Product|Many2one|product.product
res.partner|product_updatable|Can Edit Product|Boolean|
res.partner|product_uom_qty|Ordered Quantity|Float|
res.partner|product_uom|Unit of Measure|Many2one|uom.uom
res.partner|product_custom_attribute_value_ids|User entered custom product attribute values|One2many|'product.attribute.custom.value', 'sale_order_line_id'
res.partner|product_no_variant_attribute_value_ids|Product attribute values that do not create variants|Many2many|product.template.attribute.value
res.partner|product_image||Binary|Product Image
res.partner|qty_delivered_method|Method to update delivered qty|Selection|
res.partner|qty_delivered||Float|Delivered Quantity
res.partner|qty_delivered_manual||Float|'Delivered Manually
res.partner|qty_to_invoice|To Invoice Quantity|Float|
res.partner|qty_invoiced|Invoiced Quantity|Float|
res.partner|untaxed_amount_invoiced||Monetary|Untaxed Invoiced Amount
res.partner|untaxed_amount_to_invoice||Monetary|Untaxed Amount To Invoice
res.partner|salesman_id||Many2one|store=True, string='Salesperson', readonly=True
res.partner|currency_id||Many2one|store=True, string='Currency', readonly=True
res.partner|company_id|Company|Many2one|store=True, readonly=True
res.partner|order_partner_id||Many2one|store=True, string='Customer', readonly=False
res.partner|analytic_tag_ids|Analytic Tags|Many2many|account.analytic.tag
res.partner|analytic_line_ids|Analytic lines|One2many|account.analytic.line
res.partner|is_expense||Boolean|Is expense
res.partner|is_downpayment||Boolean|Is a down payment
res.partner|state|Order Status|Selection|readonly=True, copy=False, store=True, default='draft'
res.partner|customer_lead||Float| 'Delivery Lead Time'
res.partner|display_type||Selection|


model|field|String|type|note
-----|-----|------|----|----
crm.team|use_quotations|Quotations|Boolean|
crm.team|use_invoices||Boolean|
crm.team|invoiced|Invoiced This Month|Integer|
crm.team|invoiced_target|Invoicing Target|Integer|
crm.team|quotations_count|Number of quotations to invoice|Integer|
crm.team|quotations_amount|Amount of quotations to invoice|Integer|
crm.team|sales_to_invoice_count|Number of sales to invoice|Integer|
crm.team|dashboard_graph_model||Selection|


model|field|String|type|note
-----|-----|------|----|----
res.company|sale_note|Default Terms and Conditions|Text|translate=True
res.company|portal_confirmation_sign|Online Signature|Boolean|
res.company|portal_confirmation_pay|Online Payment|Boolean|
res.company|quotation_validity_days|Default Quotation Validity (Days)|Integer|
res.company|sale_quotation_onboarding_state||Selection|
res.company|sale_onboarding_order_confirmation_state|State of the sale onboarding panel|Selection|[('not_done', "Not done"), ('just_done', "Just done"), ('done', "Done"), ('closed', "Closed")]
res.company|sale_onboarding_sample_quotation_state|State of the onboarding confirmation order step|Selection|[('not_done', "Not done"), ('just_done', "Just done"), ('done', "Done")]
res.company|sale_onboarding_payment_method|State of the onboarding sample quotation step|Selection|[('not_done', "Not done"), ('just_done', "Just done"), ('done', "Done")]


model|field|String|type|note
-----|-----|------|----|----
product.template|service_type|Track Service|Selection|[('manual', 'Manually set quantities on order')]
product.template|sale_line_warn||Selection|
product.template|sale_line_warn_msg||Text|Message for Sales Order Line
product.template|expense_policy|'Re-Invoice Policy'|Selection| [('no', 'No'), ('cost', 'At cost'), ('sales_price', 'Sales price')]
product.template|sales_count|Sold|Float|
product.template|hide_expense_policy||Boolean|
product.template|invoice_policy|Invoicing Policy|Selection|[('order', 'Ordered quantities'),('delivery', 'Delivered quantities')]


model|field|String|type|note
-----|-----|------|----|----
product.product|sales_count|Sold|Float|


model|field|String|type|note
-----|-----|------|----|----
product.pricelist|discount_policy||Selection|[('with_discount', 'Discount included in the price'),('without_discount', 'Show public price & discount to the customer')]


model|field|String|type|note
-----|-----|------|----|----
payment.acquirer|so_reference_type|Communication|Selection|


model|field|String|type|note
-----|-----|------|----|----
payment.transaction|sale_order_ids|Sales Orders|Many2many|'sale.order', 'sale_order_transaction_rel', 'transaction_id', 'sale_order_id',
payment.transaction|sale_order_ids_nbr|# of Sales Orders|Integer|


model|field|String|type|note
-----|-----|------|----|----
account.analytic.line|so_line|sale.order.line|Many2one|Sales Order Item


model|field|String|type|note
-----|-----|------|----|----
account.invoice|team_id|Sales Team|Many2one|crm.team
account.invoice|comment||Text|
account.invoice|partner_shipping_id|Delivery Address|Many2one|'res.partner'


model|field|String|type|note
-----|-----|------|----|----
account.invoice.line|sale_line_ids|Sales Order Lines|Many2many|'sale.order.line','sale_order_line_invoice_rel','invoice_line_id', 'order_line_id',



