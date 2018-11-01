<h1>MaxWeb Login Implementation Guide</h1>
<p>Call the RESTful API POST endpoint /initiate with a JSON object containing the properties described below to generate a login link for each affiliate. You will receive a JSON object in the response containing a timestamp, and a login URL which you can present to the affiliates.</p>
<h2>Authentication and encryption</h2>
<p>This API calls are protected using <a href="https://tools.ietf.org/html/rfc7617" rel="nofollow">HTTP Basic Authentication</a>. Your Basic Auth credentials are constructed using your account ID as the user-id and your API secret as the password. You can view and manage your API secret in your ClickCRM account</strong>.
<br></p>
<table>
<thead>
<tr>
<th align="left"><g-emoji class="g-emoji" alias="warning" fallback-src="https://assets-cdn.github.com/images/icons/emoji/unicode/26a0.png">⚠️</g-emoji> Never share your API token, API secret, or Basic Auth credentials with <em>anyone</em> — not even ClickCRM Support.</th>
</tr>
</thead>
</table>
<p>The <a href="https://tools.ietf.org/html/rfc5246" rel="nofollow">TLS Protocol</a> is required to securely transmit your data, and we strongly recommend using the latest version.</p>
<h2>Request headers</h2>
<p>The following fields are required in the header section of your request:<br></p>
<p><code>Accept: application/json</code><br>
<code>Content-Type: application/json</code><br>
<code>Content-Length:</code>  (see <a href="https://tools.ietf.org/html/rfc7230#section-3.3.2" rel="nofollow">RFC-7230</a>)<br>
<code>Authorization:</code> (see <a href="https://tools.ietf.org/html/rfc7617" rel="nofollow">RFC 7617</a>)<br>
</p>
<h2>Request body</h2>
<p>The body of your <strong>initiate</strong> API request needs you to specify the email address of the affiliate account that you want to generate a login link for</p>
<h2>Response</h2>
<p>Unsuccessful requests will return the relevant <a href="https://tools.ietf.org/html/rfc7231#section-6" rel="nofollow">HTTP status code</a> and information about the cause of the error.</p>
<p>Successful requests will return HTTP status code <code>200 OK</code> along with a JSON object containing the information described below.</p>
<p><strong>Required items appear in bold type.</strong></p>
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
<td align="left"><strong>timestamp</strong></td>
<td align="left">Number</td>
<td align="left">Timestamp (UTC) in Unix format</td>
</tr>
<tr>
<td align="left"><strong>result</strong></td>
<td align="left">Number</td>
<td align="left">1</td>
  <td align="left"><strong>1</strong> on success. <strong>0</strong> on failure</td>
</tr>
<tr>
<td align="left"><strong>redirect_url</strong></td>
<td align="left">String</td>
<td align="left">Affiliate login URL</td>
</tr>
  <tr>
<td align="left">result_str</td>
<td align="left">String</td>
<td align="left">Contains an error message on failure due to validation errors</td>
</tr>
</tbody>
</table>
