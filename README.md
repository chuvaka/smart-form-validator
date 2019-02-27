# Smart-Form-Validator: Плагин для валидации форм

## Для чего?

Плагин предназначен для подключения валидации к любой форме в одну строчку.

Плагин содержит в себе большое количество для настройки классов для активных элементов и ошибок. Для отображения применена тема на основе material design.

## Подключение

```html
<script src="classie.js"></script>
<script src="smart.form.validator.min.js"></script>
```

Скрипт **classie.js** используется для упрощения работы с классами у элементов.

_В текущей реализации скрипт **classie.js** импортирован в плагин и не требует дополнительного подключения._

## Установка

```js
var smartForm = new SmartFormValidator('#js-smart-form');
```
Селектор может быть как id так и класс.

## Дополнительные настройки

Для дополнительных настроек, вторым параметром применяется объект со свойствами

```js
{
    selectorFormLabels:   '.form__label', // класс для лейбла
    selectorFormControls: '.form__control', // класс для элементов, которые будут валидироваться
    selectorErrorDiv:     '.form__error', // div, куда будет выводить сообщение об ошибки
    selectorSubmitBtn:    '.js-form-submit', // кнопка, которая будет блокироваться, если форма не валидна
    classNameActive:      'form__item_active', // класс для родительского div, означающий что элемент активен (есть значение в инпуте)
    classNameFocused:     'form__item_focused', // класс для родительского div, означающий что элемент в фокусе
    classNameError:       'form__item_error', // класс для родительского div, означающий что элемент с ошибкой
    defaultErrorText:     'необходимо заполнить', // стандартное сообщение об ошибке, если в инпут пустой
    invalidErrorText:     'неверный формат', // стандартное сообщение об ошибке, если в инкут ввели что-то и оно не подходит для регулярки
    displayError: false, // выводить ошибки или нет
    regExp: { // стандартный набор регулярок для инпутов, где ключ означает для какого элемента, связан с аттрибутом инпута data-field
        email: /^(([^<>()[\]\\.,;:\s@\"]+(\.[^<>()[\]\\.,;:\s@\"]+)*)|(\".+\"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/,
        phone: /^(\+7|8)([0-9]{3})([0-9]{3})([0-9]{2})([0-9]{2})$/
    },
    customValidation: {} // здесь можно добавлять свои собственные регулярки и сообщения об ошибке
}
```

## Настройка сustomValidation

Для примера добавим для трех инпутом собственные правила для обработки на ошибки.

В **empty** указывается сообщение в **errorText** если инпут пустой

В **invalid** указывается аналогии сообщение об ошибки, а в **regExp** регулярку, по которой будет проверяться

```js
{
    name: {
        empty: {
            errorText: 'необходимо заполнить поле Наименование'
        },
    },
    phone: {
        empty: {
            errorText: 'необходимо заполнить по Телефон'
        },
        invalid: {
            regExp: /^(\+7|8)([0-9]{3})([0-9]{3})([0-9]{2})([0-9]{2})$/,
            errorText: 'неверно введё номер телефона'
        }
    },
    email: {
        empty: {
            errorText: 'необходимо заполнить поле Еmail'
        },
        invalid: {
            errorText: 'не сможем отправить письмо по этому адресу. email должен быть следующего формата, например, mymail@mailbox.ru'
        }
    }
}
```

Если нет какого-то из свойств при обработке, то будут браться дефолтные значения из настроек плагина.