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
