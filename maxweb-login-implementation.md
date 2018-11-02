<h1>MaxWeb Login Implementation Guide</h1>
<p>Call the RESTful API POST endpoint /initiate with a JSON object containing the properties described below to generate a login link for each affiliate. You will receive a JSON object in the response containing a timestamp, and a login URL which you can present to the affiliates.</p>
<p><strong>HTTP Request Method:</strong> <code>POST</code><br>
<strong>REST URL</strong>: <code>https://backoffice.maxweb.com/clickcrm-login/initiate</code><br>
<h2>Authentication and encryption</h2>
<p>This API calls are protected using <a href="https://tools.ietf.org/html/rfc7617" rel="nofollow">HTTP Basic Authentication</a>. Your Basic Auth credentials are constructed using your account ID as the user-id and your API secret as the password. You can view and manage your API secret in your ClickCRM account under Profile->API Credentials</strong>.
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
<h2>Implementation Example in PHP</h2>
<pre>
<code>
function GetLoginLink($emailaddress)
{
    $loginLink  = '';
    $accoundID  = 5396;
    $privateKey = 'ad64dasd112353813e180e72d10635295e7c151';

    // Generate the authorization token
    $authorizationToken = base64_encode($accoundID.':'.$privateKey);

    // Build the data array to be submitted (in this case it's the affiliate's email address)
    $data = array(
        'emailaddress' => $emailaddress
    );

    // JSON encode the data
    $payload = json_encode($data);
     
    // Prepare the cURL request
    $ch = curl_init('https://backoffice.maxweb.com/clickcrm-login/initiate');

    // Set cURL options for POST request
    curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
    curl_setopt($ch, CURLINFO_HEADER_OUT, true);
    curl_setopt($ch, CURLOPT_POST, true);
    curl_setopt($ch, CURLOPT_POSTFIELDS, $payload);
     
    // Set HTTP Header for JSON request 
    curl_setopt($ch, CURLOPT_HTTPHEADER, array(
        'Accept: application/json',
        'Content-Type: application/json',
        'Content-Length: ' . strlen($payload),
        'Authorization: Basic '.$authorizationToken)
    );

    // Submit the POST request
    $result = curl_exec($ch);

    do
    {
        if ($result === false)
        {
            // Do some general error handling here
            // echo 'Curl error: ' . curl_error($ch);
            break;
        }

        $info = curl_getinfo($ch);

        if ($info['http_code'] != 200)
        {
            // Authentication error
            break;
        }

        $decodedData = json_decode($result, true);

        if (empty($decodedData['result']))
        {
            // Affiliate validation error. A description of the error can be found in $decodedData['result_str']
            break;
        }

        $loginLink = $decodedData['redirect_url'];

    } while (false);

    // Close cURL session handle
    curl_close($ch);

    return $loginLink;
}

$loginLink = GetLoginLink('affiliateaccount@domainname.com');

// Display the link to the user
echo '<a href="'.$loginLink.'">Login</a>';
</code>
</pre>
