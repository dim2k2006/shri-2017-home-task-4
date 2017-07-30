# ШРИ 2017, Домашнее задание 4

## Содержание

- [Задача](#Задача)
- [Решение](#Решение)

## Задача:
Составить список возможных оптимизаций для сайта [https://lifehacker.ru/](https://lifehacker.ru/).

## Решение

### Общие оптимизации:

1. Использовать кеш браузера. Необходимо указать дату и срок действия для статических файлов. В данном случае ресурсы будут загружаться из кеша браузера, а не из интернета. [Google page speed insights screenshot](/screenshots/cache.png?raw=true) 

2. Включить сжатие. Для ресурсов с расширением .svg не включено сжатие данных. [Google page speed insights screenshot](/screenshots/gzip.png?raw=true)

3. Минификация всех js файлов. [Google page speed insights screenshot](/screenshots/jsmin.png?raw=true)

4. Оптимизация изображений. [Google page speed insights screenshot](/screenshots/imgmin.png?raw=true)

5. Данный ресурс использует большое количество внешних файлов которые блокируют отображение контента. Необходимо загружать их в конце документа. Для js файлов необходимо добавить атрибуты async или defer для асинхронной загрузки.

6. Использование субдоменов для ускорения загрузки статических файлов. [Dev tools audits screenshot](/screenshots/host.png?raw=true)

7. Конкатенация css файлов. Данный ресурс использует 16 внешних ccs файлов. Для увеличения скорости загрузки необходимо сократить это число. [Dev tools audits screenshot](/screenshots/cssconcat.png?raw=true)

8. Конкатенация js файлов. [Dev tools audits screenshot](/screenshots/jsconcat.png?raw=true)

9. Загружать статические файлы с доменов у которых отключены cookie. [Dev tools audits screenshot](/screenshots/cookie.png?raw=true)

10. Удалить неиспользуемый код в html, css, js файлах.

11. На сайте присутствуют большие списки с контентом [Google chrome browser screenshot](/screenshots/content.png?raw=true). При ховере на элемент такого спииска, к нему применяются дополнительные css свойства. Существует следующая проблема: при скролле страницы с таким контентом, постоянно срабатывает ховер у элементов над которыми расположен курсор. Данный эффект значительно снижает производительность страница и приводит к резкому снижению количества кадров в секунду (fps). В качетве решенеия данной проблемы существуют прием согласно которому когда появляется событие scroll, необходимо на контейнер добавить css свойство pointer-events в значении none. По окончании скрола необходмо удалить данное css свойство. [60fps scrolling using pointer-events: none](https://www.thecssninja.com/css/pointer-events-60fps)

12. При отключенном js, главная навигационная панель - невидимая. [Google chrome browser js disable screenshot](/screenshots/navigationjsdisable.png?raw=true) [Google chrome browser js enable screenshot](/screenshots/navigationjsenable.png?raw=true). 