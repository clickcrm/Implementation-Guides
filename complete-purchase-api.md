<h1>Complete Purchase API - Implementation Guide</h1><br>
<p>The “Complete Purchase” API should be triggered to Create an Order containing the items under a ClickCRM account's shopping cart.</p>
<p><strong>HTTP Request Method:</strong> <code>GET</code> or <code>POST</code><br>
<strong>URL</strong>: <code>https://secure.clickcrm.com/v2/completepurchase</code><br></p>
<p><strong>Parameters</strong><br>
All the parameters are required.</p>
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
<td align="left">Unique API key (available under your ClickCRM account – setup page)</td>
</tr>
<tr>
<td align="left"><strong>user_id</strong></td>
<td align="left">Number</td>
<td align="left">Customer ID (provided by the Add Customer API)</td>
</tr>
</tbody>
</table>
<br>
<p><strong>Example</strong></p>
<p><code>https://secure.clickcrm.com/v2/completepurchase?a=1234&api_key=asndjaf3TUU6jhbendnheudhen&user_id=12345</code><br>
