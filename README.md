# 4D-W3 Component
This component will serve as a simple http component but the main functionality is its caching.

#### Contributors are welcome

## Installation
1. Drop w3.4dbase into your 4D Application's Components folder
2. Under /w3.4dbase/Resources, rename config-sample.json to config.json
3. Enter desired cache_expire. We only support days for cache_expire but we are open to contributors for an extended functionality.
4. Enable by assigning true to config cache_enabled
5. Done

### Features
- Cache content dynamically generated into file caching for 4D.
  - Cache will be saved as file under directory YOU_APPLICATION.4dbase/w3_cache/
- Extended json parser
- Essential helper methods like URL and Request manipulation 

### HTTP Request methods
***
#### w3_add_query_string
Adds a query string or replaces if it exist from a URL if parameter 4 is TRUE
```
$1 TEXT     URL
$2 TEXT     Query string
$3 TEXT     New value
$4 BOOLEAN  Replace if exists

Example:
$current_url:="/my-url-slug/?year=2017"
$new_url:=w3_add_query_string ($current_url;"year";"2018";True)
```
$new_url is "/my-url-slug/?year=2017"
***
#### w3_ob_http_header
Returns HTTP HEADERS as JSON
````
$0 OBJECT  Returns HTTP HEADERS as JSON

Example:
C_OBJECT($o_header)
C_TEXT($userAgent)
$o_header:=w3_ob_http_header 
$userAgent:=OB Get($o_header;"User-Agent")
````
***
#### w3_ob_url_params
This method will parse URL parameters and converts them into json
````
$0 OBJECT  Url parameters in Json format
$1 TEXT    URL

Example:
C_OBJECT($o_params)
$o_params:=w3_get_url_params ("?x=99&y=88")

Return:
{
  "x" : "99",
  "y" : "88"
}
````
***
#### w3_replace_segment
````
Replaces a segment from a clean-url
$1 LONGINT  segment position
$2 TEXT     clean-url (ugly-url can be passed as well but no effect)
$3 TEXT     text replaceent to specified segment in $1
````
***
#### w3_request
````
PHP equivalent of $_REQUEST
$0 TEXT  Returns value of requested URL parameter from current URL
$1 TEXT  url parameter
````
***
#### w3_request_segment
````
Returns a pretty-url segment
$1 LONGINT  segment position
$2 TEXT     clean-url
````
***
#### w3_send_response
````
Handles HTTP responses. Can send responses as HTML, JSON, Redirects or any text
$1   TEXT     Response(json, html)-Ignored if$2 is 301
{$2} LONGINT  HTTP status code(default: 200)-Use 301 to redirect
{$3} TEXT     Content-Type(default: text/html)(It is good practice to send response with the proper content-Type)
{$4} TEXT     Redirect URL(This is ignored if status code is NOT 301)
````
***
### Set a Cache
```
Syntax: w3_set_cache(key ; content)
returns BOOLEAN

Example 1:
$cache_is_set:=w3_set_cache ($url;$body)

Example 2:
$endpoint:="http://www.james.borillo.com"
$http_status:=HTTP Get($endpoint;$response)
$cache_is_set:=w3_set_cache ($endpoint;$response)

```

### Get a Cache
```
Syntax: w3_get_cache(key)
returns cache content

Example:
$txt:=w3_get_cache("http://www.jamesborillo.com")

```

### Purge Cache

```
Example:
http://www.yourdomain.com/4daction/purge_cache/?key=http://www.jamesborillo.com
```
will purge a cached key "http://www.jamesborillo.com"

Method "purge_cache" is requred in your application in order for the above URL to work. Add the following lines in the method.
```
C_TEXT($0;$1)
w3_purge_cache
```
***
### Parse a JSON
```
Syntax: w3_ob_value(objects;string_object)
returns string, object as string, array object as string
Important: Use Json Parse or Json Parse Array for returned value

Example:
$txt:=w3_ob_value($object;"property->propert_array[2]->property->value")

```
