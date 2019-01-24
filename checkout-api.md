<h1>Checkout API - Implementation Guide</h1><br>
<h2>1. Create the checkout form</h2>
<p>Build your custom html checkout form on your page and make sure to define the below listed elements.</p>
    <p><strong>Required items appear in bold type.</strong></p>
<table>
<thead>
<tr>
<th align="left">Name</th>
<th align="left">Description</th>
</tr>
</thead>
<tbody>
<tr>
<td align="left">htmlFormID</td>
<td align="left">The ID of the html checkout form</td>
</tr>
</tbody>
</table>
<h2>2. Include ClickCRM Javascript snippet</h2>
<p>Include the following Javascript code on your checkout page:<br></p>

<code><script type="text/javascript">var ClickCRM_DoCheckout=function(){var s,r,i="",a="",t=0,n={result:0,result_str:"Oops! Something went wrong. Please try again"};function o(e){var t=Object.assign({},n);e&&(c("Error handling..."),c(e),t.error_details=e),r&&r(t)}function c(e){1===t&&console.log(e)}function u(e){var t;try{t=JSON.parse(this.responseText),r(t)}catch(e){o(e)}}function p(e){o(e)}function d(e){o(e)}function h(e){0<e.status||function(e){var t;try{(t=new XMLHttpRequest).submittedData=e,t.addEventListener("load",u),t.addEventListener("error",p),t.addEventListener("abort",d),t.open("post",e.receiver,!0),t.setRequestHeader("Content-Type",e.contentType),t.send(e.segments.join("&"))}catch(e){o(e)}}(e)}function f(e){var t,n,s;this.contentType="application/x-www-form-urlencoded",this.receiver="https://secure.clickcrm.com/v2/docheckout",this.status=0,this.segments=["a="+a,"t="+i];for(var r=escape,o=0;o<e.elements.length;o++)if((s=e.elements[o]).hasAttribute("name"))if("FILE"===(n="INPUT"===s.nodeName.toUpperCase()?s.getAttribute("type").toUpperCase():"TEXT")&&0<s.files.length)for(t=0;t<s.files.length;this.segments.push(r(s.name)+"="+r(s.files[t++].name)));else("RADIO"!==n&&"CHECKBOX"!==n||s.checked)&&this.segments.push(r(s.name)+"="+r(s.value));i="",h(this)}function l(n){var e;try{(e=new XMLHttpRequest).addEventListener("load",function(e){var t;try{t=JSON.parse(this.responseText),i=t.token,a=t.a,"function"==typeof n&&n()}catch(e){"function"==typeof n&&o(e)}}),e.addEventListener("error",p),e.addEventListener("abort",d),e.open("GET","checkout-init.php"),e.send()}catch(e){o(e)}}function v(e){c("FORM: "+s),c("CHECKOUT: "+i),new f(s)}return l(),function(e,t){var n;s=document.getElementById(e),r=t,n=v,""!==i?(c("USING EXISTING TOKEN"),n()):(c("GETTING NEW TOKEN"),l(n))}}();</script>
</code>
<h2>3. Add ClickCRM dependency script</h2>
<p>Create a new PHP script <i>checkout-init.php</i> under the same folder as your checkout page and paste the code below.</strong></p>
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
<h2>4. Do the checkout call</h2>
<p>Add the checkout call code on your form submit button's click event handler or whereever it suits best for you.</p>
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
<p>The <b>callbackFunction</b> receives a Javascript object parameter containing the information described below.<p>
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
<td align="left">result</td>
<td align="left">Number</td>
<td align="left"><strong>1</strong> on success. <strong>0</strong> on failure</td>
</tr>
<tr>
<td align="left">result_str</td>
<td align="left">String</td>
<td align="left">Contains an error message on failure due to validation errors</td>
</tr>
<tr>
<td align="left">error_details</td>
<td align="left">Object</td>
<td align="left">Technical details on the error</td>
</tr>
</tbody>
</table>
<p>Example of using an anonymous callback function for displaying in the console the checkout call result</p>
<pre>
<code>
ClickCRM_DoCheckout('orderform', function(response) { console.log(response); });
</code>
</pre>
