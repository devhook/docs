#Asset

Компонент управления скриптами и стилями шаблона. ! Не компилирует а только подключает скрипты и стили в необходимые места.

## Сторонние решения:
- Port Laravel 3 asset [teepluss/laravel4-asset](https://github.com/teepluss/laravel4-asset)
- [RoumenDamianoff/laravel-assets](https://github.com/RoumenDamianoff/laravel-assets)
- [orchestral/asset](https://github.com/orchestral/asset)
- [basset](http://jasonlewis.me/code/basset/4.0)


## Необходимо сделать
[issues/1](../issues/1)
- Конфиг. Описание набора ассетов. (! Определиться с путем к файлу)
- Регистрация ассета
- Зависимости ассетов
- Привязка части ассета к определенному размещению (перед `</body>`)
- Добавление ассетов в текущий шаблон
- Вывод необходимых ассетов в шаблоне в зависимости от размещения
- Вывод только указанных в методе ассетов
- Отдельные ассеты для разных контейнеров: сайт, админка
- Вывод ассетов определенного контейнера
- Добавление скрипта в виде: <script>/* code */</script>
- FIX: Рекурсивный вызов зависимостей


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

### Регистрация ассета

```php
Devhook\Asset::register('jquery', array('js' => 'path/to/jquery.min.js'));
```

Добавляет ассет к текущему шаблону

```php
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
