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
<td align="left"><b>product_codename<b></td>
<td align="left">ClickCRM product's codename</td>
</tr>
<tr>
<td align="left"><b>emailaddress</b></td>
<td align="left">Customer's email address</td>
</tr>
<tr>
<td align="left">document_number</td>
<td align="left">Customer's identity card number</td>
</tr>
<tr>
<td align="left">phone</td>
<td align="left">Customer's phone number</td>
</tr>
<tr>
<td align="left"><b>creditcards_country</b></td>
<td align="left">Billing address: country</td>
</tr>
<tr>
<td align="left"><b>creditcards_state</b></td>
<td align="left">Billing address: state</td>
</tr>
<tr>
<td align="left">creditcards_city</td>
<td align="left">Billing address: city</td>
</tr>
<tr>
<td align="left"><b>creditcards_zip</b></td>
<td align="left">Billing address: zip code</td>
</tr>
<tr>
<td align="left">creditcards_address</td>
<td align="left">Billing address: street and no.</td>
</tr>
<tr>
<td align="left"><b>creditcards_name<b></td>
<td align="left">Card holder's name</td>
</tr>
<tr>
<td align="left"><b>creditcards_cardnumber</b></td>
<td align="left">Debit/credit card number</td>
</tr>
<tr>
<td align="left"><b>creditcards_month</b></td>
<td align="left">Card expiration month</td>
</tr>
<tr>
<td align="left"><b>creditcards_year</b></td>
<td align="left">Card expiration year</td>
</tr>
<tr>
<td align="left"><b>creditcards_ccv</b></td>
<td align="left">Card CVV</td>
</tr>
<tr>
<td align="left"><b>addresses_address</b></td>
<td align="left">Shipping address(only for physical products)</td>
</tr>
<tr>
<td align="left"><b>addresses_country</b></td>
<td align="left">Shipping address: country(only for physical products)</td>
</tr>
<tr>
<td align="left"><b>addresses_state</b></td>
<td align="left">Shipping address: state(only for physical products)</td>
</tr>
<tr>
<td align="left"><b>addresses_city</b></td>
<td align="left">Shipping address: city(only for physical products)</td>
</tr>
<tr>
<td align="left"><b>addresses_zip</b></td>
<td align="left">Shipping address: zip code(only for physical products)</td>
</tr>
</tbody>
</table>
<h2>2. Include the ClickCRM API Wrapper</h2>
<p>Include the following Javascript code on your checkout page:<br></p>

<code><script type="text/javascript" src="https://cdn.softwareprojects.com/classes/ClickCRM_API_Wrapper/v1/clickcrm-api-wrapper.min.js"></script>
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
define('API_KEY', 'THISISYOURSECRETAPIKEY');
define('SESS_ID', $_COOKIE['sessid2']);

header("Content-Type: application/json; charset=utf-8");

function GetCheckoutToken()
{
    $checkoutToken  = '';
    
    do
    {
        if (empty(SESS_ID))
        {
            break;
        }

        // Build the data array to be submitted
        $data = array(
            'a' => ACCOUNT_ID,
            'api_key' => API_KEY,
            'sess_id' => SESS_ID,
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

$response = array('token' => GetCheckoutToken(), 'a' => ACCOUNT_ID, 's' => SESS_ID);

echo json_encode($response);
</code>
</pre>
<h2>4. Initialize the ClickCRM API Wrapper on document ready</h2>
<p>Add the checkout call code on your form submit button's click event handler or whereever it suits best for you.</p>
<pre>
<code>
<script type="text/javascript">

// using jQuery as a helper for this example
//
$(document).ready(function()
{
	// Initialize ClickCRM API Wrapper
	//
	var _clickCRM = new ClickCRM_API_Wrapper(
	{
		// The id of the html checkout form
		//
		formID: 'checkout-form',
		
		// A callback function that can be used for displaying the taxes to the user
		//
		// ClickCRM performs an automatic tax calculation based on the country, state and zip code inputed by the user
		//
		salesTaxesChangedCallback: function(response) 
		{
			$('#taxes-to-the-user').text(response.result);
		}
	});	

	// Handle form submit
	//
	$('#checkout-form').on('submit', function()
	{
		// You can do some custom JS processing here

		// Do the checkout call
		//
		_clickCRM.checkout(function(response)
		{
			// response.result will be 0 if the checkout call didn't complete due to a validation error
			//
			if (response.result == 0)
			{
				alert('Oops! The checkout call returned the following error: ' + response.result_str);
			}
		});
	});
});

</script>
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
