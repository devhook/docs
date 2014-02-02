#Asset

## Todo

- Рекурсивный вызов зависимостей
- Пути к конфигам. (Пока без них)

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
</body>
</html>
<!-- View content -->
```
