# Refactor Notes — Load from API

## Что убрано

- Хардкод `var MASTERS = [...]` (16 объектов) из `index.html`
- Хардкод `var SERVICE_MASTERS = {...}` (18 услуг) из `index.html`
- Устаревший блок `/masters` (мержил данные в MASTERS/SERVICE_MASTERS из старого endpoint)
- Переменная `var YCL` (yclients-URL-ы теперь приходят из API)

## Новые endpoints

| Endpoint | Данные |
|---|---|
| `GET /masters-full` | Массив мастеров: id, name, photo, level, levelColor, price, avatarBg, avatarLetter, yclients, tab, services |
| `GET /services-full` | Массив услуг: id, name, masters (список имён) |

Оба endpoint возвращают готовые данные — фронт подставляет напрямую без трансформаций.

Прежние `/prices`, `/static-master-prices`, `/master-works`, `/hidden-masters`, `/settings` — не изменены.

## Как добавлять мастеров и услуги

Через Telegram-бота (Agent 2):
- `/addmaster` — добавить нового мастера
- `/editmaster` — изменить данные мастера
- `/addservice` — добавить новую услугу
- `/editservice` — изменить услугу

После изменения в боте данные сразу отображаются в Mini App при следующей загрузке (без деплоя фронта).

## Фоллбэк

При недоступности API фронт использует кэш из `localStorage` (`cache_masters`, `cache_services`) и показывает toast-уведомление.
