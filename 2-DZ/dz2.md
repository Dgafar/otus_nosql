Цель:
В результате выполнения ДЗ вы научитесь разворачивать MongoDB, заполнять данными и делать запросы.


Описание/Пошаговая инструкция выполнения домашнего задания:
Необходимо:

установить MongoDB одним из способов: ВМ, докер;
заполнить данными;
написать несколько запросов на выборку и обновление данных


Отчёт
1. Скачивание и создание контейнера с монго: docker run --name some-mongo -p 27017:27017 -d mongo:latest
![img.png](img.png)

2. Подключение к бд через командную строку: docker exec -it some-mongo mongosh
![img_1.png](img_1.png)

3. Показать все базы данных: show dbs
![img_3.png](img_3.png)

4.	Создание БД фильмов:
      А.  Скачивание джейсона: https://github.com/neelabalan/mongodb-sample-dataset/blob/main/sample_mflix/movies.json
      Б. Копирование его во временную папку в контейнере: docker cp movies.json some-mongo:/tmp/movies.json
      В. Создание новой БД: docker exec some-mongo mongoimport --db movies --collection movies --drop --file /tmp/movies.json
![img_4.png](img_4.png)

5.	Переход в созданную базу: use movies
6.	Посмотреть доступные коллекции: show collections
![img_2.png](img_2.png)

7.	Посмотреть данные в коллекции фильмов: db.movies.find()
8.	Выбрать все фильмы 1986 года db.movies.find({ year: {$in: [1986]}})
9.	Выбрать все испанские фильмы старше 1986 года: db.movies.find({$and: [{ year: { $gte: 1986} }, {countries: "Spain"}]})
![img_5.png](img_5.png)

10.	Добавить отечественный фильм: db.movies.insertOne({countries: 'Russia', genres: ['Drama', 'Action'], runtime: 96, rated: 'R', cast: ['Серргей Бодров', 'Виктор Сухоруков'], year: 1997})
![img_6.png](img_6.png)

11.	Проверка, что фильм добавился: db.movies.find({cast: "Серргей Бодров"})
![img_7.png](img_7.png)

12.	Исправляем ошибку: db.movies.updateOne({cast: "Серргей Бодров"}, {$set: {cast: ['Сергей Бодров', 'Виктор Сухоруков']}})
![img_8.png](img_8.png)

13.	Проверяем что исправилось: db.movies.find({cast: "Сергей Бодров"})
![img_9.png](img_9.png)