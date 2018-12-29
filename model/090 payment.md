TBD 2018-12-22

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



model|field|String|type|note
-----|-----|------|----|----
payment.icon||||


model|field|String|type|note
-----|-----|------|----|----
payment.transaction||||


model|field|String|type|note
-----|-----|------|----|----
payment.token||||



