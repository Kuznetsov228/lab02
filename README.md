## Laboratory work II

Данная лабораторная работа посвещена изучению систем контроля версий на примере **Git**.

```bash
$ open https://git-scm.com
```

## Tasks

- [x] 1. Создать публичный репозиторий с названием **lab02** и с лиценцией **MIT
- [x] 2. Сгенирировать токен для доступа к сервису **GitHub** с правами **repo**
- [x] 3. Ознакомиться со ссылками учебного материала
- [x] 4. Выполнить инструкцию учебного материала
- [x] 5. Составить отчет и отправить ссылку личным сообщением в **Slack**

## Tutorial
Добавляем переменные для дальнейшей работы с ними, привязываем команду edit с вызовом текстового редактора Atom
```ShellSession
$ export GITHUB_USERNAME=Kuznetsov228
$ export GITHUB_EMAIL=dgin988@gmail.com
$ export GITHUB_TOKEN=****************************************
$ alias edit=atom
```
Переходим в нашу рабочую директорию и исполняем команду из файла activate, в котором прописана команда добавления в переменную PATH пути до nodejs
```ShellSession
$ cd ${GITHUB_USERNAME}/workspace
$ source scripts/activate
```
Конфигурируем hub

```ShellSession
# Создаем директорию .config
$ mkdir ~/.config
# Создаем файл hub и вписываем в него параметры и переменные
$ cat > ~/.config/hub <<EOF
github.com:
- user: ${GITHUB_USERNAME}
  oauth_token: ${GITHUB_TOKEN}
  protocol: https
EOF
# Для всего git устанавливаем протокол *https*
$ git config --global hub.protocol https
```
Создаем локальный репозиторий, настраиваем его, создаем файл README.md, делаем первый commit и синхронизируем с удаленным репозиторием

```ShellSession
# Создаем папку lab02
$ mkdir projects/lab02 && cd projects/lab02
# Создаем в этой папке репозиторий
$ git init
Инициализирован пустой репозиторий Git в /home/nikita/Kuznetsov228/workspace/projects/lab02/.git/
# Глобально добавляем в конфигурацию ключи user.name и user.email
$ git config --global user.name $ Kuznetsov228
$ git config --global user.email $ dgin988@gmail.com
# Открываем в текстовом редакторе общий файл конфигураций
$ git config -e --global

[hub]
        protocol = https
[user]
        name = $ Kuznetsov228
        email = $ dgin988@gmail.com
# Добавляем  репозиторий origin
$ git remote add origin https://github.com/${GITHUB_USERNAME}/lab02.git
# Получаем данные и файлы
$ git pull origin master
# Создаем файл
$ touch README.md
#Проверяем статус файла
$ git status
# Добавляем в индексацию README.md
$ git add README.md
# Выполняем commit файла и добавляем комментарий к коммиту
$ git commit -m"added README.md"
# Залить все изменения ветки master с локального на удаленный репозиторий
$ git push origin master
```

Добавить на сервисе **GitHub** в репозитории **lab02** файл **.gitignore**
со следующем содержимом:

```ShellSession
*build*/
*install*/
*.swp
.idea/
```

```ShellSession
# Выгрузить изменения всех веток с удаленного репозитория в ветку master
$ git pull origin master
# История изменений
$ git log
```

```ShellSession
 # Создаем директорий
$ mkdir sources
$ mkdir include
$ mkdir examples
# Запись кода в файл .cpp
$ cat > sources/print.cpp <<EOF
#include <print.hpp>

void print(const std::string& text, std::ostream& out)
{
  out << text;
}

void print(const std::string& text, std::ofstream& out)
{
  out << text;
}
EOF
```

```ShellSession
# Запись кода в .hpp файл
$ cat > include/print.hpp <<EOF
#include <fstream>
#include <iostream>
#include <string>

void print(const std::string& text, std::ofstream& out);
void print(const std::string& text, std::ostream& out = std::cout);
EOF
```

```ShellSession
# Запись кода в .сpp файл
$ cat > examples/example1.cpp <<EOF
#include <print.hpp>

int main(int argc, char** argv)
{
  print("hello");
}
EOF
```

```ShellSession
# Запись кода в .сpp файл
$ cat > examples/example2.cpp <<EOF
#include <print.hpp>

#include <fstream>

int main(int argc, char** argv)
{
  std::ofstream file("log.txt");
  print(std::string("hello"), file);
}
EOF
```

```ShellSession
# Редактируем файл README.md
$ edit README.md
```

```ShellSession
# Текущее стаутс репозитория
$ git status
# Обработка содержимого текущей директории
$ git add .
# Выполняем commit файла и добавляем комментарий к коммиту
$ git commit -m"added sources"
# Залить все изменения ветки master с локального на удаленный репозиторий
$ git push origin master
```

## Report

```ShellSession
$ cd ~/workspace/labs/
$ export LAB_NUMBER=02
# Устанавливаем значение переменной окружения LAB_NUMBER
$ git clone https://github.com/tp-labs/lab${LAB_NUMBER}.git tasks/lab${LAB_NUMBER}
# Создаем каталог lab${LAB_NUMBER}
$ mkdir reports/lab${LAB_NUMBER}
$ cp tasks/lab${LAB_NUMBER}/README.md reports/lab${LAB_NUMBER}/REPORT.md
# Меняем директорию на reports/lab${LAB_NUMBER}
$ cd reports/lab${LAB_NUMBER}
# Редактируем файл REPORT.md
$ edit REPORT.md
#Создаем Gist из командной строки и комментарием
$ gistup -m "lab${LAB_NUMBER}"
```


## Links

- [hub](https://hub.github.com/)
- [GitHub](https://github.com)
- [Bitbucket](https://bitbucket.org)
- [Gitlab](https://about.gitlab.com)
- [LearnGitBranching](http://learngitbranching.js.org/)

```
Copyright (c) 2015-2019 The ISC Authors
```
