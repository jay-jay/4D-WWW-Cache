# 4D-W3

#### Contributors are welcome

## Installation
1. Drop w3.4dbase into your 4D Application's Components folder
2. Under Resources, rename config-sample.json to config.json
3. Enter desired cache_expire. We only support days for cache_expire but we are open to contributors for an extended functionality.
4. Done

### Features
- Cache content dynamically generated into file caching for 4D.
  - Cache will be saved as file under directory YOU_APPLICATION.4dbase/w3_cache/
- Extended json parser

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

The following method is requred in your application in order for the above URL to work
```
Method purge_cache content
C_TEXT($0;$1)
w3_purge_cache
```
### Parse a JSON
```
Syntax: w3_ob_value(objects;string_object)
returns string, object as string, array object as string
Important: Use Json Parse or Json Parse Array for returned value

Example:
$txt:=w3_ob_value($object;"property->propert_array[2]->property->value")

```
