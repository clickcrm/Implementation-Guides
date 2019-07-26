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
<td align="left">Customer Email Address</td>
</tr>
<tr>
<td align="left">address</td>
<td align="left">String</td>
<td align="left">Billing Address</td>
</tr>
<tr>
<td align="left">city</td>
<td align="left">String</td>
<td align="left">Billing City</td>
</tr>
<tr>
<td align="left">state</td>
<td align="left">String</td>
<td align="left">Billing State</td>
</tr>
<tr>
<td align="left">zip</td>
<td align="left">String</td>
<td align="left">Billing Zip</td>
</tr>
<tr>
<td align="left">country</td>
<td align="left">String</td>
<td align="left">Billing Country</td>
</tr>
<tr>
<td align="left">phone</td>
<td align="left">String</td>
<td align="left">Billing Phone</td>
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
<td align="left">Numeric</td>
<td align="left">Referring Affiliate ID</td>
</tr>
<tr>
<td align="left">subid</td>
<td align="left">String</td>
<td align="left">Customer Additional Identifier</td>
</tr>
<tr>
<td align="left">flag_validate_card</td>
<td align="left">Numeric</td>
<td align="left">Set the flag to 1 in order to store the credit card details</td>
</tr>
<tr>
<td align="left">card_number</td>
<td align="left">String</td>
<td align="left">Card Number</td>
</tr>  
<tr>
<td align="left">card_month</td>
<td align="left">String</td>
<td align="left">Card Expiration Month</td>
</tr>
<tr>
<td align="left">card_year</td>
<td align="left">String</td>
<td align="left">Card Expiration Year</td>
</tr>
<tr>
<td align="left">card_ccv</td>
<td align="left">String</td>
<td align="left">Card CCV</td>
</tr>
<tr>
<td align="left">shp_name</td>
<td align="left">String</td>
<td align="left">Shipping Name (if not provided we will store the Customer Full Name value)</td>
</tr>
<tr>
<td align="left">shp_address</td>
<td align="left">String</td>
<td align="left">Shipping Address (only for physical products)</td>
</tr>
<tr>
<td align="left">shp_city</td>
<td align="left">String</td>
<td align="left">Shipping City (only for physical products)</td>
</tr>  
<tr>
<td align="left">shp_state</td>
<td align="left">String</td>
<td align="left">Shipping State (only for physical products)</td>
</tr>
<tr>
<td align="left">shp_zip</td>
<td align="left">String</td>
<td align="left">Shipping Zip (only for physical products)</td>
</tr>
<tr>
<td align="left">shp_country</td>
<td align="left">String</td>
<td align="left">Shipping Country (only for physical products)</td>
</tr>  
</tbody>
</table>
<br>
<p><strong>Example</strong></p>
<p><code>https://secure.clickcrm.com/v2/addcustomer?a=1234&api_key=asndjaf3TUU6jhbendnheudhen&name=John+Doe&emailaddress=john_doe%40mydomain.com&address=2230%20EDawson%20Cove&city=Clovis&zip=936114&state=California&country=United%20States&ipaddress=11.22.33.44&phone=44556633&aff_id=123&flag_validate_card=1&card_number=1234567891011121&card_month=03&card_year=2022&card_cvv=777</code> + the Shipping details<br>
  
<p>Note: If the Shipping details are not provided, the Billing details will be used for Shipping.</p>

<p><b>The API outputs</b> a Result string (Success or Error) and <b>the new added Customer ID</b> (on Success). If the customer record already exists in the ClickCRM system, the existing customer's ID will be outputted. You will have to provide the Customer ID when calling the AddToCart and CompletePurchase APIs.
