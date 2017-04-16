# Firebase PHP Client

A PHP client for the [Google Firebase](https://firebase.google.com) Realtime Database

Forked from [Firebase-PHP v1.x](https://github.com/kreait/firebase-php/tree/1.x) by @jeromegamez 

How this fork is different from the original:
 * This fork is a drop-in ready version of the code. I'm committing it with all the libraries and dependencies needed so all you need to do is download it and `include()` it into your project. No Composer needed.
 * This is a fork of the v1.x code so it only requires PHP 5.6 or above.
 * The original source pulls in over [11 MB of Google SDK code which is never used](https://github.com/kreait/firebase-php/issues/74). These useless files are stripped out of the Composer vendor tree and the `autoload.php` file has been edited so that the 5000+ unused classes are not loaded. At a later stage the dependency should be completely removed. 
 * The `Query` class now supports the `silent` parameter.
 * The `set`, `put`, `update` and `delete` functions are now sent with the `silent` parameter. The functions now return the HTTP status code so you can see if the operation was a success or not.
 * This fork is meant to be a "working snapshot". The code works as it is now and will be more or less "frozen". I wont be actively maintaining it unless there is a serious security flaw or incompatibility. If you are looking for a more up to date version, please see the original repo.
---

## Quick usage example

```php

require_once 'firebase-php/vendor/autoload.php';

use Kreait\Firebase\Configuration;
use Kreait\Firebase\Firebase;

$config = new Configuration();
$config->setAuthConfigFile('/path/to/google-service-account.json');

$firebase = new Firebase('https://my-app.firebaseio.com', $config);

$res = $firebase->set(['key' => 'value'], 'my/data');

if ($res < 300) //The HTTP result code for the set() command was successful:
{
	print_r($firebase->get('my/data'));
	$firebase->delete('my/data');
}
else
{
	throw new Exception("Something went wrong!");
}

```

## Documentation

You can find the documentation at http://firebase-php.readthedocs.io/en/1.x/
