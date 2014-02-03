#Asset

Компонент управления скриптами и стилями шаблона. ! Не компилирует а только подключает скрипты и стили в необходимые места.

## Сторонние решения:
- Port Laravel 3 asset [teepluss/laravel4-asset](https://github.com/teepluss/laravel4-asset)
- [RoumenDamianoff/laravel-assets](https://github.com/RoumenDamianoff/laravel-assets)
- [orchestral/asset](https://github.com/orchestral/asset)
- [basset](http://jasonlewis.me/code/basset/4.0)


## Необходимо сделать
[Issues #1](../../issues/1)

## Конфигурация

Путь к конфигурационному файлу:
- app/config/asset.php
- ? app/config/packages/devhook/asset/config.php
- ? app/config/packages/devhook/components/asset.php

Пример конфига:
```php
return array(
    
    'assets' => array(
        
        'jquery' => 'path/to/jquery.min.js',

        'normalize' => 'path/to/normalize.min.css',
        
        'bootstrap' => array(
            'required' => 'jquery',
            'js' => array(
                'path/to/bootstrap.min.js' => 'footer',
            ),
            'css' => array(
                'path/to/bootstrap.min.css',
                'path/to/bootstrap-theme.min.css',
            )
        ),
    ),
    
);
```

## Примеры

Добавление скриптов и стилей к текущему шаблону
```php
// Добавление ссылки на скрипт к шаблону
Devhook\Asset::add('path/to/custom.js');

// Добавление ссылки на файл стилей к шаблону
Devhook\Asset::add('path/to/style.css');

// Добавление ссылки на скрипт к шаблону перед закрывающим BODY
Devhook\Asset::add('path/to/custom-footer.js', 'footer');

// Добавление стилей
Devhook\Asset::addStyle('body {background:#EEE}');

// Добавление скрипта перед закрывающим BODY
Devhook\Asset::addScript('$("#alert").show()', 'footer');
```

Примеры регистрации ассетов (предопределенные ассеты) 
```php
// Пример 1 (jQuery)
Devhook\Asset::register('jquery', 'path/to/jquery.min.js');

// Пример 2 (Twitter Bootstrap)
Devhook\Asset::register('bootstrap', array(
    'required' => 'jquery',
    'css'      => array(
        'path/to/bootstrap.min.css',
        'path/to/bootstrap-theme.min.css',
    ),
    'js' => array(
        'path/to/bootstrap.min.js' => 'footer',
    ),
));
```

Добавление ранее зарегистрированных ассетов к текущему шаблону
```php
// Добавляет ранее зарегистрированные ассет(ы) к текущему шаблону
Devhook\Asset::required('jquery', 'bootstrap', 'ckeditor');
```


Использование в шаблонах
```php
<!DOCTYPE html>
<html>
    <head>
        <title>Title</title>
        <?= Devhook\Asset::styles() ?>
        <?= Devhook\Asset::scripts() ?>
    </head>
    <body>
        <?= $content ?>

        <?= Devhook\Asset::scripts('footer') ?>
    </body>
</html>
```
