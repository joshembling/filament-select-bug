## Steps to recreate

Must be using MySQL 8.0 or greater due to nullable json column.

1. Clone this repo
2. `composer install`
3. Clone `.env.example`, set up your database creds
4. `php artisan migrate`
5. `php artisan make:filament-user`
6. Login at `/admin/login`
7. Go to Post resource
8. Create a post with all fields filled in - Title, Body, Category, Author
9. Check database has all these fields
10. Go to `App\Filament\Resources\PostResource`
11. Remove select options so you are left with:

```php
Forms\Components\Select::make('category')
->options([]),
```

and

```php
Forms\Components\Select::make('author')
->options([]),
```

12. Now go back to the post you created at `/admin/posts/1/edit`
13. Check no options exist in either select
14. Save resource
15. See that the database values have not changed for `category` and the `author` json.

This is not expected behaviour. If values no longer exist this should save the fields as null, just as when a user selects the placeholder manually.
