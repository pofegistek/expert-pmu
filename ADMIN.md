# Admin Guide — Expert PMU

Этот файл — шпаргалка по управлению содержимым Mini App через Telegram-бот.

## Кто может
Только admin с Telegram ID `317647581`.

## Команды

### Мастера
- `/masters` — список всех мастеров. Кнопки: добавить, редактировать, удалить.
- `/addmaster_v2` — пошаговое добавление нового мастера.

### Услуги
- `/services` — список всех услуг. Кнопки: добавить, редактировать, удалить.
- `/addservice_v2` — пошаговое добавление новой услуги.

### Прочее
- `/addworks` — добавить фото работ мастера в галерею.
- `/price` — изменить цену услуги.
- `/masterprice` — изменить цену «от» для мастера.
- `/broadcast` — рассылка всем пользователям.
- `/admin_help` — эта шпаргалка.

## Архитектура (кратко)

Данные о мастерах и услугах хранятся в SQLite (`/root/expertpmu_bot/database.db`) в таблицах `masters_v2`, `services_v2`, `master_services_v2`.

Frontend (`index.html` на GitHub Pages) при загрузке делает запросы к API на VPS:
- `GET https://46.30.43.23.sslip.io:9443/masters-full`
- `GET https://46.30.43.23.sslip.io:9443/services-full`

Все изменения через бота отражаются мгновенно — достаточно закрыть и снова открыть Mini App.

## Если что-то не работает
- Логи бота: `ssh root@46.30.43.23` → `journalctl -u expertpmu-bot -n 100 --no-pager`
- Перезапуск: `systemctl restart expertpmu-bot`
- Проверка API: `curl https://46.30.43.23.sslip.io:9443/masters-full`
- Бэкап БД: `/root/expertpmu_bot/database.db.backup-*`

## API-контракт
См. `/root/expertpmu_bot/API.md` на VPS.
