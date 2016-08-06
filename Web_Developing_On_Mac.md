# Laravel Valet

Laravel Valet is a good platform for local testing of PHP sites.

Everything you need will be writing a custom driver. As an example, this my driver for Flarum, the newly emerging BBS platform.

```
<?php
class FlarumValetDriver extends ValetDriver
{
/**
  * Determine if the driver serves the request.
  *
  * @param  string  $sitePath
  * @param  string  $siteName
  * @param  string  $uri
  *
  * @return bool
  */
     public function serves($sitePath, $siteName, $uri)
     {
         return is_dir($sitePath.'/vendor/flarum') && file_exists($sitePath.'/flarum');
     }
/**
 * Determine if the incoming request is for a static file.
 *
 * @param  string  $sitePath
 * @param  string  $siteName
 * @param  string  $uri
 *
 * @return string|false
 */
    public function isStaticFile($sitePath, $siteName, $uri)
    {
        if ($this->isActualFile($staticFilePath = $sitePath.$uri)) {
            return $staticFilePath;
        }
        return false;
    }
/**
* Get the fully resolved path to the application's front controller.
*
* @param  string  $sitePath
* @param  string  $siteName
* @param  string  $uri
*
* @return string
*/
   public function frontControllerPath($sitePath, $siteName, $uri)
   {
        if (strpos($uri,'/admin') === 0) {
           return $sitePath.'/admin.php';
        }
        if (strpos($uri,'/api') === 0) {
           return $sitePath.'/api.php';
        }
       return $sitePath.'/index.php';
   }
}
```
