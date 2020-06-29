<h1>Add Coupon To Cart API - Implementation Guide</h1><br>
<p>The “Add Coupon To Cart” API should be triggered to Add a Discount Coupon under a ClickCRM account's shopping cart.</p>
<p><strong>HTTP Request Method:</strong> <code>GET</code> or <code>POST</code><br>
<strong>URL</strong>: <code>https://secure.clickcrm.com/v2/addCouponToCart</code><br></p>
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
<td align="left"><strong>user_id</strong></td>
<td align="left">Number</td>
<td align="left">Customer ID (outputted by the Add Customer API)</td>
</tr>
<tr>
<td align="left">s</td>
<td align="left">String</td>
<td align="left">Cart Session ID</td>
</tr>  
<tr>
<td align="left"><strong>coupon_code</strong></td>
<td align="left">String</td>
<td align="left">Discount Coupon Code</td>
</tr>
</tbody>
</table>
<br>
<p><strong>Example</strong></p>
<p><code>https://secure.clickcrm.com/v2/addCouponToCart?a=1234&api_key=asndjaf3TUU6jhbendnheudhen&user_id=12345&coupon_code=7dg35hTG95</code><br>
  
<p>Note: The API should be called after calling the Add To Cart API.
