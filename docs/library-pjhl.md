Что делает эта библиотека?
==========================

Описания языков должны храниться в переменной `Yii::$app->params['languages']` по типу:

```php
 [
    [
        'id'     => 1,
        'url'    => 'en',
        'locale' => 'en-EN',
        'name'   => 'English'
    ],
    [
        'id'      => 2,
        'url'     => 'ru',
        'locale'  => 'ru-RU',
        'name'    => 'Русский',
        'default' => true,
    ],
]
```


файл:
`vendor/pjhl/yii2-multilanguage/assets/static/ChangeLanguage.js`

фактически сохраняет значение идентификатора языка (`id` или `Yii::$app->params['languages'][$i]['id']`) в куки `x-language-id` и перезагружает страницу
```js
window.location.reload();
```

# Файл /helpers/Languages.php

Содержит класс
```php
class Languages
{
     // ...
}
```

## detectClientLangId()
```php
public static function detectClientLangId();
```

Определяет язык пользователя по кукам/браузеру. Если не удалось, возвращает стандартный

## init()
```php
public static function init()
```
Этот метод должен вызываться при инициализации контроллера, он делает редирект (если нужно) на выбранную языковую версию.
Каким образом?


# /helpers/LanguagesList.php

Содержит класс и оперирует с масивом языков `Yii::$app->params['languages']`. При конструировании загружает их в `$this->languages`
```php
class LanguagesList
{
     private $languages = [];
     // ...
}
```

## getConfigById()

```php
public function getConfigById($id);
```
Возвращает настройки языка по идентификатору `id`
Если найдены то возвращается масив в виде:
```php
[
    'id'      => 2,
    'url'     => 'ru',
    'locale'  => 'ru-RU',
    'name'    => 'Русский',
    'default' => true,
]
```
Если не найдены то возвращается null

# /components/AdvancedUrlManager.php

```php
class AdvancedUrlManager extends UrlManager
{
     public $multilanguageHideDefaultPrefix = false;
     // ...
}
```

## createUrl()

```php
public function createUrl($params)
```
Алгоритм функции в [диаграме](https://drive.google.com/file/d/0B9lrcmdS-YbTWjhqeWcxRUQxaTg/view?usp=sharing)

Переменная `multilanguageHideDefaultPrefix` boolean
`true` - Не добавляет в формируемый url префикс языка (параметр `url` из описания языка)
`false` - Добавляет в формируемый url префикс языка (параметр `url` из описания языка)

Формула функции такова:
Если есть в параметрах `$params` переменная `$params['x-language-url']`, то она убирается из параметров и добавляется в формируемый URL по формату `$url = '/' . $url_prefix . $url`

# /components/AdvancedRequest.php

Содержит расширение обработчика Запроса \yii\web\Request

```php
class AdvancedRequest extends Request {
    private $lang_url = null;
    // ...
}
```
