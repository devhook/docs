# Theme


## Примеры решений:

- [teepluss/laravel4-theme](https://github.com/teepluss/laravel4-theme)

## Необходимо сделать:

[Issue #3](../../issues/3)


## Структура темы:

```
app/themes/
    {theme}/
        assets/
        layouts/
        partials/
        views/
        widgets/
        config.php
        preview.jpg
```

## Настройки темы (app/themes/{theme}/config.php):

```php
return array(
    'name' => 'Default theme',
    'version' => 1,
    'author' => array('name'=>'...', 'email'=>'...');
    
    'inherit' => null // OR 'default'
    'events' => array(
        'init' => function($theme){},
        'before_theme' => function($theme){},
        'before_layout' => array(
            'default' => function($theme){},
            'home' => function($theme){},
        ),
    ),
);
```
