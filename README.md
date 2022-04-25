# Краткое описание
GitLab — веб-приложение и система управления репозиториями программного кода для Git.

GitLab предлагает решение для хранения кода и совместной разработки масштабных программных проектов. Репозиторий включает в себя систему контроля версий для размещения различных цепочек разработки и веток, позволяя разработчикам проверять код и откатываться к стабильной версии софта в случае непредвиденных проблем.


## Установка
```
git clone https://github.com/iSmartyPRO/docker-gitlab.git gitlab
cd gitlab
vim .env
```
заполнить своими данными

Запустить установку:
```
docker-compose up -d
```

После успешной установки, можно узнать пароль супер админа:
```
docker exec -it gitlab grep 'Password:' /etc/gitlab/initial_root_password
```


в дополнении рекомендую использовать единую сеть для всех контейнеров, для этого отредактировав docker-compose.yml добавив следующие строки:
```
networks:
  default:
    external:
      name: "docker-net"
```


## Удаление
```
docker-compose down
```

# Дополнения

## Установка crontab
Для того чтобы выполнялись автоматически задачи EspoCRM - рекомендуется дополнительно настроить контейнер.

```
docker exec -ti espocrm bash
```

Установка зависимостей
```
apt update
apt install cron
apt install nano
```
Настройка crontab
```
nano /etc/crontab
```
Дописываем следующее:
```
* * * * * php -f /var/www/html/cron.php > /dev/null 2>&1
```

Проверяем службу cron при необходимости запускаем
```
service cron status
service cron start
```