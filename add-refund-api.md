<h1>Add Refund API - Implementation Guide</h1><br>
<p>The “Add Refund” API should be triggered every time a transaction must be marked as refunded in the system.</p>
<p>Note: If you are using ClickCRM checkout and process refunds from the Admin, there is no need to call this API. It’s designed to be used in cases where charges are processed outside of the clickCRM system.</p>
<p><strong>HTTP Request Method:</strong> <code>GET</code><br>
<strong>URL</strong>: <code>https://secure.clickcrm.com/v2/addrefund</code><br></p>
<p><strong>Parameters</strong><br>
Required items appear in bold type.</p>
<table>
<thead>
<tr>
<th align="left">Name</th>
<th align="left">Type</th>
<th align="left">Description</th>
</tr>
</thead>
<tbody>
<tr>
<td align="left"><strong>a<strong></td>
<td align="left">Numeric</td>
<td align="left">Your clickCRM account ID</td>
</tr>
<tr>
<td align="left"><strong>api_key</strong></td>
<td align="left">String</td>
<td align="left">API key provided with your account credentials</td>
</tr>
<tr>
<td align="left"><strong>codename</strong></td>
<td align="left">String</td>
<td align="left">Codename of the refunded product</td>
</tr>
<tr>
<td align="left"><strong>customer_emailaddress</strong></td>
<td align="left">String</td>
<td align="left">Email address of the customer refunded</td>
</tr>
<tr>
<td align="left"><strong>amount</strong></td>
<td align="left">Numeric</td>
<td align="left">Transaction amount to be refunded. Should match the charge amount</td>
</tr>
<tr>
<td align="left">transaction_id</td>
<td align="left">String</td>
<td align="left">Unique external transaction identifier, if used when charge was added</td>
</tr>
<tr>
<td align="left">flag_void_commissions</td>
<td align="left">Numeric</td>
<td align="left">Flag controlling if we Void the affiliate commission attached to the charge or not</td>
</tr>
</tbody>
</table>
