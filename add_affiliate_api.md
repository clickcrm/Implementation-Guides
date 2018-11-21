<h1>Add Affiliate API</h1>
<p>The “Add Affiliate” API should be triggered to create a new affiliate record in the ClickCRM system.</p>
<p>Note: If you’re using ClickCRM default affiliate signup page – there is no need to call this API. Its designed to be used in cases where the affiliate is created outside of the ClickCRM system</p>
<p><strong>HTTP Request Method:</strong> <code>GET</code> or <code>POST</code><br>
<strong>URL</strong>: <code>https://secure.clickcrm.com/v2/addaffiliate</code><br></p>
<p><strong>Parameters</strong><br>
<strong>Required items appear in bold type.</strong></p>
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
<td align="left">Affiliate Full Name</td>
</tr>
<tr>
<td align="left"><strong>emailaddress</strong></td>
<td align="left">String</td>
<td align="left">Affiliate Email address</td>
</tr>
<tr>
<td align="left"><strong>username</strong></td>
<td align="left">String</td>
<td align="left">Affiliate unique username or ID in your system (this ID should never change)</td>
</tr>
<tr>
<td align="left">address</td>
<td align="left">String</td>
<td align="left">Affiliate address</td>
</tr>
<tr>
<td align="left">city</td>
<td align="left">String</td>
<td align="left">Affiliate City</td>
</tr>
<tr>
<td align="left">state</td>
<td align="left">String</td>
<td align="left">Affiliate State</td>
</tr>
<tr>
<td align="left">state</td>
<td align="left">String</td>
<td align="left">Affiliate State</td>
</tr>
<tr>
<td align="left">zip</td>
<td align="left">String</td>
<td align="left">Affiliate Zip</td>
</tr>
<tr>
<td align="left">country</td>
<td align="left">String</td>
<td align="left">Affiliate Country</td>
</tr>
</tbody>
</table>
<br>
<p><strong>Example</strong></p>
<p><code>https://secure.clickcrm.com/v2/addaffiliate?a=1234&api_key=asndjaf3TUU6jhbendnheudhen&name=John+Doe&emailaddress=john_doe%40mydomain.com</code><br>
