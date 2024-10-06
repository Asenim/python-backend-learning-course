+++
title = 'Виселица'
weight = 1
+++

# Проект "Виселица"

Задача - реализовать игру "виселица". Интерфейс - консольный. Описание правил игры на [Википедии](https://ru.wikipedia.org/wiki/%D0%92%D0%B8%D1%81%D0%B5%D0%BB%D0%B8%D1%86%D0%B0_(%D0%B8%D0%B3%D1%80%D0%B0)).

Комментарии по проекту - [https://www.youtube.com/watch?v=kqLklwFjr5g](https://www.youtube.com/watch?v=kqLklwFjr5g) (видео записано для Java версии роадмапа).

## Что нужно знать

- [Python](../technologies/python.md) - базовый синтаксис

## Мотивация проекта

Проект является разминочным, и его основная цель - проверить себя на то, что от теории и решения задач уже можно переходить к реализации цельных проектов. Если приложения подобного уровня вы уже реализовывали без возникновения трудностей, проект можно пропустить.

## Функционал приложения и меню консольного интерфейса

1. При старте, приложение предлагает начать новую игру или выйти из приложения
2. При начале новой игры, случайным образом загадывается слово, и игрок начинает процесс по его отгадыванию
3. После каждой введенной буквы выводим в консоль счётчик ошибок, текущее состояние виселицы (нарисованное ASCII символами)
4. По завершении игры выводим результат (победа или поражение) и возвращаемся к состоянию #1 - предложение начать новую игру или выйти из приложения

## Заметки по реализации

Если у вас уже есть опыт в ООП, предлагаю написать этот проект в ООП-стиле, разбив всю логику на части и реализовав их в нескольких классах.

Если такого опыта нет, можно реализовать всё в процедурном стиле.

## План работы над приложением

- Найти в интернете словарь существительных в именительным падеже, отбросить из него слишком короткие слова. Этот словарь будет источником для выбора случайного загаданного слова для каждого раунда игры
- Реализовать игровой цикл отгадывания букв и отображения текущего состояния виселицы
- Реализовать цикл по перезапуску игры после победы/поражения

## Ресурсы для работы над ошибками

- Эталонная [реализация проекта](https://github.com/zhukovsd/tic-tac-toe) похожего уровня сложности, написанного на [стриме](https://www.youtube.com/watch?v=PPikj1qHxrA)
- [Реализации проекта](../finished-projects.md#виселица) другими студентами и мои ревью этих реализаций 
- Чеклист для самопроверки с типовыми ошибками (в конце страницы)
- Готовый проект можете отправить мне на ревью - [https://t.me/zhukovsd](https://t.me/zhukovsd)
  - **[Обновление от 7 сентября 2023]** - целевое количество видео и текстовых ревью проекта "Виселица" накоплено, новые реализации к ревью не принимаются. В любом случае призываю отправлять законченные проекты в [чат](https://t.me/zhukovsd_it_chat), добавляю их в [список](../finished-projects.md#виселица). Подробности - [https://t.me/zhukovsd_it_mentor/57](https://t.me/zhukovsd_it_mentor/57) 

## Чеклист для самопроверки

❗️**Спойлеры**: советую не читать этот список до того момента, пока не допишете первую самостоятельную работающую версию проекта❗️

Функциональные проблемы:
- Отсутствие валидации вводимых символов (валидными могут считаться, например, только маленькие буквы кириллицы). Невалидный ввод не должен увеличивать счётчик ошибок пользоваться в игровом раунде
- Повторно вводимый символ, отсутствующий в секретном слове, не должен считаться за ошибку

Код:
- Абсолютный путь к файлу со словарем слов
- Недостаточная разбивка кода на функции. Одна функция должна отвечать за одну задачу, например, открывать отгаданную букву в маске загаданного слова
- Излишнее использование "глобальных" переменных
- Неоднозначное именование полей, переменных, методов. Несовпадение имён смысловой нагрузке
- Использование рекурсии для запусков второго и последующих игровых раундов

Мелочи:
- Неаккуратное форматирование кода