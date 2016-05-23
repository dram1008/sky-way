Java Script
===========

# Функция `ajaxJson`

Объявлена в `backend/web/js/common.js`

## Параметры
```
@param options object
{
     url: string - обязательный
     data: object - не обязательный
     errorScript: function(ret) {} - не обязательный - функция вызываемая при {ststus:true}
     success: function(ret) {} - не обязательный - функция вызываемая при {ststus:false}
}
```

## Описание

Упрощает использование AJAX.
По умолчанию тип запроса POST.

по умолчанию формат выводимых данных json в формате
{
     status: bool,
     [data]: {} // не обязательно
}
Если завершено успешно то при вызове
success: function(ret) {
     // ...
}
в `ret` будет значение которая будет в `data`
Если скрипт завершен с ошибкой от скрипта
то есть $.ajax() вернул
```js
{
     status: false,
     data: {
         id: 101,
         data: 'Нет обязательного параметра'
     }
}
```
то будет вызвана функция
```js
options.errorScript(ret) {
     // ...
}
```
и в `ret` будут данные `<return>.data`

@returns {*}
