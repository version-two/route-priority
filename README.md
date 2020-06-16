## Package to add priority to Laravel 7 routes

[![Latest Stable Version](https://poser.pugx.org/bexvibi/route-priority/v/stable)](https://packagist.org/packages/bexvibi/route-priority) 
[![Total Downloads](https://poser.pugx.org/bexvibi/route-priority/downloads)](https://packagist.org/packages/bexvibi/route-priority) 
[![Latest Unstable Version](https://poser.pugx.org/bexvibi/route-priority/v/unstable)](https://packagist.org/packages/bexvibi/route-priority) 
[![License](https://poser.pugx.org/bexvibi/route-priority/license)](https://packagist.org/packages/bexvibi/route-priority)

### Installation
You can install the package via composer:
``` bash
composer require bexvibi/route-priority
```
Now open up `app/config/app.php` and add the service provider to your `providers` array.

	bexvibi\RoutePriority\RoutePriorityServiceProvider::class,

Add the trait to `App\Http\Kernel`

	use \bexvibi\RoutePriority\RouterTrait;

### Usage

Change routes priority:

```php
Route::get('test', ['uses' => 'Controller@showAction'])->setPriority(100);
```

### Default Priority

Default priority is `50`. Higher priority - values from 50 and above, lower priority - `49` and below.

### Usage example

```php
Route::get('/test/{slug}', …);
Route::get('/test/hello', …);
```

In this example second route will not work. Add priority 0 to the first route will fix the error:

```php
Route::get('/test/{slug}', …)->setPriority(0);
Route::get('/test/hello', …);
```

Second route now has higher priority.

### Group priority

You can put priority to groups:

```php
Route::group(['prefix' => 'test-group', 'priority' => 10], function () {
	Route::get('/test/hello', function () {
	    return 'First group';
	});
});

Route::group(['prefix' => 'test-group', 'priority' => 20], function () {
	Route::get('/test/hello', function () {
	    return 'Second group';
	});
});
```

Second group has higher priority then First group. All routes in the group will has the same priority as the group.
