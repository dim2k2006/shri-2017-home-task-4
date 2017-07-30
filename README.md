# ШРИ 2017, Домашнее задание 4

## Содержание

- [Задача](#Задача)
- [Решение](#Решение)

## Задача:
Составить список возможных оптимизаций для сайта [https://lifehacker.ru/](https://lifehacker.ru/).

## Решение

### Общие оптимизации:

1. Использовать кеш браузера. Необходимо указать дату и срок действия для статических файлов. В данном случае ресурсы будут загружаться из кеша браузера, а не из интернета ([Скриншот: google page speed insights](/screenshots/cache.png?raw=true)). 

2. Включить сжатие. Для ресурсов с расширением .svg не включено сжатие данных ([Скриншот: google page speed insights](/screenshots/gzip.png?raw=true)).

3. Минификация всех js файлов ([Скриншот: google page speed insights](/screenshots/jsmin.png?raw=true)).

4. Оптимизация изображений ([Скриншот: google page speed insights](/screenshots/imgmin.png?raw=true)).

5. Данный ресурс использует большое количество внешних файлов которые блокируют отображение контента. Необходимо загружать их в конце документа. Для js файлов необходимо добавить атрибуты async или defer для асинхронной загрузки.

6. Использование субдоменов для ускорения загрузки статических файлов ([Скриншот: dev tools audits](/screenshots/host.png?raw=true)).

7. Конкатенация css файлов. Данный ресурс использует 16 внешних css файлов. Для увеличения скорости загрузки необходимо сократить это число ([Скриншот: dev tools audits](/screenshots/cssconcat.png?raw=true)).

8. Конкатенация js файлов ([Скриншот: dev tools audits](/screenshots/jsconcat.png?raw=true)).

9. Загружать статические файлы с доменов у которых отключены cookie ([Скриншот: dev tools audits](/screenshots/cookie.png?raw=true)).

10. Удалить неиспользуемый код в html, css, js файлах.

11. На сайте присутствуют большие списки с контентом ([Скриншот: google chrome browser](/screenshots/content.png?raw=true)). При ховере на элемент такого спииска, к нему применяются дополнительные css свойства. Существует следующая проблема: при скролле страницы с таким контентом, постоянно срабатывает ховер у элементов над которыми расположен курсор. Данный эффект значительно снижает производительность страница и приводит к резкому снижению количества кадров в секунду (fps). В качестве решения данной проблемы можно использовать прием согласно которому при появлении события scroll, необходимо к контейнеру добавить css свойство pointer-events в значении none. По окончании скрола необходмо удалить данное css свойство ([Статья: 60fps scrolling using pointer-events: none](https://www.thecssninja.com/css/pointer-events-60fps)).

12. При отключенном js, главная навигационная панель - невидимая ([Google chrome browser js disable screenshot](/screenshots/navigationjsdisable.png?raw=true), [Google chrome browser js enable screenshot](/screenshots/navigationjsenable.png?raw=true)). 

13. При анализировании перерисовок главной страницы было выявлено, что при скроле происходит постоянная перерисовка иконки уведомлений ([Google chrome browser screenshot](/screenshots/repaint.png?raw=true)). Для решения данной проблемы можно применить «нулевой хак» ([Repaint problem video](https://drive.google.com/open?id=0B4DR2fff2kdWYlQ4RFd6T3dRQ2s), [Repaint fix video](https://drive.google.com/open?id=0B4DR2fff2kdWYnBZU0k5YmVaeE0)). 

### Оптимизации для мобильных устройств:

1. Оптимизация загрузки видимого контента ([Google page speed insights screenshot](/screenshots/visiblecontent.png?raw=true)). Для того, чтобы страница загружалась быстрее необходимо сократить размер данных необходимых для показа основого контента страницы ([Google page speed insights recommendations](https://developers.google.com/speed/docs/insights/PrioritizeVisibleContent)). Сюда же можно отнести прием инлайна css стилей и создания так называемого «Critical CSS» ([Understanding Critical CSS](https://www.smashingmagazine.com/2015/08/understanding-critical-css/)).

2. Шрифты. На сайте используется google шрифт - Roboto, который подключен через тэг link. В качестве оптимизации можно предложить использование метода FontFaceOnload. При данном подходе для первого захода на ресурс - показываем стандартный шрифт. После загрузки шрифта в cookie делается метка. При последующих посещениях с нужной нам cookie - в разметку добавляется класс отвечающий за использование каcтомных шрифтов.

3. Настроить порядок загрузки скриптов ([Браузеры с поддержкой defer screenshot](/screenshots/withdefer.png?raw=true), [iOS](/screenshots/ios.png?raw=true), [Браузеры без поддержки defer](/screenshots/withoutdefer.png?raw=true)).

4. На сайте используются иконочные шрифты. На медленном интернете пока не загрузится иконочный шрифт - пользователь не увидит ни одной иконки ([Google chrome browser screenshot](/screenshots/icon.png?raw=true)). Для таких целей вместо иконочных шрифтов лучше использовать векторную графику.

5. На iOS есть баг прокрутки при открытой мобильной навигации. Если пользователь начинает скролить страницу, то нижняя системная панелька скрывается и при открытой мобильной навигации на ее месте образуется прозрачная область, до тех пор пока браузер не выполнит перерисовку ([iOS scroll problem video](https://drive.google.com/open?id=0B4DR2fff2kdWNU1yc1U2SzhnR28)). В качестве одного из возможных вариантов решения данной проблемы можно предложить обернуть всю страницу в абсолютно спозиционированный контейнер со 100% высотой. В таком случае страница будет скролится внутри данного контейнера, а не внутри браузера, что позволит избежать данной проблемы.