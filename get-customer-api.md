<h1>Get Customer API - Implementation Guide</h1><br>
<p>The “Get Customer” API should be triggered to get the customer details.</p>
<p><strong>HTTP Request Method:</strong> <code>GET</code> or <code>POST</code><br>
<strong>URL</strong>: <code>https://secure.clickcrm.com/v2/do_getcustomer</code><br></p>
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
<td align="left">user_id</td>
<td align="left">Numeric</td>
<td align="left">Customer user ID</td>
</tr>
<tr>
<td align="left">emailaddress</td>
<td align="left">String</td>
<td align="left">Affiliate email address</td>
</tr>
<tr>
<td align="left">sess_id</td>
<td align="left">String</td>
<td align="left">Unique session identifier</td>
</tr>
</tbody>
</table>
<p><strong>Note:</strong> At least one of the following params is required: user_id, emailaddress, sess_id</p>
<br>
<p><strong>Example</strong></p>
<p><code>https://secure.clickcrm.com/v2/do_getcustomer.php?a=5407&api_key=ec7e26d19d0e2173ab649c1c47d55305&emailaddress=tshesafer22@gmail.com</code></p>

<p><code>https://secure.clickcrm.com/v2/do_getcustomer.php?a=5407&api_key=ec7e26d19d0e2173ab649c1c47d55305&user_id=12345</code></p>

<p><code>https://secure.clickcrm.com/v2/do_getcustomer.php?a=5407&api_key=ec7e26d19d0e2173ab649c1c47d55305&sess_id=896gjgjhg333</code></p><br>

<p>The JSON response looks like this:</p>
<pre><code>
{ 
   "result":1,
   "result_str":"Successfully retrieved the customer details",
   "data":{ 
      "customer":{ 
         "user_id":"213263",
         "rr_createdate":"2019-11-13 10:54:23",
         "name":"Andy Shaffer",
         "emailaddress":"tshesafer22@gmail.com",
         "phone":"8183223183",
         "city":"Wernersville",
         "address":"78 S Reber St  Apt 19",
         "state":"Pennsylvania",
         "zip":"19565",
         "country":"United States",
         "referrer_name":"Thomas Johnson",
         "referrer_url":"supplements.com\/sales\/turmeric\/thanksgiving-2019",
         "ipaddress":"185.217.69.237",
         "subid":"",
         "subid2":"",
         "subid3":"",
         "subid4":"",
         "subid5":"1066"
      }
   }
}
</code></pre>
