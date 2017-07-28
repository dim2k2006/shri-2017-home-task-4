# ШРИ 2017, Домашнее задание 4

## Содержание

- [Задача](#Задача)
- [Решение](#Решение)

## Задача:
Составить список возможных оптимизаций для сайта [https://lifehacker.ru/](https://lifehacker.ru/).

## Решение

### Общие оптимизации:

1. Использовать кеш браузера. Необходимо указать дату и срок действия для статических файлов. В данном случае ресурсы будут загружаться из кеша браузера, а не из интернета. [Google PageSpeed Insights Screenshot](/screenshots/cache.png?raw=true) 

2. Включить сжатие. Для ресурсов с расширением .svg не включено сжатие данных. [Google PageSpeed Insights Screenshot](/screenshots/gzip.png?raw=true)

3. Минификация всех js файлов. [Google PageSpeed Insights Screenshot](/screenshots/jsmin.png?raw=true)

4. Оптимизация изображений. [Google PageSpeed Insights Screenshot](/screenshots/imgmin.png?raw=true)