# Тестирование входа в систему интернет-банка 
Тестирование входа в систему интернет-банка через вэб-интерфейс на базе готовой схемы БД.
## Необходимые условия для проведения тестирования
Перед началом работы убедитесь, что на вашем ПК установлены:

1.Git

2.IntelliJ IDEA с поддержкой Java

3.Docker Desktop или Docker Toolbox

4.Браузер Google Chrome


**Окружение**:
OS Version: Windows 10, сборка 1909

Java version: AdoptOpenjdk version "11.0.9.1"

## Начало работы

1) Для получения копии проекта создайте новый проект в IntelliJ IDEA на базе Java и системы сборки Gradle.
2) Инициализируйте git репозиторий командой `git init`.
3) подключите данный репозиторий как удаленный командой `git remote https://github.com/Rina043/TaskAuto_3.2.1`.
4) Получите копию репозитория на ваш локальный ПК командой `git pull`.
5) Установите Docker Desktop или Docker Toolbox (в зависимости от вашей ОС). Подробная информация по установке в [этой](https://github.com/netology-code/aqa-homeworks/blob/aqa4/docker/installation.md) инструкции.
6) Если установили Docker Toolbox, то запустите ярлык "Docker Quickstart Terminal" на рабочем столе и дождитесь появления окна терминала:![123](https://user-images.githubusercontent.com/67234113/104813935-a0d0ba00-5825-11eb-8e15-9c57253b0515.png)

## **Установка и запуск**
1. Вам нужно запустить docker контейнер. Все параметры для запуска контейнера уже прописаны в `docker-compose.yml`. Volumes настроены таким образом, что sql схема запустится и на вашей локальной машине.
Для запуска используйте команду 
`docker-compose up`

Ожидайте появления сообщения о готовности базы к подключению:
```
[System] [MY-010931] [Server] /usr/sbin/mysqld: ready for connections. Version: '8.0.19'  socket: '/var/run/mysqld
/mysqld.sock'  port: 3306  MySQL Community Server - GPL.
```
2. Теперь устанавливаем связь с сервером и запускаем SUT. Для этого открываем новую вкладку в Терминале IDEA и вводим следующую команду:
```
java -jar artifacts/app-deadline.jar -P:jdbc.url=jdbc:mysql://192.168.99.100:3306/app -P:jdbc.user=app -P:jdbc.password=pass
```
Дожидаемся сообщения, которое будет означать готовность SUT к работе:
```
2020-10-08 21:30:53.830 [DefaultDispatcher-worker-1] INFO  Application - No ktor.deployment.watch patterns specified, automatic reload is not active
2020-10-08 21:30:54.998 [DefaultDispatcher-worker-1] INFO  Application - Responding at http://0.0.0.0:9999
```
3. Теперь запускаем тесты стандартной командой `./gradlew clean test`
 Они должны проходить.
4. Если возникла необходимость повторного запуска тестов - перезапустите приложение вручную. Для этого можно просто закрыть окно терминала с запущенным приложением и кликнуть на кнопку "Terminate" во всплывающем окне. Затем для повторного запуска приложения, введите команду `java -jar ./artifacts/app-deadline.jar.`
При этом повторно запускать контейнер и базу не требуется.
