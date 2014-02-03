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
<?php return array(
	
	'assets' => array(
        
        'jquery' => 'path/to/jquery.min.js',

        'normalize' => 'path/to/normalize.min.css',
        
        'bootstrap' => array(
            'required' => 'jquery',
            'js' => array(
                'file' => 'path/to/bootstrap.min.js',
                'place' => 'footer',
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

```php
// Добавление ассета к 
Devhook\Asset::add('path/to/custom.js');

Devhook\Asset::add('path/to/custom-footer.js', 'footer');

Devhook\Asset::addScript('$("#alert").show()', 'footer');

// Регистрация ассета
Devhook\Asset::register('jquery', 'path/to/jquery.min.js');

// Регистрация ассета
Devhook\Asset::register('bootstrap', array(
	'required' => 'jquery',
	'css' => 'path/to/bootstrap.min.css',
	'js' => array('path/to/jquery.min.js', 'place'),
));

// Добавляет ассет к текущему шаблону
Devhook\Asset::required('jquery', 'ckeditor');

```


Использование в шаблонах 

```php
// for <head>
echo Devhook\Asset::styles();
echo Devhook\Asset::scripts();

// before </body>
echo Devhook\Asset::place('footer')->scripts();
```
