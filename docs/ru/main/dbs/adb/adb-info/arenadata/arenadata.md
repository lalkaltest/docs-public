Описание
--------

Arenadata DB (ADB) – распределенная СУБД, использующая концепцию MPP (massively parallel processing, массивно-параллельные вычисления) и основанная на СУБД с открытым исходным кодом – Greenplum.

Аналитические массивно-параллельные СУБД предназначены для хранения и обработки больших объемов данных – от единиц до сотен терабайт данных. Такие СУБД чаще всего используются для предиктивной аналитики, регулярной отчетности, анализа оттока клиентов, построения корпоративных хранилищ данных.

Arenadata DB — это быстрое кластерное решение, с помощью которого можно разворачивать распределенные базы данных. Оно позволяет хранить и обрабатывать большие объемы структурированных и слабоструктурированных данных и строить на их основе модели, например, для BI-аналитики. В отличие от использования аналогичных аналитических баз данных On Premises, Arenadata DB как сервис позволяет до 5 раз ускорить построение сложных аналитических запросов благодаря возможности быстрого масштабирования до сотен узлов в облачной инфраструктуре VK CS.

Архитектура ADB – классический кластер: несколько серверов-сегментов, один сервер-мастер и один резервный, соединенные между собой быстрыми сетями. В каждом сервер-сегменте есть несколько сегментов (инстансов) PostgreSQL, содержащих данные. В случае отказа одного или нескольких сегментов они помечаются как сбойные и вместо них запускаются их зеркальные сегменты, репликация данных для которых происходит с помощью используемой в СУБД PostgreSQL технологии опережающей записи (Wright Ahead Log, WAL – все изменения таблиц и индексов записываются в файл только после их занесения в журнал).

Ключевые преимущества Arenadata DB
----------------------------------

*   Вся поддержка и экспертиза по внедрению доступна в России и на русском языке.
*   Разработан пакет утилит для оффлайн-установки (без доступа к сети Интернет).
*   Дистрибутив создан на базе Open-source ядра СУБД Greenplum.
*   Полностью российское программное обеспечение.
*   Поддержка доступна как удаленно, так и на месте (on-site). Есть набор доступных пакетных сервисов по планированию, установке, аудиту системы.
*   Есть возможность доработки и кастомизации продукта под конкретные потребности заказчика.
*   Доступна реализация как на «голом железе», так и в облаке.