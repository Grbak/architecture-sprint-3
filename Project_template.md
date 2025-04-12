# Project_template

# Задание 1. Анализ и планирование

### 1. Описание функциональности монолитного приложения

**Управление отоплением:**

Пользователи могут удалённо включать и выключать отопление в своих домах, а также устанавливать целевую температуру для каждого
подключенного устройства.

**Мониторинг температуры:**

Пользователи могут просматривать текущую температуру в своих домах через веб-интерфейс.

### 2. Анализ архитектуры монолитного приложения

- **Язык программирования**: Java
- **База данных**: PostgreSQL
- **Архитектура**: Монолитная, все компоненты системы (обработка запросов, бизнес-логика, работа с данными) находятся в рамках одного приложения.
- **Взаимодействие**: Синхронное, запросы обрабатываются последовательно.
- **Масштабируемость**: Ограничена, так как монолит сложно масштабировать по частям.
- **Развёртывание**: Требует остановки всего приложения.

### 3. Определение доменов и границы контекстов

- Домен: Управление устройствами
  - Поддомен: Управление отоплением
    - Контекст: Включение и отключение устройств
    - Контекст: Установка целевой температуры
    - Контекст: Ведение журналирования
  - Поддомен: Мониторинг температуры
    - Контекст: Сбор измерений с устройств
    - Контекст: Визуализация собранных измерений
- Домен: Управление установкой устройств
  - Поддомен: Обработка клиентских заявок
    - Контекст: Согласование с клиентом даты и времени установки
    - Контекст: Назначение заявок на технических специалистов
  - Поддомен: Настройка устройств
    - Контекст: Регистрация установленных устройств в системе

### 4. Проблемы монолитного решения

- Невозможность независимого масштабирования отдельных сервисов увеличивает риск возникновения проблем при скором увеличении количества пользователей и подключенных устройств;
- Сложность реализации горизонтального масштабирования монолита повышает риск в ближайшем будущем упереться в потолок при вертикальном масштабировании;
- Отсутствие асинхронных взаимодействий в системе увеличивает время ожидания ответа от сервера при управлении отоплением через веб-интерфейс, и по мере роста числа пользователей эта проблема будет становиться все более и более критичной;
- По мере разрастания кодовой базы в процессе внедрения нового функционала новые разработчики будут тратить все больше и больше времени на погружение в проект, что
  замедлит темпы разработки.

### 5. Визуализация контекста системы — диаграмма С4

[![](https://img.plantuml.biz/plantuml/svg/VPDDRzim38Rl_XMSJndGrPUUTcgG3kY0jWYo5JqMYiquGYrH4wcc_VUZP3lzGdkYBP4lNpwqprbCbEI6gX8h0yATYUwI4YEio0i-2LnOqqVZD8422C6MHCX1PoEsOibNrJVhso5rcE80Uv70FvicciDfRsMVjgeLswpbvRGbrsniQs97DnO33itgxCTwC5vkhwyQPrWmwj7zYbmWdoj2yRR6oEGNMUe4wbiDjSObv0EW7SWUWP-rsjNVgp_bON6SP7pN_9VPngEiyVTO2SvuqrlVmnwDv6Xy1o7Ie-toM-x5SD2PGBC3HYCf8ZWqhD6fMTRcazC3nGVrMj-LMCnwqAg1dX4X8kjuRBSAV4SHEdoqBO9Isja-gR1YVT4odRF-f5xcO5dqccP5y_hi22A5G56ozHQPP-_QzLz25lwgvGJl_jUJBCOKRNHH7aRYKrt1mEYPb4dcj5p_BhepkmApKCcg6np6vNrSoXMQwBaOVuqrQuuQF6kgKDPvBp7PhA_VPXU57dNSBxQLzQPLpJAhYGZEzoF-UQ5B1TfxRQD_Wdd3TKelOquhsyp4FwDzZhxJ3_m_)](https://editor.plantuml.com/uml/VPDDRzim38Rl_XMSJndGrPUUTcgG3kY0jWYo5JqMYiquGYrH4wcc_VUZP3lzGdkYBP4lNpwqprbCbEI6gX8h0yATYUwI4YEio0i-2LnOqqVZD8422C6MHCX1PoEsOibNrJVhso5rcE80Uv70FvicciDfRsMVjgeLswpbvRGbrsniQs97DnO33itgxCTwC5vkhwyQPrWmwj7zYbmWdoj2yRR6oEGNMUe4wbiDjSObv0EW7SWUWP-rsjNVgp_bON6SP7pN_9VPngEiyVTO2SvuqrlVmnwDv6Xy1o7Ie-toM-x5SD2PGBC3HYCf8ZWqhD6fMTRcazC3nGVrMj-LMCnwqAg1dX4X8kjuRBSAV4SHEdoqBO9Isja-gR1YVT4odRF-f5xcO5dqccP5y_hi22A5G56ozHQPP-_QzLz25lwgvGJl_jUJBCOKRNHH7aRYKrt1mEYPb4dcj5p_BhepkmApKCcg6np6vNrSoXMQwBaOVuqrQuuQF6kgKDPvBp7PhA_VPXU57dNSBxQLzQPLpJAhYGZEzoF-UQ5B1TfxRQD_Wdd3TKelOquhsyp4FwDzZhxJ3_m_)

Если схема не прогрузилась, ее можно найти [тут](https://editor.plantuml.com/uml/VPDDRzim38Rl_XMSJndGrPUUTcgG3kY0jWYo5JqMYiquGYrH4wcc_VUZP3lzGdkYBP4lNpwqprbCbEI6gX8h0yATYUwI4YEio0i-2LnOqqVZD8422C6MHCX1PoEsOibNrJVhso5rcE80Uv70FvicciDfRsMVjgeLswpbvRGbrsniQs97DnO33itgxCTwC5vkhwyQPrWmwj7zYbmWdoj2yRR6oEGNMUe4wbiDjSObv0EW7SWUWP-rsjNVgp_bON6SP7pN_9VPngEiyVTO2SvuqrlVmnwDv6Xy1o7Ie-toM-x5SD2PGBC3HYCf8ZWqhD6fMTRcazC3nGVrMj-LMCnwqAg1dX4X8kjuRBSAV4SHEdoqBO9Isja-gR1YVT4odRF-f5xcO5dqccP5y_hi22A5G56ozHQPP-_QzLz25lwgvGJl_jUJBCOKRNHH7aRYKrt1mEYPb4dcj5p_BhepkmApKCcg6np6vNrSoXMQwBaOVuqrQuuQF6kgKDPvBp7PhA_VPXU57dNSBxQLzQPLpJAhYGZEzoF-UQ5B1TfxRQD_Wdd3TKelOquhsyp4FwDzZhxJ3_m_) или в соответствующем фолдере в корне проекта.

# Задание 2. Проектирование микросервисной архитектуры

В этом задании вам нужно предоставить только диаграммы в модели C4. Мы не просим вас отдельно описывать получившиеся микросервисы и то, как вы определили взаимодействия между компонентами To-Be системы. Если вы правильно подготовите диаграммы C4, они и так это покажут.

**Диаграмма контейнеров (Containers)**

Добавьте диаграмму.

**Диаграмма компонентов (Components)**

Добавьте диаграмму для каждого из выделенных микросервисов.

**Диаграмма кода (Code)**

Добавьте одну диаграмму или несколько.

# Задание 3. Разработка ER-диаграммы

Добавьте сюда ER-диаграмму. Она должна отражать ключевые сущности системы, их атрибуты и тип связей между ними.

Четвёртое задание — дополнительное. Его можно сделать по желанию. Чтобы ревьюер быстрее проверил ваше решение, укажите, сделали вы это задание или нет. Для этого оставьте нужный эмодзи около заголовка задания:

# ❌ Задание 4. Создание и документирование API
