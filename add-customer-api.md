<h1>Add Customer API - Implementation Guide</h1><br>
<p>The “Add Customer” API should be triggered to create a new customer record in the ClickCRM system.</p>
<p><strong>HTTP Request Method:</strong> <code>GET</code> or <code>POST</code><br>
<strong>URL</strong>: <code>https://secure.clickcrm.com/v2/addcustomer</code><br></p>
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
<td align="left"><strong>emailaddress</strong></td>
<td align="left">String</td>
<td align="left">Customer Email address</td>
</tr>
<td align="left">address</td>
<td align="left">String</td>
<td align="left">Customer address</td>
</tr>
<tr>
<td align="left">city</td>
<td align="left">String</td>
<td align="left">Customer City</td>
</tr>
<tr>
<td align="left">state</td>
<td align="left">String</td>
<td align="left">Customer State</td>
</tr>
<tr>
<td align="left">zip</td>
<td align="left">String</td>
<td align="left">Customer Zip</td>
</tr>
<tr>
<td align="left">country</td>
<td align="left">String</td>
<td align="left">Customer Country</td>
</tr>
<tr>
<td align="left">phone</td>
<td align="left">String</td>
<td align="left">Customer Phone</td>
</tr>
<tr>
<td align="left">ipaddress</td>
<td align="left">String</td>
<td align="left">Customer IP Address</td>
</tr> 
<tr>
<td align="left">comments</td>
<td align="left">String</td>
<td align="left">Customer Comments</td>
</tr>
<tr>
<td align="left">aff_id</td>
<td align="left">String</td>
<td align="left">Referring Affiliate ID</td>
</tr>
<tr>
<td align="left">subid</td>
<td align="left">Numeric</td>
<td align="left">Customer Additional Identifier</td>
</tr>   
</tbody>
</table>
<br>
<p><strong>Example</strong></p>
<p><code>https://secure.clickcrm.com/v2/addaffiliate?a=1234&api_key=asndjaf3TUU6jhbendnheudhen&name=John+Doe&emailaddress=john_doe%40mydomain.com</code><br>
