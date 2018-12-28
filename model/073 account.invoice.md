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
account.invoice||||


model|field|String|type|note
-----|-----|------|----|----
account.invoice.line||||

model|field|String|type|note
-----|-----|------|----|----
account.invoice.tax||||



model|field|String|type|note
-----|-----|------|----|----
account.payment.term||||


model|field|String|type|note
-----|-----|------|----|----
account.payment.term.line||||



