<h1>ToDoList</h1>
Многопользовательский планировщик задач.

<h3>Использованные технологии</h3>
<ul><li>Java </li>
<li>Maven</li>
<li>Spring Boot, Spring Security, Spring Session, Spring AMQP, Spring Scheduler, Spring Mail</li>
<li>PostgreSQL, Spring Data JPA</li>
<li>Docker - контейнеры, образы, volumes, написание Dockerfile, Docker Compose</li>
<li>Брокер сообщений RabbitMQ - очереди</li>
<li>CI/CD, GitHub Actions</li> </ul>
<br>
При разработке проекта использовался микросервисный подход. 
<br>
<h3>Проект включает в себя 3 микросервиса:</h3>

<h4>Backend</h4>
Spring Boot (Java) приложение, реализующее REST API для работы с пользователями, сессиями, создаваемыми при авторизации, и задачами.
<p>

Работа с пользователями:

<ul><li>Регистрация</li>
<li>Авторизация</li>
<li>Logout</li></ui>
<br>
Работа с задачами:
<p>
<li>Создание, редактирование (каждая задача имеет заголовок и описание)</li>
<li>Пометка о выполнении задачи</li>
<li>Удаление</li>
https://github.com/LeontevaAnastasia/toDoListBackend
<br>
<h4>Рассыльщик писем</h4>
Spring Boot приложение с двумя модулями - Spring Mail и Spring AMQP.

С помощью Spring AMQP приложение подключается к RabbitMQ и создает очередь сообщений, после чего подписывается на сообщения, поступающие от планировщика и бэкенд-сервиса.

Для каждого полученного сообщения, содержимое которого десериализуется в экземпляр модели, используется модуль Spring Mail, чтобы отправить письмо на электронный адрес пользователя.
https://github.com/LeontevaAnastasia/toDoListEmailSender
<br>
<h4>Планировщик</h4>
Spring Boot приложение с двумя модулями - Spring Scheduler и Spring AMQP.

Задача сервиса - раз в сутки итерировать всех пользователей, формировать для них отчёты о задачах и изменениях в них за сутки, а также формировать email для отправки. 
Сформированные сообщения отправляются в RabbitMQ очередь.
https://github.com/LeontevaAnastasia/toDoListScheduler
