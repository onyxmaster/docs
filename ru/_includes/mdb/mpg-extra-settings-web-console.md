- **Начало резервного копирования (UTC)** — время по UTC в 24-часовом формате, в которое начинается резервное копирование кластера. Если время не задано, резервное копирование начинается в 22:00 UTC.

- **Срок хранения автоматических резервных копий, дней** — время, в течение которого нужно хранить созданные автоматически резервные копии. Если для такой копии истекает срок хранения, то она удаляется. Значение по умолчанию — {{ mpg-backup-retention }} дней. Подробнее см. в разделе [{#T}](../../managed-mongodb/concepts/backup.md).

    Изменение срока хранения затрагивает как новые автоматические резервные копии, так и уже существующие. Например, изначальный срок хранения был 7 дней. Оставшееся время жизни отдельной автоматической резервной копии при таком сроке — 1 день. При увеличении срока хранения до 9 дней оставшееся время жизни этой резервной копии будет уже 3 дня.

    Автоматические резервные копии кластера хранятся заданное количество дней, а созданные вручную — бессрочно. После удаления кластера все копии хранятся 7 дней.

- {% include [Maintenance window](console/maintenance-window.md) %}

- **Доступ из {{ datalens-name }}** — опция разрешает анализировать данные из кластера в сервисе [{{ datalens-full-name }}](../../datalens/concepts/index.md).

- **Доступ из консоли управления** — опция разрешает выполнять SQL-запросы к базам кластера из консоли управления {{ yandex-cloud }}.

- **Доступ из Serverless** — включите эту опцию, чтобы разрешить доступ к кластеру из сервиса [{{ sf-full-name }}](../../functions/concepts/index.md). Подробнее о настройке доступа см. в документации [{{ sf-name }}](../../functions/operations/database-connection.md).

- **Сбор статистики** — опция разрешает использовать в кластере инструмент [{#T}](../../managed-postgresql/operations/performance-diagnostics.md). Эта функциональность находится на стадии [Preview](../../overview/concepts/launch-stages.md).

- **Автоматическое переключение мастера** — включите эту опцию, чтобы при смене мастера источник репликации для всех хостов-реплик автоматически переключился на новый хост-мастер. Подробнее см. в разделе [Репликация](../../managed-postgresql/concepts/replication.md).


- **Режим работы менеджера подключений** — выберите один из [режимов работы менеджера подключений](../../managed-postgresql/concepts/pooling.md).

- {% include [Deletion protection](console/deletion-protection.md) %}

    {% include [Ограничения защиты от удаления](deletion-protection-limits-db.md) %}
