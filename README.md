# Лабораторная работа: Docker и Apache

**Студент:** [Имя Фамилия], группа [номер]  
**Дата:** 06.05.2026

---

## Цель

Познакомиться с базовыми командами Docker и Ubuntu, запустить Apache в контейнере.

## Задание

Запустить контейнер Ubuntu, установить Apache и открыть страницу "Hello, World!" в браузере.

---

## Выполнение

Запустил контейнер с пробросом порта:

```bash
docker run -ti -p 8000:80 --name containers04 ubuntu bash
```

Внутри контейнера установил и запустил Apache:

```bash
apt update
apt install apache2 -y
service apache2 start
```

По адресу `http://localhost:8000` открылась стандартная страница Apache.

Заменил `index.html`:

```bash
echo '<h1>Hello, World!</h1>' > /var/www/html/index.html
```

После обновления страницы в браузере появился текст **Hello, World!**

Посмотрел конфиг Apache:

```bash
cat /etc/apache2/sites-enabled/000-default.conf
```

Из него видно, что сервер слушает порт 80 и отдаёт файлы из `/var/www/html`.

Вышел из контейнера, удалил его:

```bash
exit
docker ps -a        # контейнер в статусе Exited
docker rm containers04
```

---

## Выводы

Развернул Apache внутри контейнера и убедился, что проброс портов даёт доступ к нему с хоста. Все изменения внутри контейнера исчезают после его удаления — для постоянного хранения нужны volumes.

---

## Источники

1. Документация Docker — https://docs.docker.com/
2. Документация Apache — https://httpd.apache.org/docs/
