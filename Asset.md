#Asset


## Необходимо

- Конфиг. Описание набора ассетов. (! Определиться с путем к файлу)
- Регистрация ассета
- Зависимости ассетов
- Привязка части ассета к определенному размещению (перед `</body>`)
- Добавление ассетов в текущий шаблон
- Вывод необходимых ассетов в шаблоне в зависимости от размещения
- Вывод только указанных в методе ассетов
- Отдельные ассеты для разных контейнеров: сайт, админка
- Вывод ассетов определенного контейнера
- FIX: Рекурсивный вызов зависимостей


## Config

Config file:
- app/config/asset.php
- ? app/config/packages/devhook/asset/config.php
- ? app/config/packages/devhook/components/asset.php

```php
<?php return array(
	
	'assets' => array(
        
        'jquery' => array(
            'js' => 'path/to/jquery.min.js'
        ),
        
        'normalize' => array(
            'css' => 'path/to/normalize.min.css'
        ),
        
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

## Examples

### Регистрация ассета

```php
Devhook\Asset::register('jquery', array('js' => 'path/to/jquery.min.js'));
```

### Использование в представлении

```php
<?php
Devhook\Asset::required('jquery');
?>
<!-- View content -->
```

### Использование в шаблонах 

```php
<html>
<head>
    <!-- ... -->
    <?=Devhook\Asset::styles() ?>
    <?=Devhook\Asset::scripts() ?>
</head>
<body>
    <!-- ... -->
    
    <?=Devhook\Asset::scripts('footer') ?>
    <!-- OR -->
    <?=Devhook\Asset::place('footer')->scripts() ?>
</body>
</html>
<!-- View content -->
```
