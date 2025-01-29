# Урок 5 Язык запросов SQL )

Данное домашнее задание выполнено в ClickHouse v24.12.3 установленного в docker container.
Все данные с которыми я работал во время выполнения ДЗ прокинуты в корень текущего репозитория и загружены в git
Если потребуется более детальная проверка ДЗ, контейнер запустится с базами которыми я работал. 

Как запустить контейнера ClickHouse?

``` 
docker compose up --build -d
```

Как попасть в контейнер с ClickHouse?

``` 
docker compose exec clickhouse-server bash
```
Как авторизоваться в ClickHouse?

```
clickhouse-client --user default --password 12345
```

Этапы выполнения ДЗ

1) Создать новую базу данных и перейти в нее.

![1.png](src%2Fimg%2F1.png)

2) Создать таблицу для бизнес-кейса "Меню ресторана" с 5+ полями, наполнить ее данными. Обязательно указывать, где нужно, модификаторы Nullable, LowCardinality и пр. Добавить комментарии.

![2.png](src%2Fimg%2F2.png)

![3.png](src%2Fimg%2F3.png)

3) Протестировать CRUD на созданной таблице.

Добавление записи

![4.png](src%2Fimg%2F4.png)

Удаление записи

![5.png](src%2Fimg%2F5.png)

Редактирование записи

![6.png](src%2Fimg%2F6.png)

Выборка данных

![7.png](src%2Fimg%2F7.png)

![8.png](src%2Fimg%2F8.png)

4) Добавить несколько новых полей, удалить пару старых.

![9.png](src%2Fimg%2F9.png)

5) Заселектить таблицу (любую) из sample dataset - https://clickhouse.com/docs/en/getting-started/example-datasets/menus.

Для выполнения пятого задания создал новую базу с именем dataset

![10.png](src%2Fimg%2F10.png)

Скачивание и распоковка датасете

![11.png](src%2Fimg%2F11.png)

Создание таблиц

![12.png](src%2Fimg%2F12.png)

![13.png](src%2Fimg%2F13.png)

![14.png](src%2Fimg%2F14.png)

![15.png](src%2Fimg%2F15.png)

Импорт данных

```
clickhouse-client  --user default --password 12345 --format_csv_allow_single_quotes 0 --input_format_null_as_default 0 --query "INSERT INTO dataset.dish FORMAT CSVWithNames" < Dish.csv
clickhouse-client  --user default --password 12345 --format_csv_allow_single_quotes 0 --input_format_null_as_default 0 --query "INSERT INTO dataset.menu FORMAT CSVWithNames" < Menu.csv
clickhouse-client  --user default --password 12345 --format_csv_allow_single_quotes 0 --input_format_null_as_default 0 --query "INSERT INTO dataset.menu_page FORMAT CSVWithNames" < MenuPage.csv
clickhouse-client  --user default --password 12345 --format_csv_allow_single_quotes 0 --input_format_null_as_default 0 --date_time_input_format best_effort --query "INSERT INTO dataset.menu_item FORMAT CSVWithNames" < MenuItem.csv
```

Для разнообразия подключился к ClickHouse через датагрит.

Для примера получил кол-во блюд на всех страницах меню с id 12882 используя подзапрос

![16.png](src%2Fimg%2F16.png)

Рассчитал среднюю стоимость блюда для меню с id 12882 на всех страницах

![17.png](src%2Fimg%2F17.png)

Рассчитал среднюю стоимость блюда для меню с id 12882 на каждой странице

![18.png](src%2Fimg%2F18.png)