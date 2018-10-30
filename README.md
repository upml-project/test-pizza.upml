Zend Framework 3 Simple Application
=======================

## Настройка приложения
- создать пустую базу данных для приложения, к примеру используя pma
- убедиться в том, что в файле /config/autoload/doctrine.global.php указаны правильные доступы к БД. Если они не верны, нужно создать файл /config/autoload/doctrine.local.php, где указать нужные доступы
- в корне проекта выполнить:
    - `php composer.phar install`
    - `chmod -R 777 /data/cache`
    - `chmod -R 777 /public/tmp`
    - `chmod -R 777 /public/images`
    - `chmod -R 777 /public/uploads`
    - `./vendor/bin/doctrine-module -n migrations:migrate`

* Документация по модулю миграций библиотеки Doctrine - http://docs.doctrine-project.org/projects/doctrine-migrations/en/latest/index.html
    Самые необходимые команды:
    - `./vendor/bin/doctrine-module list migrations` - список доступных команд с пояснениями;
    - `./vendor/bin/doctrine-module -n migrations:migrate` - выполнить миграцию до последней версии не задавая вопросов;
    - `./vendor/bin/doctrine-module migrations:diff` - автоматически создать миграцию после внесения правок в entity;
    - `./vendor/bin/doctrine-module migrations:execute YYYYMMDDHHMMSS --down` - выполнить откат миграции с указанным номером;
    - `./vendor/bin/doctrine-module migrations:migrate --help` - список доступных аргументов команды миграции

    Для создания миграции нужно использовать команду
    - `./vendor/bin/doctrine-module migrations:diff --filter-expression='~^(?!email|user|state|city|count|product|attr|zip|category|white_ip|banner)~'`

    Для создания миграции для конкретной entity можно использовать команду
    - `./vendor/bin/doctrine-module migrations:diff --filter-expression='~^(table_name)~'`
    где table_name - название таблички новой entity

    Для удаление версии миграции можно использовать команду
    - `./vendor/bin/doctrine-module migrations:version YYYYMMDDHHMMSS --delete`

* Для включения режима отладки выполнить команду composer development-enable
