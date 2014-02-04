# Theme

Структура файлов:

| Файл / Папка  | Описание                                                       |
| ------------- | -------------------------------------------------------------- |
| public/       | Папка с публичными файлами (стили, скрипты, картинки)          |
| layouts/      | Папка с файлами шаблона (default.php, home.php, mobile.php)    |
| partials/     | Папка с файлами частей шаблона (header.php, footer.php)        |
| views/        | Папка с файлами предстовлений в виде `{controller}/{view}.php` |
| widgets/      | Папка с шаблонами виджетов                                     |
| config.php    | Конфигурационный файл темы                                     |
| preview.jpg   | Скриншот темы (640x480)                                        |

```php
<?php
// partials
echo $theme->partial('footer')->render();

// views
echo $theme->view('news/index')->with('news', '...')->render();

// widgets
$theme->breadcrumbs()->add('Item', '#link');
$theme->breadcrumbs()->template('breadcrumbs'); // {theme}/partials/breadcrumbs

echo $theme->widget('news')->render();
```

> Содержимое папки `app/themes/{theme}/public/` копируется в папку `public/themes/{theme}/`


## Настройки темы

Файл: `app/themes/{theme}/config.php`

```php
<?php
return array(
    // Название темы
    'name' => 'Simple theme',

    // Описание темы
    'description' => '',

    // Автор темы
    'author' => 'Devhook',

    // Наследование
    // Если в текущей теме какой то файл отсутствует,
    // то этот файл будет искаться в наследованной теме
    'inherit' => false, // OR 'default' OR array('path' => 'path/to/theme/root')

    // Регистрация всех ассетов темы
    'assets' => array(),

    // События
    'events' => array(
        // 'init' => function($theme){},
        // 'before_theme' => function($theme){},
        // 'before_layout' => array(
        //     'default' => function($theme){},
        //     'home' => function($theme){},
        // ),
    ),
);
?>
```

## Использование в контроллере

```php
<?php
Route::get('news/{id}', function($id){

    $theme = app('theme'); // default theme and layout

    // $theme = Devhook\Theme::theme('default')->layout('mobile');
    // $theme = app('theme')->theme('default')->layout('mobile');
    Devhook\Theme::theme()->
    $theme->setTitle('News');
    $theme->setDescription('...');

    $theme->breadcrumbs()->add('News', 'news');

    $theme->asset()->add('path/to/news.js');
    // OR:
    // Devhook\Theme::asset()->add('path/to/custom/global.js', 'footer');

    $theme->content('news/show', array(
        'news' => News::find($id),
    ));

    // OR:
    // $theme->setContent('custom content string');

    echo $theme;
});
?>
```

## Использование в шаблоне (layout/default.php)

```php
<!doctype html>
<html lang="<?=$theme->lang ?>">
<head>
    <meta charset="UTF-8">
    <title><?=$theme->title ?></title>
    <meta type="description" content="<?=$theme->description ?>">
    <meta type="keywords" content="<?=$theme->keywords ?>">

    <?=$theme->asset()->styles() ?>
    <?=$theme->asset()->scripts() ?>
</head>
<body>
    <?=$theme->partial('header')->render() ?>

    <?=$theme->widget('breadcrumbs')->render() ?>

    <?=$theme->content ?>

    <?=$theme->partial('footer')->render() ?>

    <?=$theme->asset()->scripts('footer')->render() ?>
</body>
</html>
```



## Глобальные настройки

Файл: `app/packages/devhook/theme/config.php`

```php
<?php
return array(

    // app/themes/{theme}/*
    'theme_path' => app_path() . '/themes',

    'components' => array(
        'asset'       => 'Devhook\Theme\Asset',
        'breadcrumbs' => 'Devhook\Theme\Breadcrumbs',
        // 'menu'     => 'Devhook\Theme\Menu',
        // 'notice'   => 'Devhook\Theme\Notice',
    ),

    // public/themes/{theme}/(css|js|img)
    'public_dir' => 'themes',

    'default_theme' => 'default',
    'default_layout' => 'default',

    'assets' => array(),

    'events' => array(),
);
?>
```


## Advanced

```php
<?php
App::singleton('adminTheme', function()
{
    return new Devhook\Theme\Theme($config, new Devhook\Theme\Asset);
});

app()->adminTheme->asset()->add('add/to/admin/script.js', 'footer');
```
