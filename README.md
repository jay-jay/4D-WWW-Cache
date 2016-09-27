# 4D-W3
Features
- Static caching for 4D.
  - Cache will be saved as file under directory w3.4dbase/w3_cache/
- Extended json parser
##Usage

### Set a Cache
```
Syntax: _w3_set_cache(key ; content)
returns BOOLEAN

Example 1:
$cache_is_set:=_w3_set_cache ($url;$body)

Example 2:
$endpoint:="http://www.james.borillo.com"
$http_status:=HTTP Get($endpoint;$response)
$cache_is_set:=_w3_set_cache ($endpoint;$response)

```

### Get a Cache
```
Syntax: _w3_get_cache(key)
returns cache content

Example:
$txt:=_w3_get_cache("http://www.jamesborillo.com")

```

### Parse a JSON
```
Syntax: _w3_ob_value(objects;string_object)
returns string, object as string, array object as string
Important: Use Json Parse or Json Parse Array for returned value

Example:
$txt:=_w3_ob_value($object;"property->propert_array[2]->property->value")

```
