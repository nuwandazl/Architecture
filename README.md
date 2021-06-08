# Архитектура информационной системы Google
Google – это поисковая система с дополнительными инструментами и сервисами. 

## Платформа
* Linux
* Большое разнообразие языков программирования: Python, Java, C++

## Статистика
* На 2021 год Google оценивается в 1,000,000 выделенных серверов, что превышает долю в 2% от всех серверов в мире.
* За 2020 год проиндексировано более 10 миллиардов страниц.
* На момент написания оригинала Google включает в себя более 200 GFS кластеров. Один кластер может состоять из 1000 или даже 5000 компьютеров
* Десятки и сотни тысяч компьютеров получают данные из GFS кластеров, которые насчитывают более 5 петабайт дискового пространства. Суммарные пропускная способность операций записи и чтения между дата центрами может достигать 40 гигабайт в секунду
* BigTable позволяет хранить миллиарды ссылок (URL), сотни терабайт снимков со спутников, а также настройки миллионов пользователей

## Стек
Google визуализирует свою инфраструктуру в виде трехслойного стека:
* Продукты: поиск, реклама, электронная почта, карты, видео, чат, блоги
* Распределенная инфраструктура системы:GFS, MapReduce и BigTable
* Вычислительные платформы: множество компьютеров во множестве датацентров
* Легкое развертывание для компании при низком уровне издержек
* Больше денег вкладывается в оборудование для исключения возможности потерь данных

## Надежное хранение данных с помощью GFS
* Надежное масштабируемое хранение данных крайне необходимо для любого приложения. GFS является основой их платформы хранения информации
* GFS - большая распределенная файловая система, способная хранить и обрабатывать огромные объемы информации
* Зачем строить что-либо самим вместо того, чтобы просто взять это с полки? Они контролируют абсолютно всю систему и именно эта платформа отличает их от всех остальных.

Она представляет собой:
* высокую надежность дата центров
* масштабируемость до тысяч сетевых узлов – высокую пропускную способность операций чтения и записи
* поддержку больших блоков данных, размер которых может измеряться в гигабайтах
* эффективное распределение операций между датацентрами для избежания возникновения "узких мест" в системе
В системе существуют мастер-сервера и сервера, собственно хранящие информацию:
* Мастер-сервера хранят метаданные для всех файлов. Сами данные хранятся блоками по 64 мегабайта на остальных серверах. Клиенты могут выполнять операции с метаданными на мастер-серверах, чтобы узнать на каком именно сервере расположены необходимые данные.
* Для обеспечения надежности один и тот же блок данных хранится в трех экземплярах на разных серверах, что обеспечивает избыточность на случай сбоев в работе какого-либо сервера.
* Новые приложения могут пользоваться как существующими кластерами, так и новыми, созданными специально для них.
* Ключ успеха заключается в том, чтобы быть уверенными в том, что у людей есть достаточно вариантов выбора для реализации их приложений. GFS может быть настроена для удовлетворения нужд любого конкретного приложения.

## 
