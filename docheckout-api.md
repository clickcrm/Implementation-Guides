<h1>Add To Cart API - Implementation Guide</h1><br>
<p>The “Add To Cart” API should be triggered to Add Products under a ClickCRM account's shopping cart.</p>
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
<td align="left"><strong>s</strong></td>
<td align="left">String</td>
<td align="left">Cart Session ID</td>
</tr>
<tr>
<td align="left"><strong>creditcards_name</strong></td>
<td align="left">String</td>
<td align="left">Billing  First Name and Last Name separated by space</td>
</tr>
<tr>
<td align="left"><strong>creditcards_state</strong></td>
<td align="left">String</td>
<td align="left">Billing  State</td>
</tr>  
<tr>
<td align="left"><strong>creditcards_country</strong></td>
<td align="left">String</td>
<td align="left">Billing  Country</td>
</tr>  
<tr>
<td align="left"><strong>creditcards_zip</strong></td>
<td align="left">String</td>
<td align="left">Billing  ZIP</td>
</tr>
<tr>
<td align="left"><strong>creditcards_cardnumber</strong></td>
<td align="left">String</td>
<td align="left">Card Number</td>
</tr>      
<tr>
<td align="left"><strong>creditcards_ccv</strong></td>
<td align="left">String</td>
<td align="left">Card Code</td>
</tr>      
<tr>
<td align="left"><strong>emailaddress</strong></td>
<td align="left">String</td>
<td align="left">Customer Email Address</td>
</tr>
<tr>
<td align="left">addresses_address</td>
<td align="left">String</td>
<td align="left">Shipping address</td>
</tr>  
<tr>
<td align="left">addresses_city</td>
<td align="left">String</td>
<td align="left>Shipping address city</td>
</tr>  
<tr>
<td align="left">addresses_zip</td>
<td align="left">String</td>
<td align="left">Shipping address ZIP Code</td>
</tr>
<tr>
<td align="left">addresses_country</td>
<td align="left">String</td>
<td align="left">Shipping address Country</td>
</tr>                    
</tbody>
</table>
<br>
<p><strong>Example</strong></p>
<p><code>http://secure.clickcrm.com/v2/docheckout?a=2390&api_key=Your_API_KEY&s=sessid2019073108222750853497d0d87d6f823bcd70d7eb4a26146a8fab&creditcards_name=FirstName LastName&creditcards_state=Maramures&emailaddress=test.test+12@softwareprojects.com&creditcards_country=Romania&creditcards_zip=1234&creditcards_cardnumber=4583286917384859&creditcards_ccv=3455&addresses_address=adresa shipping&addresses_city=oras&addresses_zip=zip&addresses_country=Romania&creditcards_address=Enescu 5</code><br>
  
<p>Note: The API should be called after the items have been placed in the cart.</p>
