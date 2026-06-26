# checker-dist — CDN артефактов RUS-STANDART.XYZ Checker

Собранные файлы для скачивания (**не исходники** — они в монорепо `rstandart-checker`).
Раздаётся nginx с VPS-клона (`/var/www/api_rus_stan_usr/data/checker-pages`), плюс GitHub Pages-резерв.

| Каталог | Что |
|---|---|
| `programs/` | Компоненты: `frontend_vN.enc`, `win_session_vN.zip`, `win_index_vN.zip`, `win_runtime.zip`, `baseline_vN.zip` + сторонние тулзы (Everything, HxD, …) |
| `versions/` | NSIS-установщики по версиям приложения |

## Важно

- **Пути неизменны.** На `/checker/programs/…` и `/checker/versions/…` завязаны nginx, GitHub
  Pages-резерв, `app_mirrors` (БД) и хардкоды живых клиентов 1.2.0.0. Переименовывать/переносить — нельзя.
- **Трассировка к исходнику** — по имени: артефакт `<comp>_vN` ↔ git-тег `<comp>-vN` в монорепо
  `rstandart-checker` (`git checkout <comp>-vN`). Отдельного манифеста нет — имя и есть ссылка.
- **Синхронизация с VPS** — после `git push` сюда обязательно:
  `ssh checker-vps "cd /var/www/api_rus_stan_usr/data/checker-pages && git pull"`.
  Содержимое этого репо и VPS-клона обязано совпадать (nginx раздаёт прямо с диска клона).

## Добавить/обновить компонент

1. Бамп версии в монорепо (`git tag <comp>-v<N+1>`), сборка артефакта.
2. Положить `<comp>_v<N+1>.<ext>` в `programs/` → `git push` → `git pull` на VPS.
3. Обновить серверный маппинг (`component_releases`/`frontend_releases`/`app_programs`) при необходимости.
