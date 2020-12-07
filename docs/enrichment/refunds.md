# Refunds of transactions

Refunded transactions are a significant part of online fundraising and payment processing. Despite this, there is no common standard for when and how to report refunds of transactions. Most conversion tracking systems (Google, Facebook) do have minimal support for conversion adjustments, but we at Frakture have not seen extensive use of them. As such, most revenue and ROI calculations in the wild do _not_ include refund amounts.

At Frakture we lie at the intersection of common marketing practice and good revenue reporting. To try to accommodate both practices, we provide both revenue and refund data, and allow you to determine which refund practice you want to use.

For every transaction, Frakture will attempt to record a refund_amount if that transaction has been refunded. *In your warehouse, the "revenue" and "amount" numbers reflect all transactions, without refunds.* To obtain the transaction sum less refunds, just subtract refund_amount to get the final net value.

> **_EXAMPLE:_** select (SUM(amount) - SUM(refund_amount)) AS amount_less_refunds from <your transaction table>

In Frakture standard reports, we use the non-refunded totals unless specifically labeled otherwise (e.g., our Refund report).
