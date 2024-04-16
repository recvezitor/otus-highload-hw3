# otus-highload-hw3
Репликация

### Инструкция

* Вместо `Patroni` используется `repmgr` от EnterpriseDB
* Запустить docker compose файл `docker compose -f docker/docker-compose.yml up`
* потушить мастер командой `docker stop postgres_1`
* В логах обнаружить:
```
postgres_2     | NOTICE: STANDBY PROMOTE successful
postgres_2     | DETAIL: server "pg-2" (ID: 1002) was successfully promoted to primary
```
* Восстановить старый 'мастер' комнадой `docker start postgres_1`:
```
postgres_1     | LOG:  database system is ready to accept read-only connections
```
* При настройке ДатаСорса DB_URL указать `jdbc:postgresql://localhost:32769,localhost:32770/test_db?connectTimeout=1&hostRecheckSeconds=2&socketTimeout=600&targetServerType=primary`
* При настройке дополнительного ДатаСорса, который читает только с реплики указать `targetServerType=secondary`
