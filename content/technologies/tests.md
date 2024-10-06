+++
weight = 6
title = 'Тестирование'
+++

# Тестирование

Тесты - кусочки кода, проверяющие корректную функциональность вашего приложения, или его частей. Один такой кусочек называется тест кейсом, процесс их написания называется покрытием кода приложения тестами.

Тесты бывают различных видов, в зависимости от того, что они тестируют. Рассмотрим основные:
1. Юнит тесты тестируют небольшие части кода, методы или классы. Типичный пример юнит теста - создать объект, вызвать его метод, проверить результат.
2. Интеграционные тесты проверяют, что ваше приложение работает правильно в контексте внешних инструментов и сервисов, например, баз данных. Пример интеграционного теста - вызов метода REST API вашего приложения, проверка корректности результата.
3. E2E (end to end) тесты тестируют приложение в целом, затрагивая максимальное количество его частей. Пример - на веб-интерфейсе приложения есть форма, при заполнении и отправки которой в базе появляется новая запись. E2E тест может сэмулировать действия на веб-интерфейсе, после чего проверить состояние базы данных.

Кроме видов тестов, важно понимать некоторые смежные с тестированием идеи:
- Mocking - техника эмуляции поведения какого-то метода или внешнего сервиса. Например, если метод возвращает какое-то постоянно меняющееся значение (биржевую котировку, например), то в целях предсказуемого теста можно создать мок объект, возвращающий заранее известную котировку, провести с ней некоторые вычисления и проверить результат на корректность.
- Edge case (пограничный случай) - маловероятный, но тем не менее возможный пример входных данных, который может получить тестируемый код. Пример - длина email при регистрации пользователя. Маловероятная, но максимально возможная длина email адреса - 320 символов, и тестируя пограничные случаи мы можем быть уверены, что приложение корректно их обрабатывает.
- Тестовые данные - если код работает с данными, то для его тестирование нужны тестовые данные. Такие данные редко являются данными реальных пользователей (это было бы небезопасно), а их целью зачастую является воссоздание различных пограничных случаев.
- Тестовое окружение - во время тестов редко используется реальные база данных и внешние сервисы, это создавало бы ненужную активность (например, вставку тестовых данных в базу). Поэтому, частая практика - создать отдельное тестовое окружение, которое рождается перед стартом тестов и уничтожается после. Пример - вместо внешней Postgres базы данных, можно запустить in-memory H2 базу и инициализировать её состояние таблицами с тестовыми данными. Другой популярный инструмент - [Testcontainers](https://www.testcontainers.org/), позволяет запускать необходимые для тест кейсов инструменты (базы данных, очереди) в Docker контейнерах.

В работе с тестами, как и везде, есть плюсы и минусы.

Плюсы:
- Написание тестов помогает формализовать работу приложения
- Для написания качественных тестов покрываемый ими код должен быть спроектирован на необходимом уровне. Необходимость тестов может стать поводом для рефакторинга, улучшающего качество кода
- Тесты являются ещё одной формой документации, хочешь понять в деталях, что делает класс - прочитай юнит тесты к нему
- Тесты помогают поддерживать работоспособность кода при его рефакторинге и добавления нового функционала. В случае некорректных изменений часть тестов сломается
- Тесты помогают поддерживать здоровый уровень качества кода приложения, особенно в больших командах, где люди приходят и уходят

Минусы:
- Дополнительная работа. Написание тестов и их поддержка требуют времени
- Плохо написанные тесты создают больше проблем, чем приносят пользы

Практически любой устоявшийся проект содержит тесты, и разработчикам необходимо уметь с ними работать. Уровень проникновения тестов в проект, их глубина и количество зависят от конкретных условий и варьируются от поверхностного тестирования до полного [TDD](https://ru.wikipedia.org/wiki/%D0%A0%D0%B0%D0%B7%D1%80%D0%B0%D0%B1%D0%BE%D1%82%D0%BA%D0%B0_%D1%87%D0%B5%D1%80%D0%B5%D0%B7_%D1%82%D0%B5%D1%81%D1%82%D0%B8%D1%80%D0%BE%D0%B2%D0%B0%D0%BD%D0%B8%D0%B5).

## Unit тестирование

Для написания юнит тестов студент должен уметь писать качественные тест кейсы и пользоваться одной из популярных библиотек для юнит тестирования (unittest, pytest). Важнее всего понять идеи качественных кейсов, применять эти идеи к конкретной библиотеке - дело практики.

Основные рекомендации для написания качественных юнит тестов:
- Проверяйте пограничные случаи
- Тестируйте не только успешные сценарии работы кода, но и неудачные - покрывайте тестами случаи, когда метод должен вернуть ошибку или кинуть exception
- Давайте тест кейсам короткие и понятные имена, описывающие суть их проверки. Если имя слишком длинное или непонятное, возможно, тест слишком общий или сложный

#### Избранные курсы и учебные ресурсы

- [Плейлист](https://www.youtube.com/playlist?list=PLeLN0qH0-mCVdHgdjlnKTl4jKuJgCK-4b) от Артёма Шумейко
- Практика - [проект 4](../projects/tennis-scoreboard.md)

## Интеграционные тесты

Интеграционные тесты проверяют взаимодействия между частями системы (например - между слоем сервисов и слоем хранения данных) и взаимодействия с внешними сервисами. Для написания таких тестов нужно знать и уметь пользоваться следующими идеями и инструментами:
- Библиотека для написания тестов - unittest, pytest
- Моки, как инструмент симуляции поведения классов или внешних сервисов
- Тестовые данные, независимые от основных данных приложения
- [Testcontainers](https://www.testcontainers.org/) - библиотека для запуска экземпляров нужных для тестов инструментов внутри Docker контейнеров

Примеры интеграционного тестирования в контексте бэкенд приложений:
- Взаимодействия класса-сервиса и БД, куда сервис вставляет данные. Можно проверить реакцию БД на вставку некорректных данных и реакцию сервиса на возникшую при этом ошибку
- Взаимодействия класса-сервиса и внешнего REST API. Проверки парсинга ответов, реакции на HTTP ошибки (коды 4xx, 5xx) и сетевые ошибки (таймаут подключения)
- Взаимодействия REST контроллера и сервисов. Проверка того, что REST API вернёт ожидаемые ответы на различные наборы параметров в запросах. Реакции на ошибки - неправильно сформированные запросы, отсутствие необходимой авторизации

#### Избранные курсы и учебные ресурсы

- [Доклад](https://www.youtube.com/watch?v=PEVVvZOt7bY) по TestContainers с конференции Joker
- TODO добавить ресурсов по тестированию в Python
- Практика - проекты 5, 6