<h1>Checkout API - Implementation Guide</h1><br>
<p><strong>1. Include the following Javascript code on your checkout page:</strong><br></p>

<code><script type="text/javascript">var ClickCRM_DoCheckout=function(){var s,o,a="",i="",n={result:0,result_str:"Oops! Something went wrong. Please try again"};function r(e){var t=n;try{t=JSON.parse(this.responseText)}catch(e){}o(t)}function c(e){o(n)}function u(e){o(n)}function l(e){var t,n;0<e.status||(t=e,(n=new XMLHttpRequest).submittedData=t,n.addEventListener("load",r),n.addEventListener("error",c),n.addEventListener("abort",u),n.open("post",t.receiver,!0),n.setRequestHeader("Content-Type",t.contentType),n.send(t.segments.join("&")))}function t(e){var t,n,s;this.contentType="application/x-www-form-urlencoded",this.receiver="https://secure.clickcrm.com/v2/docheckout",this.status=0,this.segments=["a="+i,"t="+a];for(var o=escape,r=0;r<e.elements.length;r++)if((s=e.elements[r]).hasAttribute("name"))if("FILE"===(n="INPUT"===s.nodeName.toUpperCase()?s.getAttribute("type").toUpperCase():"TEXT")&&0<s.files.length)for(t=0;t<s.files.length;this.segments.push(o(s.name)+"="+o(s.files[t++].name)));else("RADIO"!==n&&"CHECKBOX"!==n||s.checked)&&this.segments.push(o(s.name)+"="+o(s.value));a="",l(this)}function p(n){var s=new XMLHttpRequest;s.addEventListener("load",function(e){var t;try{s.readyState===s.DONE&&200===s.status&&(t=JSON.parse(s.responseText),a=t.token,i=t.a,"function"==typeof n&&n())}catch(e){}}),s.open("GET","checkout-init.php"),s.send()}function h(e){console.log("FORM: "+s),console.log("CHECKOUT: "+a),new t(s)}return p(),function(e,t){var n;s=document.getElementById(e),o=t,n=h,""!==a?(console.log("USING EXISTING TOKEN"),n()):(console.log("GETTING NEW TOKEN"),p(n))}}();</script>
</code>

<p><strong>2. Create a new PHP script <i>checkout-init.php</i> under the same folder as your checkout page and paste the code below.</strong><br></p>
<p>You will need to replace the <b>ACCOUNT_ID</b> and <b>API_KEY</b> with the ones belonging to your ClickCRM account. You can view and manage your API secret in your ClickCRM account under Profile->API Credentials</strong>.
<br></p>
<table>
<thead>
<tr>
<th align="left"><g-emoji class="g-emoji" alias="warning" fallback-src="https://assets-cdn.github.com/images/icons/emoji/unicode/26a0.png">⚠️</g-emoji> Never share your API token, API secret, or Basic Auth credentials with <em>anyone</em> — not even ClickCRM Support.</th>
</tr>
</thead>
</table>
<p><b>checkout-init.php</b></p>
<pre>
<code>
define('ACCOUNT_ID', 5396);
define('API_KEY', 'ad64dasd112353813e180e72d10635295e7c151');
header("Content-Type: application/json; charset=utf-8");
function GetCheckoutToken()
{
    $checkoutToken  = '';
    do
    {
        if (empty($_COOKIE['sessid2']))
        {
            break;
        }
        // Build the data array to be submitted
        $data = array(
            'a' => ACCOUNT_ID,
            'api_key' => API_KEY,
            'sess_id' => $_COOKIE['sessid2'],
            'order_total' => 100
        );
        // Prepare the cURL request
        $ch = curl_init('https://secure.clickcrm.com/v2/generate_token');
        // Set cURL options for POST request
        curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
        curl_setopt($ch, CURLINFO_HEADER_OUT, true);
        curl_setopt($ch, CURLOPT_POST, true);
        curl_setopt($ch, CURLOPT_POSTFIELDS, $data);
        // Submit the POST request
        $result = curl_exec($ch);
        if ($result === false)
        {
            // Do some general error handling here
            // echo 'Curl error: ' . curl_error($ch);
            break;
        }
        $info = curl_getinfo($ch);
        $decodedData = json_decode($result, true);
        if (empty($decodedData['result']))
        {
            // Authentication error. A description of the error can be found in $decodedData['result_str']
            break;
        }
        $checkoutToken = $decodedData['data']['token'];

        // Close cURL session handle
        curl_close($ch);
    } while (false);
    return $checkoutToken;
}
$response = array('token' => GetCheckoutToken(), 'a' => ACCOUNT_ID);
echo json_encode($response);
</code>
</pre>
<p><strong>3. Add the checkout call code on your form submit button's click event handler or whereever it suits best for you.</strong></p>
<pre>
<code>
ClickCRM_DoCheckout(htmlFormID, callbackFunction);
</code>
</pre>
<p><b>ClickCRM_DoCheckout</b> requires 2 parameters that are described below.</p>
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
<td align="left">htmlFormID</td>
<td align="left">String</td>
<td align="left">The ID of the html checkout form</td>
</tr>
<tr>
<td align="left">callbackFunction</td>
<td align="left">Function</td>
<td align="left">User defined callback function that will be automatically called when the checkout call is completed.</td>
</tr>
</tbody>
</table>
<p>callbackFunction<p>
<p> JSON object containing the information described below.</p>
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
