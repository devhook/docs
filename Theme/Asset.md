#Asset

Компонент управления скриптами и стилями шаблона. ! Не компилирует а только подключает скрипты и стили в необходимые места.

## Примеры

Добавление скриптов и стилей к текущему шаблону

```php
<?php
// Добавление ссылки на скрипт к шаблону
Devhook\Theme::asset()->add('path/to/custom.js');

// Добавление ссылки на файл стилей к шаблону
Devhook\Theme::asset()->add('path/to/style.css');

// Добавление ссылки на скрипт к шаблону перед закрывающим BODY
Devhook\Theme::asset()->add('path/to/custom-footer.js', 'footer');

// Добавление стилей
Devhook\Theme::asset()->writeStyle('body {background:#EEE}');

// Добавление скрипта перед закрывающим BODY
Devhook\Theme::asset()->writeScript('$("#alert").show()', 'footer');
?>
```

Регистрация ассетов (предопределенные ассеты)

```php
<?php
// Пример 1 (jQuery)
Devhook\Theme::asset()->register('jquery', 'path/to/jquery.min.js');

// Пример 2 (Twitter Bootstrap)
Devhook\Theme::asset()->register('bootstrap', array(
    'required' => 'jquery',
    'css'      => array(
        'path/to/bootstrap.min.css',
        'path/to/bootstrap-theme.min.css',
    ),
    'js' => array(
        'path/to/bootstrap.min.js' => 'footer',
    ),
));

// Пример 3 (Групповое добавление)
Devhook\Theme::asset()->register(array(
    'jquery' => 'path/to/jquery.min.js',
    'jquery-ui' => array(
        'required' => 'jquery',
        'js' => 'path/to/jquery.min.js'
    ),
));
?>
```

Добавление ранее зарегистрированных ассетов к текущему шаблону

```php
<?php
// Добавляет ранее зарегистрированные ассет(ы) к текущему шаблону
Devhook\Theme::asset()->required('jquery', 'bootstrap', 'ckeditor');
?>
```


Использование в шаблонах

```php
<!DOCTYPE html>
<html>
    <head>
        <title>Title</title>
        <?= Devhook\Theme::asset()->styles() ?>
        <?= Devhook\Theme::asset()->scripts() ?>
    </head>
    <body>
        <?= $content ?>

        <?= Devhook\Theme::asset()->scripts('footer') ?>
    </body>
</html>
```
