# SolusVM API #

SolusVM is a VPS control panel. This API is a wrapper for the [SolusVM API](http://docs.solusvm.com/v2/Default.htm#Developer/Admin-Api/Admin-Api.htm). Each command is mapped one-to-one with a Class and Method. For example, [Booting a Virtual Server](http://docs.solusvm.com/v2/Default.htm#Developer/Admin-Api/Virtual-Server-Functions/Boot.htm) requires the vserver-boot API command, which is executed via SolusvmVserver::boot().

#### NOTE ####

SolusVM responds with non-standard XML data. This API implementation makes every attempt to correct inconsistencies that appear in the response data in a forward-compatible way (anticipating that SolusVM corrects such issues in the future).


## Requirements ##

* PHP 5.1.3 or greater

## Using the API ##

```php
<?php
require_once "solusvm_api.php";

$user = "YOUR_SOLUSVM_USER"; // User ID required to access the API 
$key = "YOUR_SOLUSVM_KEY"; // Key required used to access the API 
$host = "mysolusvmserver.com"; // The host to connect to
$port = 5656; // The default port

$api = new SolusvmApi($user, $key, $host, $port);

// Create a new instance of the command class we want to use
$api->loadCommand("solusvm_vserver");
$vserver = new SolusvmVserver($api);

$vars = array('vserverid' => "1");

print_r($vserver->boot($vars)->response());
?>
```