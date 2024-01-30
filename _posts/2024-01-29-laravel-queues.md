---
layout: post
title: Laravel Queues/Jobs (Очереди)
tags: [Laravel]
comments: true
author: Вадим Двоеглазов
---

Для выполнения длительных операций в Laravel можно воспользоваться [механизмом очередей](https://laravel.com/docs/10.x/queues). Для реализации механизма очередей понадобится:

- Миграция для создания **jobs** таблицы
- Миграция для создания **failed_jobs** таблицы
- Класс задания

По умолчания миграции для создания **jobs** таблицы нет в Laravel.
Чтобы создать миграцию необходимо выполнить в терминале команду:

`php artisan queue:table`

Миграция для создания **failed_jobs** таблицы обычно уже присутствует в новых приложениях Laravel. Однако, если приложение не содержит миграцию для этой таблицы, для создания можно использовать команду:

`php artisan queue:failed-table`

Для создания таблиц **jobs** и **failed_jobs** в БД необходимо выполнить миграцию, команда:

`php artisan migrate`

Также не забываем указать своему приложению использовать database драйвер, обновив QUEUE_CONNECTION переменную в .env файле приложения:

`QUEUE_CONNECTION=database`

Далее [генерируем класс задания](https://laravel.com/docs/10.x/queues#generating-job-classes), к примеру, SendNotificationAllUsersJob, который будет выполняться асинхронно. Для генерации используем команду:

`php artisan make:job SendNotificationAllUsersJob`

[Запустить рабочий процесс](https://laravel.com/docs/10.x/queues#running-the-queue-worker) можно с помощью команды:

`php artisan queue:work`

Рабочий процесс будет выполняться до тех пор, пока не будет остановлен вручную или вы не закроете свой терминал. Чтобы queue:work процесс постоянно выполнялся в фоновом режиме, необходимо использовать монитор процесса, такой как [Supervisor](https://laravel.com/docs/10.x/queues#supervisor-configuration), чтобы гарантировать, что рабочий процесс очереди не прекратит свою работу.

Если задача не может быть выполнена из-за какой-либо ошибки, такая задача перемещается из таблицы **jobs** в таблицу **failed_jobs**. Посмотреть [такие задачи](https://laravel.com/docs/10.x/queues#dealing-with-failed-jobs) можно выполнив команду:

`php artisan queue:failed`

Для повторного запуска задач из таблицы **failed_jobs** необходимо выполнить команду:

`php artisan queue:retry ID`, где ID - идентификатор задачи в таблице **failed_jobs**

или

`php artisan queue:retry all`, где **all** означает попытку повторного запуска всех задач из таблицы **failed_jobs**
