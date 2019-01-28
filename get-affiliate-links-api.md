<h1>Get Affiliate Links API - Implementation Guide</h1><br>
<p>The “Get Affiliate Links” API should be triggered to get the offer links for a specific affiliate.</p>
<p><strong>HTTP Request Method:</strong> <code>GET</code> or <code>POST</code><br>
<strong>URL</strong>: <code>https://secure.clickcrm.com/v2/get_affiliate_links</code><br></p>
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
<td align="left"><strong>emailaddress</strong></td>
<td align="left">String</td>
<td align="left">Affiliate email address</td>
</tr>
</tbody>
</table>
<br>
<p><strong>Example</strong></p>
<p><code>http://secure.clickcrm.com/v2/get_affiliate_links?a=5336&api_key=d1beb3c4970324d9acfbb0140093828f&emailaddress=manager@convertcoldmedia.com</code><br>

<p>The JSON response looks like this:</p>
<pre><code>
{  
   "result":1,
   "result_str":"Successfully retrieved affiliate offer links",
   "data":{  
      "offers":[  
         {  
            "name":"Offer 1",
            "link":"Link 1"
         },
         {  
            "name":"Offer 2",
            "link":"Link 2"
         }
      ],
      "message":"Successfully retrieved affiliate offer links"
   }
}
</code></pre>
<br>
<p>Note: In order to get a functional URL, the link in the API response must be decoded (urldecode).</p>
