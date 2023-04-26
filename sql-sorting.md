### File
```
Traits/SortTrait.php
```

### Code
```php
<?php

namespace App\Traits;

trait SortTrait
{
    public function scopeSort($query, $sort = null, $defaultColumn = 'id')
    {
        $query->when($sort, function ($query, $sort) {
            $column = trim($sort, '-');
            $direction = str_starts_with($sort, '-') ? 'desc' : 'asc';
            $query->orderBy($column, $direction);
        }, function ($query) use ($defaultColumn) {
            $query->orderByDesc($defaultColumn);
        });
    }
}
```

### Usage
```php
User::sort(request('sort'))->get();
```

### URL
**Ascending Order URL**
```
https//domain.com/user?sort=name
```
**Descending Order URL**
```
https//domain.com/user?sort=-name
```
