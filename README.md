### laravel-new-base

1.

[https://github.com/Hesto/multi-auth]()

composer require hesto/multi-auth
php artisan multi-auth:install admin -f



2.
#### laravel-cors
Config "spatie/laravel-cors" on app/http/kernel.php
```
    protected $middleware = [
        ...
        \Spatie\Cors\Cors::class
    ];
```

3.
#### mandrill for send email
Config on app/config/services.php
```
'mandrill' => [
        'secret' =>  env('MAIL_PASSWORD'),
    ],
```