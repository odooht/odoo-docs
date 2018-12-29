TBD 2018-12-22

model|field|String|type|note
-----|-----|------|----|----
account.invoice|name|Reference/Description|Char|index=True,readonly=True
account.invoice|origin|Source Document|Char|readonly=True
account.invoice|type||Selection|
account.invoice|refund_invoice_id|Invoice for which this invoice is the credit note|Many2one|account.invoice
account.invoice|number|Journal Entry Name|Char|
account.invoice|move_name||Char|default=False, copy=False
account.invoice|reference|Payment Ref|Char|
account.invoice|comment||Text|Additional Information
account.invoice|state|Status|Selection|index=True, readonly=True, default='draft'
account.invoice|sent||Boolean|readonly=True, default=False, copy=False
account.invoice|date_invoice|Invoice Date|Date|
account.invoice|date_due|Due Date|Date|
account.invoice|partner_id|Partner|Many2one|res.partner
account.invoice|vendor_bill_id|Vendor Bill|Many2one|account.invoice
account.invoice|payment_term_id|Payment Terms|Many2one|account.payment.term
account.invoice|date|Accounting Date|Date|readonly=True
account.invoice|account_id|Account|Many2one|account.account
account.invoice|invoice_line_ids|Invoice Lines|One2many|'account.invoice.line', 'invoice_id'
account.invoice|tax_line_ids|Tax Lines|One2many|'account.invoice.tax', 'invoice_id'
account.invoice|refund_invoice_ids|Refund Invoices|One2many|'account.invoice', 'refund_invoice_id'
account.invoice|move_id|Journal Entry|Many2one|account.move
account.invoice|amount_by_group|Tax amount by group|Binary|
account.invoice|amount_untaxed|Untaxed Amount|Monetary|store=True, readonly=True
account.invoice|amount_untaxed_signed|Untaxed Amount in Company Currency|Monetary|store=True, readonly=True
account.invoice|amount_tax|Tax|Monetary|store=True, readonly=True
account.invoice|amount_total|||store=True, readonly=True
account.invoice|amount_total_signed|Total|Monetary|store=True, readonly=True
account.invoice|amount_total_company_signed|Total in Company Currency|Monetary|store=True, readonly=True
account.invoice|currency_id|Currency|Many2one|res.currency
account.invoice|company_currency_id|Company Currency|Many2one|res.currency
account.invoice|journal_id|Journal|Many2one|account.journal
account.invoice|company_id|Company|Many2one|res.company
account.invoice|reconciled|Paid/Reconciled|Boolean|store=True, readonly=True
account.invoice|partner_bank_id|Bank Account|Many2one|res.partner.bank
account.invoice|residual|store=True|Monetary|Amount Due
account.invoice|residual_signed|Amount Due in Invoice Currency|Monetary|store=True
account.invoice|residual_company_signed|Amount Due in Company Currency|Monetary|store=True
account.invoice|payment_ids|Payments|Many2many|'account.payment', 'account_invoice_payment_rel', 'invoice_id', 'payment_id'
account.invoice|payment_move_line_ids|Payment Move Lines|Many2many|account.move.line
account.invoice|user_id|Salesperson|Many2one|res.user
account.invoice|fiscal_position_id|Fiscal Position|Many2one|account.fiscal.position
account.invoice|commercial_partner_id|Commercial Entity|Many2one|res.partner
account.invoice|outstanding_credits_debits_widget||Text|
account.invoice|payments_widget||Text|
account.invoice|has_outstanding||Boolean|
account.invoice|cash_rounding_id|Cash Rounding Method|Many2one|account.cash.rounding
account.invoice|sequence_number_next|Next Number|Char|Next Number
account.invoice|sequence_number_next_prefix|Next Number Prefix|Char|
account.invoice|incoterm_id|Incoterm|Many2one|account.incoterms
account.invoice|source_email|Source Email|Char|
account.invoice|vendor_display_name||Char|store=True
account.invoice|invoice_icon||Char|store=False


model|field|String|type|note
-----|-----|------|----|----
account.invoice.line|name|Description|Text|
account.invoice.line|origin|Source Document|Char|
account.invoice.line|sequence||Integer|
account.invoice.line|invoice_id|Invoice Reference|Many2one|account.invoice
account.invoice.line|invoice_type||Selection|
account.invoice.line|uom_id|Unit of Measure|Many2one|uom.uom
account.invoice.line|product_id|Product|Many2one|product.product
account.invoice.line|product_image||Binary|Product Image
account.invoice.line|account_id|Account|Many2one|account.account
account.invoice.line|price_unit|Unit Price|Float|
account.invoice.line|price_subtotal|Amount (without Taxes)|Monetary| store=True, readonly=True
account.invoice.line|price_total|Amount (with Taxes)|Monetary| store=True, readonly=True
account.invoice.line|price_subtotal_signed|Amount Signed|Monetary|store=True, readonly=True
account.invoice.line|price_tax|Tax Amount|Monetary|
account.invoice.line|quantity|Quantity|Float|required=True
account.invoice.line|discount|Discount (%)|Float|
account.invoice.line|invoice_line_tax_ids|Taxes|Many2many|'account.tax','account_invoice_line_tax', 'invoice_line_id', 'tax_id'
account.invoice.line|account_analytic_id|Analytic Account|Many2one|account.analytic.account
account.invoice.line|analytic_tag_ids|Analytic Tags|Many2many|account.analytic.tag
account.invoice.line|company_id|Company|Many2one|res.company
account.invoice.line|partner_id|Partner|Many2one|res.partner
account.invoice.line|currency_id||Many2one|res.currency
account.invoice.line|res.currency||Many2one|res.currency
account.invoice.line|is_rounding_line|Rounding Line|Boolean|
account.invoice.line|display_type||Selection|


model|field|String|type|note
-----|-----|------|----|----
account.invoice.tax|invoice_id|Invoice|Many2one|account.invoice
account.invoice.tax|name|Tax Description|Char|required=True
account.invoice.tax|tax_id|Tax|Many2one|account.tax
account.invoice.tax|account_id|Tax Account|Many2one|account.account
account.invoice.tax|account_analytic_id|Analytic account|Many2one|account.analytic.account
account.invoice.tax|analytic_tag_ids|Analytic Tags|Many2many|account.analytic.tag
account.invoice.tax|amount||Monetary|Tax Amount
account.invoice.tax|amount_rounding||Monetary|Amount Delta
account.invoice.tax|amount_total|Amount Total|Monetary|
account.invoice.tax|manual||Boolean|
account.invoice.tax|sequence||Integer|
account.invoice.tax|company_id|Company|Many2one|res.company
account.invoice.tax|currency_id||Many2one|res.currency
account.invoice.tax|base|Base|Monetary|


model|field|String|type|note
-----|-----|------|----|----
account.payment.term|name|Payment Terms|Char| translate=True, required=True
account.payment.term|active||Boolean|default=True
account.payment.term|note|Description on the Invoice|Text|translate=True
account.payment.term|line_ids|Terms|One2many|'account.payment.term.line', 'payment_id'
account.payment.term|company_id|Company|Many2one|res.company
account.payment.term|sequence||Integer|required=True, default=10


model|field|String|type|note
-----|-----|------|----|----
account.payment.term.line|value|Type|Selection|
account.payment.term.line|value_amount|Value|Float|
account.payment.term.line|days|Number of Days|Integer| required=True, default=0
account.payment.term.line|day_of_the_month|Day of the month|Integer|
account.payment.term.line|option||Selection|required=True, string='Options'
account.payment.term.line|payment_id|Payment Terms|Many2one|account.payment.term
account.payment.term.line|sequence||Integer|



