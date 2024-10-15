# engschool2
# Отчет о выполнении задачи "Онлайн-школа английского языка"

## Постановка задачи
Цель состоит в создании безопасной платформы для проведения онлайн-курсов английского языка, включая защиту данных пользователей, курсов и транзакций.


##Модель угроз

##Определение негативных последствий
- Утечка личных данных: Потеря доверия со стороны обучающихся, возможные юридические последствия и штрафы.
- Недоступность сервиса: Снижение качества обучения, потеря клиентов и финансовые потери.
- Уничтожение данных: Утрата важной информации о студентах и курсах, что затруднит восстановление работы.

##Инвентаризация систем и сетей
- Платформа для онлайн-занятий (например, Яндекс Телемост).
- Веб-сайт школы.
- База данных пользователей (личные данные, результаты обучения).

Сети:
- Локальная сеть (LAN) для сотрудников.
- Внешние сети для доступа студентов.

##Определение источников угроз
Внешние источники:
- Хакеры, использующие различные методы атак (фишинг, DDoS).

Внутренние источники:
- Сотрудники, которые могут случайно или намеренно раскрыть данные.

##Оценка способов реализации угроз
- Фишинг: Использование поддельных писем для получения учетных данных.
- DDoS-атаки: Атаки на серверы с целью их перегрузки.
- Несанкционированный доступ: Использование уязвимостей в системе для доступа к данным.

##Оценка возможности реализации угроз
- Вероятность возникновения: Высокая (особенно для фишинга и DDoS-атак).
- Актуальность угроз: Угрозы актуальны в условиях увеличения числа онлайн-платформ и кибератак.

##Оценка сценариев реализации угроз
- Сценарий 1: Студент получает фишинговое письмо и передает свои учетные данные злоумышленнику. Это приводит к несанкционированному доступу к аккаунтам других студентов.
- Сценарий 2: Хакеры запускают DDoS-атаку на платформу, что делает ее недоступной для всех пользователей на несколько часов.
- Сценарий 3: Сотрудник случайно отправляет конфиденциальные данные третьим лицам через ошибку в электронной почте.

##Заключение
Эта модель угроз позволяет систематически оценить риски и разработать стратегии по защите информации в онлайн-школе английского языка, обеспечивая безопасность данных студентов и преподавателей.









## Цели и Предположения Безопасности (ЦПБ)

### Цели:
- Обеспечение безопасности передачи данных пользователей и курсов
- Предоставление уникальных идентификаторов для каждой сессии и пользователя
- Обеспечение конфиденциальности персональных данных учащихся и преподавателей
- Гарантия целостности данных, транзакций и успешной доставки контента

### Предположения:
- Применение второго фактора для обеспечения безопасности авторизации пользователей
- Использование одноразового пароля (OTP) на основе времени для аутентификации учащихся и преподавателей
- OTP, отправляемый по SMS или предоставляемый через мобильное приложение
- Использование цифровой подписи для проверки авторизованных пользователей при доступе к учебным материалам и сессиям
- Токен запроса-ответа для обеспечения защищенного доступа к видеоматериалам и вебинарам

## Архитектура решения

### Компоненты

| Название                             | Назначение                                                                 |
|--------------------------------------|-----------------------------------------------------------------------------|
| Веб-сервис                           | Реализация бизнес-логики в виде микросервисов для предоставления услуг онлайн-обучения, связанных с сессиями и курсами |
| Мобильное приложение                 | Доступ к курсам, домашним заданиям и личному кабинету через мобильное устройство |
| Модуль безопасности контроля авторизаций | Отдельный микросервис для аутентификации и авторизации пользователей, включая преподавателей и учащихся |
| Центр управления курсами             | Микросервис, отвечающий за управление контентом курсов, сессиями и прогрессом учащихся |

## Алгоритм работы решения

1. Пользователь регистрируется и инициирует сессию через веб-сервис или мобильное приложение.
2. Веб-сервис или мобильное приложение отправляет запрос на авторизацию в модуль безопасности контроля авторизаций.
3. Модуль безопасности контроля авторизаций запрашивает второй фактор аутентификации у пользователя (например, OTP).
4. Пользователь предоставляет второй фактор аутентификации.
5. Модуль безопасности контроля авторизаций проверяет предоставленные данные и, в случае успеха, генерирует уникальный токен для текущей сессии.
6. Веб-сервис или мобильное приложение направляет запрос на доступ к сессии в центр управления курсами, включая уникальный токен.
7. Центр управления курсами проверяет токен у модуля безопасности контроля авторизаций.
8. При успешной проверке токена центр управления курсами предоставляет доступ к сессии или курсу.
9. Веб-сервис или мобильное приложение информирует пользователя об успешной авторизации и предоставляет доступ к контенту.

## Безопасность

### Выполнение целей безопасности:

1. **Обеспечение безопасности передачи данных пользователей и курсов**
   - Использование протокола HTTPS для шифрования всех коммуникаций между компонентами системы.
   - Применение современных алгоритмов шифрования для защиты данных пользователей.

2. **Предоставление уникальных данных для каждой сессии**
   - Генерация уникального токена для каждой сессии модулем безопасности контроля авторизаций.
   - Использование временных меток и случайных чисел для обеспечения уникальности токенов.

3. **Обеспечение конфиденциальности данных**
   - Хранение персональных данных в зашифрованном виде.
   - Применение принципа минимальных привилегий для доступа к данным.
   - Использование токенизации для защиты данных курсов и материалов.

4. **Целостность данных и успешная доставка**
   - Использование цифровых подписей для обеспечения целостности данных курсов.
   - Реализация механизма подтверждения и сверки данных при доступе к учебным материалам.
   - Внедрение системы мониторинга и логирования для отслеживания статуса курсов и прогресса учащихся.

## Негативные сценарии и защита от них

- **Негативный сценарий:** Перехват данных при передаче
  - Защита от перехвата данных с помощью современных криптографических протоколов, HSTS и Certificate Pinning.

- **Негативный сценарий:** Нарушение целостности токенов
  - Применение криптографически стойких методов генерации токенов и ограничение времени их использования.

- **Негативный сценарий:** Компрометация мобильного приложения или веб-сервиса
  - Регулярное обновление и защита от вредоносного ПО, а также шифрование локальных данных.

## Тестирование

1. **Функциональное тестирование**
   - Проверка доступа к курсам при правильных учетных данных и вторичном факторе.
   - Тестирование уникальности токенов и устойчивости при высокой нагрузке.

2. **Тестирование безопасности**
   - Проведение тестов на проникновение, сканирование уязвимостей, и анализ безопасности компонентов.

3. **Нагрузочное тестирование**
   - Симуляция нагрузки на систему и проверка устойчивости к DDoS-атакам.

4. **Тестирование отказоустойчивости**
   - Проверка работоспособности системы при отказе одного из компонентов и восстановление после сбоев.

## Заключение
Предложенная архитектура решения учитывает безопасность данных учащихся и преподавателей, а также обеспечивает надежный доступ к курсам. Микросервисная архитектура поддерживает масштабируемость системы и безопасность критически важных компонентов. Регулярное тестирование и мониторинг позволяют своевременно выявлять и устранять уязвимости.

**Рекомендации для повышения безопасности:**
- Рассмотреть возможность внедрения машинного обучения для выявления аномального поведения.
- Использование блокчейна для повышения прозрачности и надежности данных о курсах и успеваемости учащихся.

## Источники

