# otus-highload-hw3
Репликация

### Инструкция

Запустить файл docker-compose.yml

docker compose up

Автоматически запустит мастера и реплику

Альтернативно можно определить параметры мастера через postgres.conf, но не забыть прописать расположение файла через команду -c

```
    services:
        postgresql-master:
        image: postgres:14
        shm_size: 1g
        ports:
        - "5432:5432"
        environment:
            POSTGRES_USERNAME: postgres
            POSTGRES_DATABASE: postgres
            POSTGRES_PASSWORD: postgres
        volumes:
          - ./pg_master/01_init.sql:/docker-entrypoint-initdb.d/init.sql
          - ./pg_master/02_schema.sql:/docker-entrypoint-initdb.d/schema.sql
          - ./pg_master/postgres.conf:/etc/postgresql/postgresql.conf
        command: postgres -c config_file=/etc/postgresql/postgresql.conf
```


Для проверки вставить данные в мастер и проверить на реплике

insert into otus_highload.person (id, first_name, second_name, birthdate, biography, city, created_at, updated_at)
values ('370c779a-3570-49e4-b066-34f1c06f494d', 'name1', 'secondName1', '2010-01-01', 'text text', 'Vladivostok', now(), null); 
