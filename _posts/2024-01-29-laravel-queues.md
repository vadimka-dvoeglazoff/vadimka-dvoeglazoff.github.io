---
layout: post
title: Laravel Queues/Jobs (Очереди)
tags: [Laravel]
comments: false
author: Вадим Двоеглазов
---

Для выполнения длительных операций в Laravel можно воспользоваться механизмом очередей. Миграции таблицы **Jobs**, для записи заданий на выполнения, по умолчанию нет в Laravel.
Чтобы создать миграцию необходимо выпонить в терминале команду: `php artisan queues:table`

Для создания таблицы в БД необходимо выполнить миграцию, команда: `php artisan migrate`

Далее создаем сами задачи и переносим в них код выполнения длительных операций, к примеру, с названием SendNotificationAllUsersJob, для рассылки уведомлений всем пользователям ресурса: `php artisan make:job SendNotificationAllUsersJob`
