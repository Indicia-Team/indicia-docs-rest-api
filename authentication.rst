Authentication
==============

Several authentication mechanisms have been reviewed to see if they meet the needs of this
API. In particular, the mechanism must be:
 
  * Secure
  * RESTful (and therefore stateless)
  * Easily understood and implemented.

Login/session based approaches are not stateless and therefore not truly RESTful, so 
authentication data must be presented with every request. 

In order to achieve the requirements a protocol based the standard method of using an
HMAC (keyed-hash message authentication code) has been implemented:
  #. The requesting entity creates a HMAC-SHA1 value of the complete request url 
     (including parameters). The hash value uses the user password as the shared secret.
  #. The requesting entity adds an Authorization header to the request containing the
     following string USER:[user_id]:HMAC:[hmac] where:

       * [user_id] is the requesting user’s agreed system identifier
       * [hmac] is the HMAC-SHA1 value computed in (1)
       
  #. The receiving entity recomputes the HMAC-SHA1 in the same manner as (1) and any 
     authorisation failure is returned as HTTP 401 Unauthorized.

This authentication should provide suitable protection against tampering and sufficient 
level of authentication providing the shared secret is sufficiently long. 

The following example PHP snippet illustrates the code required for authentication against
the REST API:

  .. code-block:: php
  
    <?php
    $shared_secret = 'mypassword';
    $userId = 'ME';
    $url = 'http://www.example.com/rest/projects';
    $session = curl_init();
    // Set the POST options.
    curl_setopt ($session, CURLOPT_URL, $url);
    curl_setopt($session, CURLOPT_HEADER, false);
    curl_setopt($session, CURLOPT_RETURNTRANSFER, true);
    // Create the authentication HMAC
    $hmac = hash_hmac("sha1", $url, $shared_secret, $raw_output=FALSE);
    curl_setopt($session, 
        CURLOPT_HTTPHEADER, 
        array("Authorization: USER:$userId:HMAC:$hmac")
    );
    // Do the request
    $response = curl_exec($session);
    $httpCode = curl_getinfo($session, CURLINFO_HTTP_CODE); 
    $curlErrno = curl_errno($session);
    // Check for an error, or check if the http response was not OK.
    if ($curlErrno || $httpCode != 200) {
      echo "Error occurred accessing $url<br/>";
      echo "Rest API Sync error $httpCode<br/>";
      if ($curlErrno) {
        echo 'Error number: '.$curlErrno;
        echo 'Error message: '.curl_error($session);
      }
      throw new exception('Request to server failed');
    }
    $data = json_decode($response, true);
    ?>
