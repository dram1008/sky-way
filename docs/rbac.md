Роли Рользователей и права доступа
==================================

# Терминология

- Пользователь
- Элемент - это Роль или Разрешение
- Роль (Role)
- Разрешение (Permission)

В приложении `Sky-Way` Используется RBAC менеджер `\yii\rbac\DbManager` и `\backend\components\Accessor`.

# `\yii\rbac\DbManager`
Настраивается через Базу данных

В таблице `auth_item` перечисляются Элементы
где `type`:
- 1: Разрешение (Permission)
- 2: Роль (Role)

В таблице `auth_item_child` перечисляется какой элемент имеет каких родственников

# `\backend\components\Accessor`

Используется в контроле доступа к контроллеру следующим образом

```php
class Controller extends \yii\web\Controller
{
    // ...
    public function beforeAction($action)
    {
        if (parent::beforeAction($action)) {
            if (Yii::$app->user->isGuest && !in_array($this->id, ['site'])) {
                return Yii::$app->getResponse()->redirect(['site/login']);
            }

            if (!Yii::$app->accessor->checkAccess([
                'userId'       => Yii::$app->user->id,
                'controllerId' => $this->id,
                'actionId'     => $this->action->id
            ])
            ) {
                throw new HttpException(403, 'Нет доступа');
                return false;
            }

            return true;
        }

        return false;
    }
    // ...
}
```

Права распределяются в настройках компонента `\backend\components\Accessor` в `main.php`

```php
return [
    // ...
    'components'          => [
        'accessor'     => [
            'class' => 'backend\components\Accessor',
            'rules' => [
                'sales'        => [
                    'all' => ['sales']
                ],
                // ...
                'user_manage'  => [
                    'users' => ['*'],
                    'user'  => ['*']
                ]
            ],
            'home'  => 'site'
        ],

```

```php
'sales'        => [
    'all' => ['sales']
],
```

это значит что пользователь имеющий элемент `sales`
имеет доступ только в контроллер 'all', действие 'sales'

Возможные значения

```php
'sales' => '*'
```
доступ во все контроллеры и действия

```php
'sales'        => [
    'all' => ['*']
],
```
доступ во все действия контроллера 'all'

```php
'sales'        => [
    'all' => ['sales']
],
```
доступ только в действие 'sales' контроллера 'all'

# `sidebar`




