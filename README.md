# DePostgres

Я написал [docker-compose.yaml](docker-compose.yaml) файл так, чтобы поднималась локально база данных Postgres и графический клиент pgAdmin для взаимодействия с базой данных.
После того, как контейнеры запущены командой ```docker compose up -d```, нужно открыть браузер и набрать ```http://localhost:8080/```.

Откроется окно, где нужно будет в поле логина ввести ```admin@admin.com```, а в поле пароля ввести ```root``` (просто потому что я так задал всё сам).

Далее нужно будет нажать на поле ```Server``` как на картинке и проделать все шаги так, как на последующих картинках:

![](img1.jpg)
![](img2.jpg)
![](img3.jpg)

В качестве пароля также нужно использовать ```root```.

Когда база данных поднята, нужно создать в ней таблицы и заполнить их данными. Для этого нужно запустить скрипт [ingest_spacex_data.py](ingest_spacex_data.py). Эта программа получает данные из [SpaceX link](https://studio.apollographql.com/public/SpaceX-pxxbxen/home?variant=current) с помощью GraphQL API и переносит их в базу данных postgres. Таблицу payloads я решил не переносить, так как она пустая. 

Чтобы подсчитать кол-во публикаций по миссиям, ракетам и пускам, нужно написать следующие запросы к полученной базе данных:

```SELECT COUNT(*) from missions```

```SELECT COUNT(*) from rockets```

```SELECT COUNT(*) from launches```

Модель данных выглядит следующим образом: [Модель данных](model.png)
