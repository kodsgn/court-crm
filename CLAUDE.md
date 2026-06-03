# cashtime CRM — контекст для агента

## Проект
Single-file CRM для відстеження судових справ. Весь код — один файл `index.html`. Немає фреймворків, збірки, npm.

**Сайт:** https://kodsgn.github.io/court-crm/ (пароль — у власника репо)  
**Репо:** https://github.com/kodsgn/court-crm  
**Власник:** kodsgn (Anton)

## Правила які НЕ можна порушувати

- Назва скрізь — **судові справи** (не КешТайм, не cashtime CRM)
- **Браузерні нотифікації видалені** — не повертати. Нагадування тільки через Telegram-бота
- Функції `requestNotifications`, `scheduleNotifications`, `new Notification(...)` — не додавати
- CSS клас `.notif-bar` — не додавати
- **НЕ мінімізувати файл** — index.html має залишатись читабельним
- **НЕ робити force push** і не перезаписувати чужі зміни — завжди `git pull` перед роботою

## Workflow для змін

```bash
git pull                  # ЗАВЖДИ перед початком роботи
# редагуй index.html
git add index.html
git commit -m "опис змін"
git push                  # сайт оновиться автоматично за ~1 хв
```

**Важливо:** завжди робити `git pull` перед тим як починати редагувати. Інакше затреш чужі зміни.

## Архітектура

- Дані зберігаються в `localStorage` браузера
- Синхронізація з Google Sheets через Apps Script (кнопка "📊 Google Sheets" у navbar)
- Telegram-нагадування: GitHub Actions cron щоранку о 08:00 → `.github/workflows/notify.yml`
- Деплой: GitHub Actions при кожному push → Staticrypt шифрує HTML → GitHub Pages

## GitHub Secrets (не чіпати)

- `SITE_PASSWORD` — пароль сайту
- `TELEGRAM_BOT_TOKEN` — токен бота
- `TELEGRAM_CHAT_ID` — ID групи "CRM updates"
- `GS_SCRIPT_URL` — URL Apps Script для читання Google Sheets
