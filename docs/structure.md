Структура Инвестиционной системы
================================

# Терминология

- Инвестиционная система -
- Приложение -
- Блок - совокупность контроллеров составляющих единый пул задач приложения

Приложение состоит из четырех блоков:
- API
- Админка
- Личный Кабинет
- Консольные команды

# Планировщик задач

Планировщик задач использует консольные команды которые находятся в блоке `Консольные команды`

Запуск производится так:

`./yii <controller>[/<action>] [--param1=value]`

# Конструирование приложения

Навешивание событий происходит в классе `\eventer\Eventer`.

Он же дожен быть прописан в файле конфигурации `main.php`.
```php
return [
    // ...
    'bootstrap' => ['eventer'],
    // ...
];
```