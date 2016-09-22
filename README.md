# 4D-WWW-Cache
Static caching for 4D

##Usage
```
$txt:=_w3c_get_cache("http://www.jamesborillo.com")

If ($txt="") // Create cache

$endpoint:=http://www.jamesborillo.com
$http_status:=HTTP Get($endpoint;$response)
$cache_is_set:=_w3c_set_cache ($endpoint;$response)

End if 

```
