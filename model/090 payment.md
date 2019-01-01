TBD 2018-12-22


## account payment

![account payment](https://github.com/odooht/odoo-docs/blob/master/model/image/payment.png)


model|中文名字|note
-----|-------|----
account.payment|收付款单|
payment.acquirer|银行卡支付服务方|
payment.icon|图标|
payment.transaction|业务单据|
payment.token|api接口令牌|



model|field|String|type|note
-----|-----|------|----|----
account.payment|payment_transaction_id|Payment Transaction|Many2one|payment.transaction
account.payment|payment_token_id|Saved payment token|Many2one|payment.token


model|field|String|type|note
-----|-----|------|----|----
account.invoice|transaction_ids|Transactions|Many2many|'payment.transaction', 'account_invoice_transaction_rel', 'invoice_id', 'transaction_id'
account.invoice|authorized_transaction_ids|Authorized Transactions|Many2many|payment.transaction

model|field|String|type|note
-----|-----|------|----|----
res.partner|payment_token_ids||One2many|'payment.token', 'partner_id', 'Payment Tokens'
res.partner|payment_token_count||Integer|Count Payment Token


model|field|String|type|note
-----|-----|------|----|----
res.company|payment_acquirer_onboarding_state|State of the onboarding payment acquirer step|Selection|[('not_done', "Not done"), ('just_done', "Just done"), ('done', "Done")]
res.company|payment_onboarding_payment_method|Selected onboarding payment method|Selection|[('paypal', "PayPal"),('stripe', "Stripe"),('manual', "Manual"),('other', "Other"),]



model|field|String|type|note
-----|-----|------|----|----
payment.acquirer|name||Char|Name
payment.acquirer|description||Html|Description
payment.acquirer|sequence||Integer|Sequence
payment.acquirer|provider|Provider|Selection|default='manual', required=True
payment.acquirer|company_id||Many2one|'res.company', 'Company'
payment.acquirer|view_template_id||Many2one|'ir.ui.view', 'Form Button Template'
payment.acquirer|registration_view_template_id||Many2one|'ir.ui.view', 'S2S Form Template'
payment.acquirer|environment|Environment|Selection|('test', 'Test'),('prod', 'Production')
payment.acquirer|website_published||Boolean|Visible in Portal / Website
payment.acquirer|capture_manually|Capture Amount Manually|Boolean|
payment.acquirer|journal_id||Many2one|'account.journal', 'Payment Journal'
payment.acquirer|specific_countries|||
payment.acquirer|country_ids|Specific Countries|Boolean|'res.country', 'payment_country_rel',
payment.acquirer|pre_msg||Html|Help Message
payment.acquirer|post_msg||Html|Thanks Message
payment.acquirer|pending_msg||Html|Pending Message
payment.acquirer|done_msg||Html|Done Message
payment.acquirer|cancel_msg||Html|Cancel Message
payment.acquirer|error_msg||Html|Error Message
payment.acquirer|save_token|Save Cards|Selection|
payment.acquirer|token_implemented||Boolean|Saving Card Data supported
payment.acquirer|authorize_implemented||Boolean|Authorize Mechanism Supported
payment.acquirer|fees_implemented||Boolean|Fees Computation Supported
payment.acquirer|fees_active||Boolean|Add Extra Fees
payment.acquirer|fees_dom_fixed||Float|Fixed domestic fees
payment.acquirer|fees_dom_var||Float|Variable domestic fees (in percents)
payment.acquirer|fees_int_fixed||Float|Fixed international fees
payment.acquirer|fees_int_var||Float|Variable international fees (in percents)
payment.acquirer|qr_code||Boolean|Use SEPA QR Code
payment.acquirer|module_id|Corresponding Module|Many2one|ir.module.module
payment.acquirer|module_state|Installation State|Selection|
payment.acquirer|image||Binary|Image
payment.acquirer|image_medium||Binary|Medium-sized image
payment.acquirer|image_small||Binary|Small-sized image
payment.acquirer|payment_icon_ids|Supported Payment Icons|Many2many|payment.icon
payment.acquirer|payment_flow|Payment Flow|Selection|form', 'Redirection to the acquirer website
payment.acquirer|inbound_payment_method_ids||Many2many|account.payment.method


model|field|String|type|note
-----|-----|------|----|----
payment.icon|name|Name|Char|
payment.icon|acquirer_ids|Acquirers|Many2many|payment.acquirer
payment.icon|image||Binary|Image
payment.icon|image_payment_form||Binary|Image displayed on the payment form


model|field|String|type|note
-----|-----|------|----|----
payment.transaction|date||Datetime|Validation Date
payment.transaction|acquirer_id|Acquirer|Many2one|payment.acquirer
payment.transaction|provider|Provider|Selection|
payment.transaction|type||Selection|
payment.transaction|state|Status|Selection|default='draft', required=True, readonly=True
payment.transaction|state_message|Message|Text|
payment.transaction|amount|Amount|Monetary|
payment.transaction|fees||Many2one|'res.currency', 'Currency'
payment.transaction|currency_id||Many2one|res.currency', 'Currency',
payment.transaction|reference||Reference|
payment.transaction|acquirer_reference|Acquirer Reference|Char|
payment.transaction|partner_id||Many2one|'res.partner', 'Customer'
payment.transaction|partner_name||Char|Partner Name
payment.transaction|partner_lang||Selection|
payment.transaction|partner_email||Char|Email
payment.transaction|partner_zip||Char|Zip
payment.transaction|partner_address||Char|Address
payment.transaction|partner_city||Char|City
payment.transaction|partner_country_id||Many2one|'res.country', 'Country'
payment.transaction|partner_phone||Char|Phone
payment.transaction|html_3ds||Char|'3D Secure HTML'
payment.transaction|callback_model_id||Many2one|'ir.model', 'Callback Document Model'
payment.transaction|callback_res_id||Integer|'Callback Document ID'
payment.transaction|callback_method||Char|'Callback Method'
payment.transaction|callback_hash||Char|'Callback Hash'
payment.transaction|return_url||Char|'Return URL after payment'
payment.transaction|is_processed||Boolean|'Has the payment been post processed'
payment.transaction|payment_token_id||Many2one|'payment.token', 'Payment Token'
payment.transaction|payment_id|Payment|Many2one|'account.payment'
payment.transaction|invoice_ids|Invoices|Many2many|'account.invoice', 'account_invoice_transaction_rel', 'transaction_id', 'invoice_id'
payment.transaction|invoice_ids_nbr|# of Invoices|Integer|



model|field|String|type|note
-----|-----|------|----|----
payment.token|name||Char|Name
payment.token|short_name||Char|Short name
payment.token|partner_id||Many2one|'res.partner', 'Partner'
payment.token|acquirer_id||Many2one|'payment.acquirer', 'Acquirer Account'
payment.token|acquirer_ref||Char|'Acquirer Ref.'
payment.token|active||Boolean|'Active'
payment.token|payment_ids||One2many|'payment.transaction', 'payment_token_id', 'Payment Transactions'
payment.token|verified|Verified|Boolean|default=False



