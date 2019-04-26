# Variables

## 1. $\_SERVER\(= $HTTP\_SERVER\_VARS \[removed\]\)

> #### 'DOCUMENT\_ROOT'
>
> The document root directory under which the current script is executing, as defined in the server's configuration file.

```php
chdir($_SERVER['DOCUMENT_ROOT']);   // '/var/www/html'
define('DRUPAL_ROOT', getcwd());    // DRPAL_ROOT = 'var/www/html'
```

* **A few "magical" PHP constants**

| Name | Description |
| :--- | :--- |
| \_\_LINE\_\_ | The current line number of the file. |
| \_\_FILE\_\_ | The full path and filename of the file with symlinks resolved. If used inside an include, the name of the included file is returned. |
| \_\_DIR\_\_ | The directory of the file. If used inside an include, the directory of the included file is returned. This is equivalent to dirname\(\_\_FILE\_\_\). This directory name does not have a trailing slash unless it is the root directory. |
| \_\_FUNCTION\_\_ | The function name, or {closure} for anonymous functions. |
| \_\_CLASS\_\_ | The class name. The class name includes the namespace it was declared in \(e.g. Foo\Bar\). Note that as of PHP 5.4 \_\_CLASS\_\_ works also in traits. When used in a trait method, \_\_CLASS\_\_ is the name of the class the trait is used in. |
| \_\_TRAIT\_\_ | The trait name. The trait name includes the namespace it was declared in \(e.g. Foo\Bar\). |
| \_\_METHOD\_\_ | The class method name. |
| \_\_NAMESPACE\_\_ | The name of the current namespace. |
| ClassName::class | The fully qualified class name. See also [::class](https://www.php.net/manual/en/language.oop5.basic.php#language.oop5.basic.class.class). |



