# Laravel Shopping Cart

Shopping cart for Laravel Application.

# Installation

```shell
composer require "overtrue/laravel-shopping-cart:dev-master"
```

  or add the following line to your project's `composer.json`:

```json
"require": {
    "overtrue/laravel-lang": "dev-master"
}
```

then

```shell
composer update
```

After completion of the above, add the follow line to the section `providers` of `config/app.php`:

```php
'Overtrue\LaravelShoppingCart\ServiceProvider',
```

And add the follow line to the section `aliases`:

```php
'Cart'      => 'Overtrue\LaravelShoppingCart\Facade',
```

## Usage

### Add item to cart

**syntax:**

```php
string | null Cart::add(string | int $id, string $name, int $quantity, int | float 100.00 [, array $attributes = []]);
```

**example:**

```php
$rawId = Cart::add(37, 'Item name', 5, 100.00, ['color' => 'red']);
```

### Update item

**syntax:**

```php
Item Cart::update(string $rawId, int $quantity);
Item Cart::update(string $rawId, array $arrtibutes);
```

**example:**

```php
Cart::update('8a48aa7c8e5202841ddaf767bb4d10da', ['name' => 'New item name');
// or only update quantity
Cart::update('8a48aa7c8e5202841ddaf767bb4d10da', 5);
```

### Get all items

**syntax:**

```php
Collection Cart::all();
```

**example:**

```php
$items = Cart::all();
```


### Get item

**syntax:**

```php
Item Cart::get(string $rawId);
```

**example:**

```php
$item = Cart::get('8a48aa7c8e5202841ddaf767bb4d10da');
```

### Remove item

**syntax:**

```php
boolean Cart::remove(string $rawId);
```

**example:**

```php
Cart::remove('8a48aa7c8e5202841ddaf767bb4d10da');
```

### Destroy cart

**syntax:**

```php
boolean Cart::destroy(string $rawId);
```

**example:**

```php
Cart::destroy();
```

### Total price

**syntax:**

```php
int | float Cart::total();
```

**example:**

```php
$total = Cart::total();
```


### Count rows

return the number of rows.

**syntax:**

```php
int Cart::countRows();
```

**example:**

```php
$rows = Cart::countRows();
```


### Count quantity

**syntax:**

```php
int Cart::count($totalItems = true);
```

`$totalItems` : When `false`,will return the number of rows.

**example:**

```php
$count = Cart::count();
$rows = Cart::count(false); // same as Cart::countRows();
```

### Search items

**syntax:**

```php
Collection Cart::search(array $conditions);
```

**example:**

```php
$items = Cart::search(['color' => 'red']);
$items = Cart::search(['name' => 'Item name']);
$items = Cart::search(['qty' => 10]);
```

## Specifies the associated model

Specifies the associated model of item.

**syntax:**

```php
Cart Cart::associate(string $modelName);
```

**example:**

```php
Cart::associate('App\Models\Product');
$item = Cart::get('8a48aa7c8e5202841ddaf767bb4d10da');
$item->product->name; // $item->product is instanceof 'App\Models\Product'
```



## the Collection And Item

`Collection` and `Overtrue\LaravelShoppingCart\Item` both are instanceof `Illuminate\Support\Collection`, Usage Refer to：[Collections - Laravel doc.](http://laravel.com/docs/5.0/collections)

properties of `Overtrue\LaravelShoppingCart\Item`:

- `id` - your goods item ID.
- `name` - Name of item.
- `qty` - Quantity of item.
- `price` - Unit price of item.
- `total` - Total price of item.
- `__raw_id` - Unique ID of row.
- `__model` - Name of item associated Model.

## License

MIT