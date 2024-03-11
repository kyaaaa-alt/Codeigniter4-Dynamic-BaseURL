### Updated up to Codeingiter 4.4.6
### /app/Config/Constants.php
Added support for servers behind a load balancer, and it's will work share local app using **localhost.run** or **ngrok.io**
Put the code below and place it at the end of the line of the file `/app/Config/Constants.php`
```
$isSecure = false;

if (
    (isset($_SERVER['HTTPS']) && $_SERVER['HTTPS'] === 'on') ||
    (isset($_SERVER['HTTP_X_FORWARDED_PROTO']) && $_SERVER['HTTP_X_FORWARDED_PROTO'] === 'https') ||
    (isset($_SERVER['HTTP_X_FORWARDED_SSL']) && $_SERVER['HTTP_X_FORWARDED_SSL'] === 'on')
) {
    $isSecure = true;
}

$protocol = $isSecure ? 'https' : 'http';
$base = $protocol . '://' . (isset($_SERVER['HTTP_HOST']) ? $_SERVER['HTTP_HOST'] : '127.0.0.1');
$base .= str_replace(basename($_SERVER['SCRIPT_NAME']), '', $_SERVER['SCRIPT_NAME']);

defined('BASE') || define('BASE', str_replace('\\', '', $base));
```

### /app/Config/App.php
Find line of `public $baseURL` and change the value to `BASE`
```
public $baseURL = BASE;
```
