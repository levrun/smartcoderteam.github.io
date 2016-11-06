---
title: "Зачем нужен локальный веб-сервер в случае javascript-приложения?"
excerpt: "ведь мое приложение уже у меня и браузер может его выполнить и так локально"
modified: 2016-11-03T09:55:10-04:00
header:
tags: 
  - javascript
  - local web server
  - tricky questions
---

Очень часто задают вопрос по следующей теме:

> "Зачем нужен локальный веб-сервер? Я всегда открывал мои примеры на javascript _как файл_
через браузер и все работало. Зачем же мне нужны эти дополнительные телодвижения?

Когда вы открываете _index.html_ файл напрямую через ваш браузер то 
он использует файловый протокол:
```
file:///index.html
```

Из-за настроек безопасности некоторые браузеры не позволяют выполнить AJAX-запросы
в этом случае. Это на самом деле хорошая вещь так как некоторые скрипты могут
прочитать любой файл на вашем жестком диске и сделать чтолибо зловредное.

Браузер Сhrome по умолчанию запрещает запросы типа _XMLHttpRequest_
на локальном файле. Эту настройку можно убрать запустив chrome вот так:
```
chrome.exe --disable-web-security
```
Однако теперь вы понимаете, что убирая защиту, становитесь уязвимы для зловредых скриптов.

Подробнее читайте тут [allow-google-chrome-to-use-xmlhttprequest](http://stackoverflow.com/questions/4819060/allow-google-chrome-to-use-xmlhttprequest-to-load-a-url-from-a-local-file) 