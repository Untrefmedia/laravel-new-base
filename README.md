### laravel-new-base

1.

[https://github.com/Hesto/multi-auth]()

composer require hesto/multi-auth
php artisan multi-auth:install admin -f

2.
#### Add to model Admin
On app/Admin.php
```
/**
* Relation
* @return mixed
*/
public function venues()
{
    return $this->belongsToMany('Untrefmedia\UMBooks\App\Venue', 'venue_admin', 'admin_id', 'venue_id');
}

/**
* Relation
* @return mixed
*/
public function createdEvents()
{
    return $this->hasMany('Untrefmedia\UMBooks\App\Event', 'admin_id', 'id');
}
```

3.
#### laravel-cors
Config "spatie/laravel-cors" on app/http/kernel.php
```
    protected $middleware = [
        ...
        \Spatie\Cors\Cors::class
    ];
```

4.
#### mandrill for send email
Config on app/config/services.php
```
'mandrill' => [
        'secret' =>  env('MAIL_PASSWORD'),
    ],
```

5.
#### Intervention\Image\Image
Config providers and facade on config/app.php
[http://image.intervention.io/getting_started/installation#laravel]

6.
#### spatie/laravel-permission
Add middleware on app/Http/Kernel.php
[https://github.com/spatie/laravel-permission#using-a-middleware]
```
protected $routeMiddleware = [
    // ...
    'role' => \Spatie\Permission\Middlewares\RoleMiddleware::class,
    'permission' => \Spatie\Permission\Middlewares\PermissionMiddleware::class,
    'role_or_permission' => \Spatie\Permission\Middlewares\RoleOrPermissionMiddleware::class,
];
```

7.
#### spatie/laravel-permission
Role super-admin with all permissions
[https://github.com/spatie/laravel-permission/wiki/Global-%22Admin%22-role]

Add on app/Providers/AuthServiceProvider.php
```
public function boot()
{
    ...
    
    // Implicitly grant "super-admin" role all permissions
    // This works in the app by using gate-related functions like auth()->user->can() and @can()
    Gate::before(function ($user, $ability) {
        return $user->hasRole('super-admin') ? true : null;
    });
}
```