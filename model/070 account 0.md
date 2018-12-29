TBD 2018-12-22

model|field|String|type|note
-----|-----|------|----|----
res.company|fiscalyear_last_day||Integer|
res.company|fiscalyear_last_month||Selection|
res.company|period_lock_date|Lock Date for Non-Advisers|Date|
res.company|fiscalyear_lock_date|Lock Date|Date|
res.company|transfer_account_id|Inter-Banks Transfer Account|Many2one|account.account
res.company|expects_chart_of_accounts|Expects a Chart of Accounts|Boolean|
res.company|chart_template_id||Many2one|account.chart.template
res.company|bank_account_code_prefix|Prefix of the bank accounts|Char|
res.company|cash_account_code_prefix|Prefix of the cash accounts|Char|
res.company|transfer_account_code_prefix|Prefix of the transfer accounts|Char|
res.company|account_sale_tax_id|Default Sale Tax|Many2one|account.tax
res.company|account_purchase_tax_id|Default Purchase Tax|Many2one|account.tax
res.company|tax_cash_basis_journal_id|Cash Basis Journal|Many2one|account.journal
res.company|tax_calculation_rounding_method|Tax Calculation Rounding Method|Selection|[('round_per_line', 'Round per Line'),<br/>('round_globally', 'Round Globally'),]       
res.company|currency_exchange_journal_id|Exchange Gain or Loss Journal|Many2one|account.journal
res.company|income_currency_exchange_account_id|Gain Exchange Rate Account|Many2one|account.account
res.company|expense_currency_exchange_account_id|Loss Exchange Rate Account|Many2one|
res.company|anglo_saxon_accounting|Use anglo-saxon accounting|Boolean|
res.company|property_stock_account_input_categ_id|Input Account for Stock Valuation|Many2one|account.account
res.company|property_stock_account_output_categ_id|Output Account for Stock Valuation|Many2one|account.account
res.company|property_stock_valuation_account_id|Account Template for Stock Valuation|Many2one|account.account
res.company|bank_journal_ids|Bank Journals|One2many|'account.journal', 'company_id'
res.company|overdue_msg|Overdue Payments Messag|Text|
res.company|tax_exigibility|Use Cash Basis|Boolean|
res.company|account_bank_reconciliation_start|Bank Reconciliation Threshold|Date|
res.company|incoterm_id|Default incoterm|Many2one|account.incoterms
res.company|invoice_reference_type|Default Communication Type|Selection|
res.company|qr_code|Display SEPA QR code|Boolean|
res.company|invoice_is_email||Boolean|Email by default
res.company|invoice_is_print||Boolean|Print by default
res.company|account_opening_move_id|Opening Journal Entry|Many2one|
res.company|account_opening_journal_id|Opening Journal|Many2one|
res.company|account_opening_date|Opening Date|Date|
res.company|account_setup_bank_data_state|State of the onboarding bank data step|Selection|[('not_done', "Not done"), <br/>('just_done', "Just done"), <br/>('done', "Done")]
res.company|account_setup_fy_data_state|State of the onboarding fiscal year step||[('not_done', "Not done"), <br/>('just_done', "Just done"), <br/>('done', "Done")]
res.company|account_setup_coa_state|State of the onboarding charts of account step|Selection|[('not_done', "Not done"), <br/>('just_done', "Just done"), <br/>('done', "Done")]
res.company|account_onboarding_invoice_layout_state|State of the onboarding invoice layout step|Selection|[('not_done', "Not done"), <br/>('just_done', "Just done"), <br/>('done', "Done")]
res.company|account_onboarding_sample_invoice_state|State of the onboarding sample invoice step|Selection|[('not_done', "Not done"), <br/>('just_done', "Just done"), <br/>('done', "Done")]
res.company|account_onboarding_sale_tax_state|State of the onboarding sale tax step|Selection|[('not_done', "Not done"), <br/>('just_done', "Just done"), <br/>('done', "Done")]
res.company|account_invoice_onboarding_state|State of the account invoice onboarding panel|Selection|[('not_done', "Not done"), <br/>('just_done', "Just done"), <br/>('done', "Done"), <br/> ('closed', "Closed")]
res.company|account_dashboard_onboarding_state|State of the account dashboard onboarding panel|Selection|[('not_done', "Not done"), <br/>('just_done', "Just done"), <br/>('done', "Done"), <br/> ('closed', "Closed")]


model|field|String|type|note
-----|-----|------|----|----
product.category|property_account_income_categ_id|Income Account|Many2one|account.account
product.category|property_account_expense_categ_id|Expense Account|Many2one|account.account

model|field|String|type|note
-----|-----|------|----|----
product.template|taxes_id|Customer Taxes|Many2many|account.tax
product.template|supplier_taxes_id|Vendor Taxes|Many2many|account.tax
product.template|property_account_income_id|Income Account|Many2one|account.account
product.template|property_account_expense_id|Expense Account|Many2one|account.account


model|field|String|type|note
-----|-----|------|----|----
account.fiscal.year|name|Char||Name
account.fiscal.year|date_from|Start Date|Date|
account.fiscal.year|date_to|End Date|Date|
account.fiscal.year|company_id|Company|Many2one|res.company


model|field|String|type|note
-----|-----|------|----|----
account.cash.rounding|name||Char|Name
account.cash.rounding|rounding|Rounding Precision|Float|
account.cash.rounding|strategy|Rounding Strategy|Selection|[('biggest_tax', 'Modify tax amount'), <br/>('add_invoice_line', 'Add a rounding line')]
account.cash.rounding|account_id|Account|Many2one|account.account
account.cash.rounding|rounding_method|Rounding Method|Selection|

model|field|String|type|note
-----|-----|------|----|----
account.fiscal.position|sequence||Integer|
account.fiscal.position|name|Fiscal Position|Char|
account.fiscal.position|active||active|
account.fiscal.position|company_id|Company|Many2one|res.company
account.fiscal.position|account_ids|Account Mapping|One2many|'account.fiscal.position.account', <br/>'position_id'
account.fiscal.position|tax_ids|Tax Mapping|One2many|'account.fiscal.position.tax',<br/> 'position_id'
account.fiscal.position|note||Text|Notes
account.fiscal.position|auto_apply|Detect Automatically|Boolean|
account.fiscal.position|country_id|Country|Many2one|res.country
account.fiscal.position|country_group_id|Country Group|Many2one|res.country.group
account.fiscal.position|state_ids|Federal States|Many2many|res.country.state
account.fiscal.position|zip_from|Zip Range From|Integer|
account.fiscal.position|zip_to|Zip Range To|Integer|
account.fiscal.position|states_count||Integer|


model|field|String|type|note
-----|-----|------|----|----
account.analytic.line|product_id|Product|Many2one|product.product
account.analytic.line|general_account_id|Financial Account|Many2one|account.account
account.analytic.line|move_id|Journal Item|Many2one|account.move.line
account.analytic.line|code||Char|
account.analytic.line|ref|Ref.|Char|


model|field|String|type|note
-----|-----|------|----|----
account.fiscal.position.tax|position_id|Fiscal Position|Many2one|account.fiscal.position
account.fiscal.position.tax|tax_src_id|Tax on Product|Many2one|account.tax
account.fiscal.position.tax|tax_dest_id|Tax to Apply|Many2one|account.tax


model|field|String|type|note
-----|-----|------|----|----
account.fiscal.position.account|position_id|Fiscal Position|Many2one|account.fiscal.position
account.fiscal.position.account|account_src_id|Account on Product|Many2one|account.account
account.fiscal.position.account|account_dest_id|Account to Use Instead|Many2one|account.account


model|field|String|type|note
-----|-----|------|----|----
res.partner|credit|Total Receivable|Monetary|
res.partner|debit|Total Payable|Monetary|
res.partner|debit_limit||Monetary|Payable Limit
res.partner|total_invoiced|Total Invoiced|Monetary|
res.partner|currency_id|Currency|Many2one|res.currency
res.partner|contracts_count|Contracts Count|Integer|
res.partner|journal_item_count|Journal Items|Integer|
res.partner|property_account_payable_id|Account Payable|Many2one|account.account
res.partner|property_account_receivable_id|Account Receivable|Many2one|
res.partner|property_account_position_id|Fiscal Position|Many2one|account.fiscal.position
res.partner|property_payment_term_id|Customer Payment Terms|Many2one|account.payment.term
res.partner|property_supplier_payment_term_id|Vendor Payment Terms|Many2one|account.payment.term
res.partner|ref_company_ids|Companies that refers to partner|One2many|'res.company', 'partner_id'
res.partner|has_unreconciled_entries||Boolean|
res.partner|last_time_entries_checked|Latest Invoices & Payments Matching Date|Datetime|
res.partner|invoice_ids|Invoices|One2many|'account.invoice', 'partner_id'
res.partner|contract_ids|Partner Contracts|One2many|'account.analytic.account', 'partner_id'
res.partner|bank_account_count|Bank|Integer|
res.partner|trust|Degree of trust you have in this debtor|Selection|[('good', 'Good Debtor'),<br/> ('normal', 'Normal Debtor'),<br/> ('bad', 'Bad Debtor')]
res.partner|invoice_warn||Selection|WARNING_MESSAGE
res.partner|invoice_warn_msg||Text|Message for Invoice


