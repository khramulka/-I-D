# Домашнее задание к занятию "`Что такое DevOps. СI/СD`" - `Храмов Александр`

### Задание 1

**Что нужно сделать:**

1. Установите себе jenkins по инструкции из лекции или любым другим способом из официальной документации. Использовать Docker в этом задании нежелательно.
2. Установите на машину с jenkins [golang](https://golang.org/doc/install).
3. Используя свой аккаунт на GitHub, сделайте себе форк [репозитория](https://github.com/netology-code/sdvps-materials.git). В этом же репозитории находится [дополнительный материал для выполнения ДЗ](https://github.com/netology-code/sdvps-materials/blob/main/CICD/8.2-hw.md).
3. Создайте в jenkins Freestyle Project, подключите получившийся репозиторий к нему и произведите запуск тестов и сборку проекта ```go test .``` и  ```docker build .```.

В качестве ответа пришлите скриншоты с настройками проекта и результатами выполнения сборки.

---

### Решение 1

1. Создана ВМ на Яндекс облаке с образом диска jenkins на ubuntu. Она же будет использоваться для работы registry и golang.
Проведена первоначальная настройка jenkins. http://158.160.129.4:8080/
![Инициализация jenkins](https://github.com/duskdemon/sys-29-hw-8.02/blob/main/img/8-02-vmyc-jenki.png)
2. Установлен golang из репозитория ubuntu: **sudo apt install golang**
3. Установлен докер: **sudo apt install docker.io**
Сделаны настройки по добавлению пользователя jenkins в группу docker и разрешение на использование http-репозитория.
4. Из докер-хаба скачан nexus: **sudo docker pull sonatype/nexus3**, запущен с пробросом порта 8081-8082 и проведена
начальная настройка. Запуск командой **docker run -d -p 8081:8081 -p :8082:8082 --name nexus -e INSTALL4J_ADD_VM_PARAMS="-Xms512m -Xmx512m -XX:MaxDirectMemorySize=273m" sonatype/nexus3**. Создан репозиторий для загрузки образа docker
![настройка nexus](https://github.com/duskdemon/sys-29-hw-8.02/blob/main/img/8-02-vmyc-nexus.png)
5. Создана задача с приведенными параметрами и запущена сборка, завершившаяся успешно.
![задача 1](https://github.com/duskdemon/sys-29-hw-8.02/blob/main/img/8-02-vmyc-jenk1.png)
![сборка 1](https://github.com/duskdemon/sys-29-hw-8.02/blob/main/img/8-02-vmyc-build1.png)
![загрузка в nexus](https://github.com/duskdemon/sys-29-hw-8.02/blob/main/img/8-02-vmyc-repo1.png)

---

### Задание 2

**Что нужно сделать:**

1. Создайте новый проект pipeline.
2. Перепишите сборку из задания 1 на declarative в виде кода.

В качестве ответа пришлите скриншоты с настройками проекта и результатами выполнения сборки.

---

### Решение 2

1. Настройки приведены в вид пайплайна 
![загрузка в nexus](https://github.com/duskdemon/sys-29-hw-8.02/blob/main/img/8-02-vmyc-jenk2.png)
2. Запущена сборка
![загрузка в nexus](https://github.com/duskdemon/sys-29-hw-8.02/blob/main/img/8-02-vmyc-build2.png)

---

### Задание 3

**Что нужно сделать:**

1. Установите на машину Nexus.
1. Создайте raw-hosted репозиторий.
1. Измените pipeline так, чтобы вместо Docker-образа собирался бинарный go-файл. Команду можно скопировать из Dockerfile.
1. Загрузите файл в репозиторий с помощью jenkins.

В качестве ответа пришлите скриншоты с настройками проекта и результатами выполнения сборки.

---

### Решение 3

1. Создан raw repo в nexus, переделан пайплайн на сборку на golang вместо docker-образа, и push в репо через curl
![задача 3](https://github.com/duskdemon/sys-29-hw-8.02/blob/main/img/8-02-vmyc-jenk3.png)
2. Запущена сборка
![сборка 3](https://github.com/duskdemon/sys-29-hw-8.02/blob/main/img/8-02-vmyc-build3.png)
