# Simple HTTP Connector For Flows

Start a flow with a simple HTTP Get request, use HTTP response codes as a flow
condition or execute HTTP requests as a flow action with this app.

### Trigger cards
- Incoming GET requests
 - `http://<YourHomeyIP>/api/app/com.internet/<event>`
 - `http://<YourHomeyIP>/api/app/com.internet/<event>/<value>` will put a value in the 'value'-token of this card.
 - for external access use `https://<YourId>.homey.athom.com/api/app/com.internet/<event>`
- GET variable step 2 (read 'get variable and trigger flow')

### Condition cards
- HTTP Get Response: Checks the HTTP response code of a GET Request.
- HTTP Get JSON Response: Variant with query parameters.

### Action cards
- HTTP Delete
- HTTP Get
- HTTP Get JSON (for query parameters like ?a=1&b=zz use `{"a":1,"b":"zz"}`)
- HTTP Put JSON
- HTTP Post Form (content-type 'application/x-www-form-urlencoded')
- HTTP Post JSON (content-type 'application/json')
- WebSocket Send (message to ws://x.x.x.x:y endpoint)
- GET variable step 1 (read 'get variable and trigger flow')
- DEPRICATED: HTTP Geek Request (Will be removed in next version)

## Get variable and trigger a flow with it
The paired action and trigger cards GET variable step 1/2 enables you to get a value from any JSON-formatted or XML-formatted get response and start a flow with the retrieved value as a token.

The action card has four parameters:
 1. Url (could also be a [node http options](https://nodejs.org/api/http.html#http_http_request_options_callback) object)
 2. JSON encoded query parameters: ?a=1&b=zz use `{"a":1,"b":"zz"}`)
 3. [JSONpath formatted](http://jsonpath.com/) expression of desired value. The result of this expression must be a single value.
 4. Name of trigger/event for step 2

When this cards executes succesfull, it will start flows with the 'GET variable step 2' trigger card and same trigger/event as step 1. The result of the JSONpath expression is available as a token on the card.

Happy hacking!
#### Notes   
  Passing a valid JSON string (at least `{}` ) is obligatory for cards with a JSON parameter.

###### Advanced HTTP options
  Instead of an url you can also provide a valid json with [node http options](https://nodejs.org/api/http.html#http_http_request_options_callback) in *every* card. These options will override options defined by the card to ensure maximal flexibility. Example with headers:
  ```
  {"method":"put","protocol":"https:","hostname":"httpbin.org","path":"/put","headers":{"User-Agent":"Node.js http.min"}}
  ```

###### Authorization on API calls
  API calls requires header `Authorization` with value `Bearer <token>`, where <token> is your secret token (get it by typing `window.bearer_token` in the chrome console while logged in on your Homey). This can be disabled in the settings screen of this app.

TODO:
