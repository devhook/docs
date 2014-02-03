# Theme


## Примеры решений:

- [teepluss/laravel4-theme](https://github.com/teepluss/laravel4-theme)

## Необходимо сделать:

[Issue #3](../../issues/3)


## Структура темы:

```
app/themes/
    {theme}/
        public/
        layouts/
        partials/
        views/
        widgets/
        config.php
        preview.jpg
```

> Содержимое папки `app/themes/{theme}/public/` копируется в папку `public/themes/{theme}/`


## Настройки темы (app/themes/{theme}/config.php):

```php
return array(
    'name' => 'Default theme',
    'description' => '',
    'author' => 'Devhook';
    
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

## Использование

```php
$theme = Theme::make('default')->layout('mobile');

$theme->setTitle('News');
$theme->setDescription('...');

$theme->asset->add('path/to/news.js');

$theme->view('news/index', array(
    'news' => News::all(),
));

echo $theme;
```
