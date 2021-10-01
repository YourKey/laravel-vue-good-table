# laravel-vue-good-table
Customizable table tool for Laravel, uses powerful [vue-good-table](https://xaksis.github.io/vue-good-table/). Server side tables without pain.

Supports pagination, filtering, searching, sorting. Inspired by Laravel Nova :)

![til](https://xaksis.github.io/vue-good-table/hero-image.png)

## Reqs
- Laravel 5.6+ or Laravel 6, Laravel 7, Laravel 8
- Using Vue.js in your project

## Usage example

1. Use `InteractsWithVueGoodTable` trait in your controller and implement two methods: `getColumns()` and `getQuery()`.
2. Register two new routes.
3. Use Vue component `laravel-vue-good-table` wherever you want.

#### Controller:
```php

namespace App\Http\Controllers;

use LaravelVueGoodTable\InteractsWithVueGoodTable;
use LaravelVueGoodTable\Columns\Column;
use LaravelVueGoodTable\Columns\Date;
use Illuminate\Http\Request;
use App\User;

class TestController extends Controller
{
    use InteractsWithVueGoodTable;

    /**
     * Get the query builder
     * 
     * @param Request $request
     *
     * @return Illuminate\Database\Eloquent\Builder
     */
    protected function getQuery(Request $request)
    {
        return User::query();
    }

    /**
     * Get the columns displayed in the table
     *
     * @return array
     */
    protected function getColumns(): array
    {
        return [
            Text::make('ID', 'id')
                ->sortable()
                ->searchable(),
                
            Text::make('Name', 'name')
                ->searchable(),
                
            Text::make('E-mail', 'email')
                ->searchable(),
                
            Date::make('Created At', 'created_at')
                ->sortable()
                ->dateOutputFormat('dd.MM.yyyy HH:mm:ss'),
        ];
    }
}
```

#### Routes:
```php
Route::get('/lvgt/config', 'TestController@handleConfigRequest');
Route::get('/lvgt/data', 'TestController@handleDataRequest');
```

#### Blade/HTML:
```blade
<div id="vue">
    <laravel-vue-good-table data-url="/lvgt/data" config-url="/lvgt/config"/>
</div>
```

## Installation
```
composer require underwear/laravel-vue-good-table
```
See the full [Installation Guide in DOCUMENTATION.md](./DOCUMENTATION.md#installation)

## Documentation
See [DOCUMENTATION.md](./DOCUMENTATION.md)

## Contributing
Contributions are welcome!

## Credits
* [Igor Filippov](https://github.com/underwear/)

## License
The MIT License (MIT). Please see [License File](./LICENSE) for more information.
