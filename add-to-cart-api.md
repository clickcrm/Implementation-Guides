<h1>Add To Cart API - Implementation Guide</h1><br>
<p>The “Add To Cart”  should be triggered to Add Products under a ClickCRM account's shopping cart.</p>
<p><strong>HTTP Request Method:</strong> <code>GET</code> or <code>POST</code><br>
<strong>URL</strong>: <code>https://secure.clickcrm.com/v2/addtocart</code><br></p>
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
<td align="left">Unique API key (available under your ClickCRM account – setup page)</td>
</tr>
<tr>
<td align="left"><strong>name</strong></td>
<td align="left">String</td>
<td align="left">Customer Full Name</td>
</tr>
<tr>
<td align="left"><strong>user_id</strong></td>
<td align="left">Number</td>
<td align="left">Customer ID (outputted by the Add Customer API)</td>
</tr>
<td align="left"><strong>product_codename</strong></td>
<td align="left">String</td>
<td align="left">Product Codename</td>
</tr>
<td align="left">quantity</td>
<td align="left">Number</td>
<td align="left">Product Quantity (if not provided the default value is 1)</td>
</tr>
<tr>
</tbody>
</table>
<br>
<p><strong>Example</strong></p>
<p><code>https://secure.clickcrm.com/v2/addtocart?a=1234&api_key=asndjaf3TUU6jhbendnheudhen&user_id=12345&product_codename=thyroid-3-onetime-CT&quantity=2</code><br>
