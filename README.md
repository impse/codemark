Необходимо разработать backend для Restful веб-приложения. Основная задача бекенда - управление пользователями и их ролями. Описание модели данных:  

У пользователя может быть несколько ролей, одна роль может быть у нескольких пользователей. Например, Вася - Админ и Оператор, Петя - Оператор и Аналитик. 
Атрибуты пользователя - Имя, Логин (первичный ключ), Пароль (шифровать пароль в рамках тестового задания не требуется, это просто строка). 
Атрибуты роли – id (первичный ключ), Имя. 
 

Необходимо: 

Разработать сервисы работы с данными. Сервисы должны работать с форматом JSON. Сделать GET, PUT, POST, DELETE REST сервисы, которые будут:
Получать список пользователей из БД (без ролей)
Получать конкретного пользователя (с его ролями) из БД
Удалять пользователя в БД
Добавлять нового пользователя с ролями в БД.
Редактировать существующего пользователя в БД. Если в запросе на редактирование передан массив ролей, система должна обновить список ролей пользователя в БД - новые привязки добавить, неактуальные привязки удалить.
На бекенде для методов добавления и редактирования должен производиться формато-логический контроль пришедших значений. Поля name, login, password - обязательные для заполнения, password содержит букву в заглавном регистре и цифру. 
Если все проверки пройдены успешно, должен вернуться ответ {success: true}
Если случилась ошибка валидации, то должен прийти ответ {success: false, errors: {массив ошибок}}
Для функционала добавления, редактирования и удаления пользователя должны быть написаны unit тесты. 
 

Решение должно быть реализовано на языке Java,  платформе Spring Framework / Springboot, использовать Spring Data или Hibernate в качестве ORM, и быть выложено в git (bitbucket или github). Базу данных для задачи можно выбрать любую и создать любым способом, на ваше усмотрение - автосоздание таблиц hibernate, скрипт создания create_schema.sql, допускается использовать in-memory БД. 

**Запуск приложения на Java 11**
java -jar codemark-0.0.1.jar
адрес для запросов
http://localhost:8080

**Endpoints**

GET /api/users - получить список всех пользователей

GET /api/users/{login} - получить пользователя по первичному ключу {login}

GET /api/roles - поучить список ролей

POST /api/users - добавить пользователя из тела запроса в формате json. 

POST /api/roles - добавить роль из тела запроса в формате json. 

PUT /api/users - изменить пользователя из тела запроса в формате json.

DELETE /api/users/{login} - удалить пользователя по первичному ключу {login}

**Примеры json для тела POST запросов**

**1. POST /api/users** 

_{
   "userLogin": "userlogin",
   "userName": "User Name",
   "password": "Password1"
}_

Создаст пользователя "userlogin" без ролей

**2. POST /api/roles**

_{
   "roleName": "Admin"
}_

Создаст роль "Admin"

**3. PUT /api/users**

_{
   "userLogin": "userlogin",
   "userName": "New Name",
   "password": "Password2",
   "roles": [
   {
   "id": 1,
   "roleName": "Admin"
   }            
   ]
}_

Отредактирует пользователя "userlogin", назначит ему роль "Admin"
