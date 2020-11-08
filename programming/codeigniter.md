# CodeIgniter

![Image by Teknologi.id](https://berita.teknologi.id/uploads/2018/04/CodeIgniter-620x350-c.png)

[CodeIgniter](https://codeigniter.com) is a powerful PHP framework with a very small footprint, built for developers who need a simple and elegant toolkit to create full-featured web applications..

## Table Of Contents

1. [Solved, CodeIgniter 3 with HMVC error on PHP 7](#solved-codeigniter-3-with-hmvc-error-on-PHP-7)

## Solved, CodeIgniter 3 with HMVC error on PHP 7

If you’re using Codeigniter 3 with Modular Extensions/HMVC on PHP version 7, you might be seeing the following error:

> Message: strpos(): Non-string needles will be interpreted as strings in the future. Use an explicit chr() call to preserve the current behavior

Just change `application/third_party/MX/Router.php` line 239:

```php
public function set_class($class)
{
  $suffix = $this->config->item('controller_suffix');
  if (strpos($class, $suffix) === FALSE)
  {
    $class .= $suffix;
  }
  parent::set_class($class);
} 
```

to this:

```php
public function set_class($class)
{
  $suffix = $this->config->item('controller_suffix');
  if($suffix && strpos($class, $suffix) === FALSE)
  {
    $class .= $suffix;
  }
  parent::set_class($class);
} 
```