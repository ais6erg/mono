# Monoweb
[![Build Status](https://cloud.drone.io/api/badges/PaulAnnekov/monoweb/status.svg)](https://cloud.drone.io/PaulAnnekov/monoweb)

Неофициальный веб-интерфейс для популярного в Украине мобильного банка [monobank](https://www.monobank.ua/).

![Превью](https://user-images.githubusercontent.com/1203892/60048747-8419e200-96d5-11e9-96ae-c4f31b4715d8.gif)

## Описание

Monoweb реализует маленькую часть функционала monobank: аутентификация, просмотр списка транзакций, списка карт и
информации о пользователе.

Приложение создавалось исключительно в исследовательских целях. Работает в read-only режиме, т.е. не позволяет изменять состояние банковского счёта. Планов добавлять функционал создания платежей нет.
Приложение использует неофициальный API. Может работать нестабильно при получении неожиданных ответов. Рекомендую использовать [официальный API](https://api.monobank.ua/docs/).

## Заметки

### Одна сессия

monobank разрешает только одну одновременную сессию. Как только вы аутентифицируетесь на другом устройстве сессия на текущем устройстве оборвётся. Вам придётся с нуля проходить процесс аутентификации (телефон - SMS код - пин). Это не проблема, но доставляет некоторый дискомфорт, да.

### Множественные запросы SMS кода

Множественные запросы SMS кода в течении короткого промежутка времени, допустим, вход то на смартфоне, то на ПК, в какой-то момент приведут к тому, что коды перестанут приходить. Никакой ошибки вы не увидите. Через несколько часов можно запросить SMS код ещё раз и он должен прийти. Это похоже на какой-то внутренний механизм защиты от подозрительной активности.

### CORS

Так как monobank не предоставляет своего веб-интерфейса, то и [CORS заголовки](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS) они не передают. Это исключает возможность напрямую делать запросы к их API из браузера. Данный веб-интерфейс использует [CORS proxy](https://github.com/PaulAnnekov/mighty-lambda-proxy), единственной задачей которого является добавление CORS заголовков в ответ от API.

## Как запустить локально

- `git clone https://github.com/PaulAnnekov/monoweb.git && cd monoweb`
- `cp config.sample.json config.json`
- `npm install`
- `npm start`
- Открываем http://localhost:3000
