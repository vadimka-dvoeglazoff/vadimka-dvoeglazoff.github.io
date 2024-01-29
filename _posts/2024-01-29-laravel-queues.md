---
layout: post
title: Laravel Queues/Jobs (Очереди)
Tegs: [Laravel]
comments: false
Author: Вадим Двоеглазов
---

Создать миграцию для таблицы **Jobs**: `php artisan queues:table`

Выполнить миграцию: `php artisan migrate`

Создать задачу для очереди, к примеру, с названием SendNotificationAllUsersJob: `php artisan make:job SendNotificationAllUsersJob`
