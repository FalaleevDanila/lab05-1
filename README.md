[![Build Status](https://travis-ci.com/Toliak/lab05.svg?branch=master)](https://travis-ci.com/Toliak/lab05)
## Laboratory work II

Данная лабораторная работа посвещена изучению систем контроля версий на примере **Git**.

```bash
$ open https://git-scm.com
```

## Tasks

- [x] 1. Создать публичный репозиторий с названием **lab05** и с лиценцией **MIT**
- [x] 2. Сгенирировать токен для доступа к сервису **GitHub** с правами **repo**
- [x] 3. Ознакомиться со ссылками учебного материала
- [x] 4. Выполнить инструкцию учебного материала
- [x] 5. Составить отчет и отправить ссылку личным сообщением в **Slack**

## Tutorial

Установка переменных

```ShellSession
$ export GITHUB_USERNAME=Toliak                                     # Установка переменной GITHUB_USERNAME
$ export GITHUB_EMAIL=ibolosik@gmail.com                            # Установка переменной GITHUB_EMAIL
$ export GITHUB_TOKEN=xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx      # Установка переменной GITHUB_TOKEN
$ alias edit=nano                                                   # Установка синонима команды edit
```

Подготовка рабочего места

```ShellSession
$ cd ${GITHUB_USERNAME}/workspace               # Переход в папку workspace
$ source scripts/activate                       # Выполнение скрипта подготовки
```

Конфигурация hub

```ShellSession
$ mkdir ~/.config                               # Создание папки с конфигами
mkdir: cannot create directory ‘/home/toliak/.config’: File exists
$ cat > ~/.config/hub <<EOF                     # Создание файла конфига hub и запись в него
github.com:
- user: ${GITHUB_USERNAME}
  oauth_token: ${GITHUB_TOKEN}
  protocol: https
EOF
$ git config --global hub.protocol https        # Установка переменной конфига git
```

Работа с git

```ShellSession
$ mkdir projects/lab05 && cd projects/lab05             # Создание папки и переход в нее
$ git init                                              # Создание пустого репозиторий
Initialized empty Git repository in /home/toliak/Documents/Toliak/workspace/projects/lab05/.git/
$ git config --global user.name ${GITHUB_USERNAME}      # Установка переменной конфига user.name для git
$ git config --global user.email ${GITHUB_EMAIL}        # Установка переменной конфига user.email для git
# check your git global settings
$ git config -e --global                                # Вывод всего конфига из git
[user]
        email = ibolosik@gmail.com
        name = Toliak
[hub]
        protocol = https
$ git remote add origin https://github.com/${GITHUB_USERNAME}/lab05.git     # Добавление ссылки на репозиторий на гитхабе
$ git pull origin master                                                    # Перенос изменения с гитхаба
remote: Enumerating objects: 3, done.
remote: Counting objects: 100% (3/3), done.
remote: Compressing objects: 100% (2/2), done.
remote: Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
Unpacking objects: 100% (3/3), done.
From https://github.com/Toliak/lab05
 * branch            master     -> FETCH_HEAD
 * [new branch]      master     -> origin/master
$ touch README.md                                                           # Создать README.md
$ git status                                                                # Посмотреть статус репозитория
On branch master
Untracked files:
  (use "git add <file>..." to include in what will be committed)

        README.md

nothing added to commit but untracked files present (use "git add" to track)
$ git add README.md                                                         # Добавить README.md в список фиксированных
$ git commit -m"added README.md"                                            # Закоммитить фиксированные изменения
[master 44830ab] added README.md
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 README.md
$ git push origin master                                                    # Отправить изменения на гитхаб
Username for 'https://github.com': Toliak
Password for 'https://Toliak@github.com': 
Enumerating objects: 4, done.
Counting objects: 100% (4/4), done.
Delta compression using up to 4 threads
Compressing objects: 100% (2/2), done.
Writing objects: 100% (3/3), 277 bytes | 277.00 KiB/s, done.
Total 3 (delta 0), reused 0 (delta 0)
To https://github.com/Toliak/lab05.git
   fb79117..44830ab  master -> master
```

Добавить на сервисе **GitHub** в репозитории **lab05** файл **.gitignore**
со следующем содержимом:

```ShellSession
*build*/
*install*/
*.swp
.idea/
```

Перенос изменений с гитхаба

```ShellSession
$ git pull origin master        # Перенос изменений с гитхаба
remote: Enumerating objects: 4, done.
remote: Counting objects: 100% (4/4), done.
remote: Compressing objects: 100% (2/2), done.
remote: Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
Unpacking objects: 100% (3/3), done.
From https://github.com/Toliak/lab05
 * branch            master     -> FETCH_HEAD
   44830ab..c52a23e  master     -> origin/master
Updating 44830ab..c52a23e
Fast-forward
 .gitignore | 4 ++++
 1 file changed, 4 insertions(+)
 create mode 100644 .gitignore
$ git log                       # Просмотр коммитов
commit c52a23ea39cd2bfb22ae8e5d6b108eaafea7431b (HEAD -> master, origin/master)
Author: Toliak <ibolosik@gmail.com>
Date:   Mon Mar 18 18:43:35 2019 +0300

    Create .gitignore

commit 44830ab32d44d1a6c1b97bcfed20d2b79c04e4fd
Author: Toliak <ibolosik@gmail.com>
Date:   Mon Mar 18 18:36:55 2019 +0300

    added README.md

commit fb79117022cbe4d85efa783dd41cdbaeeb5e9da5
Author: Toliak <ibolosik@gmail.com>
Date:   Mon Mar 18 18:19:54 2019 +0300

    Initial commit
```

Создание папок и файла с кодом

```ShellSession
$ mkdir sources                     # Создание папки sources
$ mkdir include                     # Создание папки include
$ mkdir examples                    # Создание папки examples
$ cat > sources/print.cpp <<EOF     # Запись кода в файл
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

Создание файла с кодом

```ShellSession
$ cat > include/print.hpp <<EOF         # Запись кода в файл
#include <fstream>
#include <iostream>
#include <string>

void print(const std::string& text, std::ofstream& out);
void print(const std::string& text, std::ostream& out = std::cout);
EOF
```

Создание файла с кодом

```ShellSession
$ cat > examples/example1.cpp <<EOF         # Запись кода в файл
#include <print.hpp>

int main(int argc, char** argv)
{
  print("hello");
}
EOF
```

Создание файла с кодом

```ShellSession
$ cat > examples/example2.cpp <<EOF         # Запись кода в файл
#include <print.hpp>

#include <fstream>

int main(int argc, char** argv)
{
  std::ofstream file("log.txt");
  print(std::string("hello"), file);
}
EOF
```

Редактирование README.md

```ShellSession
$ edit README.md                # Редактировать README.md
```

Просмотр состояния репозитория и отправка изменений на гитхаб

```ShellSession
$ git status                            # Просмотр статуса репозитория
$ git add .                             # Фиксация всех изменений
$ git commit -m"added sources"          # Коммит зафиксированных изменений
$ git push origin master                # Отправка изменений на гитхаб
```

## Report

```ShellSession
$ cd ~/workspace/labs/
$ export LAB_NUMBER=02
$ git clone https://github.com/tp-labs/lab${LAB_NUMBER}.git tasks/lab${LAB_NUMBER}
$ mkdir reports/lab${LAB_NUMBER}
$ cp tasks/lab${LAB_NUMBER}/README.md reports/lab${LAB_NUMBER}/REPORT.md
$ cd reports/lab${LAB_NUMBER}
$ edit REPORT.md
$ gistup -m "lab${LAB_NUMBER}"
```

## Homework

### Part I

1. Создайте пустой репозиторий на сервисе github.com (или gitlab.com, или bitbucket.com).
2. Выполните инструкцию по созданию первого коммита на странице репозитория, созданного на предыдещем шаге.
3. Создайте файл `hello_world.cpp` в локальной копии репозитория (который должен был появиться на шаге 2). Реализуйте программу **Hello world** на языке C++ используя плохой стиль кода. Например, после заголовочных файлов вставьте строку `using namespace std;`.
4. Добавьте этот файл в локальную копию репозитория.
5. Закоммитьте изменения с *осмысленным* сообщением.
6. Изменитьте исходный код так, чтобы программа через стандартный поток ввода запрашивалось имя пользователя. А в стандартный поток вывода печаталось сообщение `Hello world from @name`, где `@name` имя пользователя.
7. Закоммитьте новую версию программы. Почему не надо добавлять файл повторно `git add`?
8. Запуште изменения в удалёный репозиторий.
9. Проверьте, что история коммитов доступна в удалёный репозитории.

### Part II

**Note:** *Работать продолжайте с теми же репоззиториями, что и в первой части задания.*
1. В локальной копии репозитория создайте локальную ветку `patch1`.
2. Внесите изменения в ветке `patch1` по исправлению кода и избавления от `using namespace std;`.
3. **commit**, **push** локальную ветку в удалённый репозиторий.
4. Проверьте, что ветка `patch1` доступна в удалёный репозитории.
5. Создайте pull-request `patch1 -> master`.
6. В локальной копии в ветке `patch1` добавьте в исходный код комментарии.
7. **commit**, **push**.
8. Проверьте, что новые изменения есть в созданном на **шаге 5** pull-request
9. В удалённый репозитории выполните  слияние PR `patch1 -> master` и удалите ветку `patch1` в удаленном репозитории.
10. Локально выполните **pull**.
11. С помощью команды **git log** просмотрите историю в локальной версии ветки `master`.
12. Удалите локальную ветку `patch1`.

### Part III

**Note:** *Работать продолжайте с теми же репоззиториями, что и в первой части задания.*
1. Создайте новую локальную ветку `patch2`.
2. Измените *code style* с помощью утилиты [**clang-format**](http://clang.llvm.org/docs/ClangFormat.html). Например, используя опцию `-style=Mozilla`.
3. **commit**, **push**, создайте pull-request `patch2 -> master`.
4. В ветке **master** в удаленном репозитории измените комментарии, например, расставьте знаки препинания, переведите комментарии на другой язык.
5. Убедитесь, что в pull-request появились *конфликтны*.
6. Для этого локально выполните **pull** + **rebase** (точную последовательность команд, следует узнать самостоятельно). **Исправьте конфликты**.
7. Сделайте *force push* в ветку `patch2`
8. Убедитель, что в pull-request пропали конфликтны. 
9. Вмержите pull-request `patch2 -> master`.

## Links

- [hub](https://hub.github.com/)
- [GitHub](https://github.com)
- [Bitbucket](https://bitbucket.org)
- [Gitlab](https://about.gitlab.com)
- [LearnGitBranching](http://learngitbranching.js.org/)

```
Copyright (c) 2015-2019 The ISC Authors
```