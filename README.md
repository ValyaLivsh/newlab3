## Laboratory work II

Данная лабораторная работа посвещена изучению систем контроля версий на примере **Git**.

```bash
$ open https://git-scm.com
```

## Tasks

- [ ] 1. Создать публичный репозиторий с названием **lab02** и с лиценцией **MIT**
- [ ] 2. Сгенирировать токен для доступа к сервису **GitHub** с правами **repo**
- [ ] 3. Ознакомиться со ссылками учебного материала
- [ ] 4. Выполнить инструкцию учебного материала
- [ ] 5. Составить отчет и отправить ссылку личным сообщением в **Slack**

## Tutorial

```sh
$ export GITHUB_USERNAME=<имя_пользователя>
$ export GITHUB_EMAIL=<адрес_почтового_ящика>
$ export GITHUB_TOKEN=<сгенирированный_токен>
$ alias edit=<nano|vi|vim|subl>
```

```sh
$ cd ${GITHUB_USERNAME}/workspace
$ source scripts/activate
```

```sh
$ mkdir ~/.config
$ cat > ~/.config/hub <<EOF
github.com:
- user: ${GITHUB_USERNAME}
  oauth_token: ${GITHUB_TOKEN}
  protocol: https
EOF
$ git config --global hub.protocol https
```

```sh
$ mkdir projects/lab02 && cd projects/lab02
$ git init
$ git config --global user.name ${GITHUB_USERNAME}
$ git config --global user.email ${GITHUB_EMAIL}
# check your git global settings
$ git config -e --global
$ git remote add origin https://github.com/${GITHUB_USERNAME}/lab02.git
$ git pull origin master
$ touch README.md
$ git status
$ git add README.md
$ git commit -m"added README.md"
$ git push origin master
```

Добавить на сервисе **GitHub** в репозитории **lab02** файл **.gitignore**
со следующем содержимом:

```sh
*build*/
*install*/
*.swp
.idea/
```

```sh
$ git pull origin master
$ git log
```

```sh
$ mkdir sources
$ mkdir include
$ mkdir examples
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

```sh
$ cat > include/print.hpp <<EOF
#include <fstream>
#include <iostream>
#include <string>

void print(const std::string& text, std::ofstream& out);
void print(const std::string& text, std::ostream& out = std::cout);
EOF
```

```sh
$ cat > examples/example1.cpp <<EOF
#include <print.hpp>

int main(int argc, char** argv)
{
  print("hello");
}
EOF
```

```sh
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

```sh
$ edit README.md
```

```sh
$ git status
$ git add .
$ git commit -m"added sources"
$ git push origin master
```

## Report

```sh
$ cd ~/workspace/
$ export LAB_NUMBER=02
$ git clone https://github.com/tp-labs/lab${LAB_NUMBER}.git tasks/lab${LAB_NUMBER}
$ mkdir reports/lab${LAB_NUMBER}
$ cp tasks/lab${LAB_NUMBER}/README.md reports/lab${LAB_NUMBER}/REPORT.md
$ cd reports/lab${LAB_NUMBER}
$ edit REPORT.md
$ gist REPORT.md
```

## Homework

### Part I

1. Создайте пустой репозиторий на сервисе github.com (или gitlab.com, или bitbucket.com).
https://github.com/ValyaLivsh/lab02_homework
2. Выполните инструкцию по созданию первого коммита на странице репозитория, созданного на предыдещем шаге.
```
$ cd ../
$ git clone https://github.com/AlexCoder47/lab02_homework.git
$ cd lab02_homework
```
3. Создайте файл `hello_world.cpp` в локальной копии репозитория (который должен был появиться на шаге 2). Реализуйте программу **Hello world** на языке C++ используя плохой стиль кода. Например, после заголовочных файлов вставьте строку `using namespace std;`.
```
$ code hello_world.cpp
```
```
#include <iostream>

using namespace std;

int main() {
	cout << "Hello world!" << endl;
}
```
```
$ g++ hello_world.cpp
$ ./a.out
Hello world!
```
4. Добавьте этот файл в локальную копию репозитория.
```
$ git add .
```
5. Закоммитьте изменения с *осмысленным* сообщением.
```
$ git commit -m "create hello_world"
```
6. Изменитьте исходный код так, чтобы программа через стандартный поток ввода запрашивалось имя пользователя. А в стандартный поток вывода печаталось сообщение `Hello world from @name`, где `@name` имя пользователя.
```
$ code hello_world.cpp
```
```
#include <iostream>

using namespace std;

int main()
{
	string name;

	cout << "Input name: ";
	cin >> name;

	cout << "Hello world from " + name << endl;
}
```
```
$ g++ hello_world.cpp
$ ./a.out
Input name: Valya
Hello world from Valya
```
7. Закоммитьте новую версию программы. 
```
$ git commit -m "add input name"
```
8. Запуште изменения в удалёный репозиторий.
```
$  git push origin main
Username for 'https://github.com': ValyaLivsh
Password for 'https://ValyaLivsh@github.com': 
Enumerating objects: 6, done.
Counting objects: 100% (6/6), done.
Delta compression using up to 4 threads
Compressing objects: 100% (5/5), done.
Writing objects: 100% (5/5), 13.71 KiB | 4.57 MiB/s, done.
Total 5 (delta 0), reused 0 (delta 0), pack-reused 0
To https://github.com/ValyaLivsh/lab02_homework
   33ac359..4f5c92d  main -> main
```

### Part II

**Note:** *Работать продолжайте с теми же репоззиториями, что и в первой части задания.*
1. В локальной копии репозитория создайте локальную ветку `patch1`.
```
$ git branch patch1
$ git checkout patch1
```
2. Внесите изменения в ветке `patch1` по исправлению кода и избавления от `using namespace std;`.
```
$ code hello_world.cpp
```
```
#include <iostream>

int main()
{
	std::string name;

	std::cout << "Input name: ";
	std::cin >> name;

	std::cout << "Hello world from " + name << std::endl;
}
```
3. **commit**, **push** локальную ветку в удалённый репозиторий.
```
$ git add .
$ git commit -m "change style code"
$ git push origin patch1
```
4. Создайте pull-request `patch1 -> master`.
5. В локальной копии в ветке `patch1` добавьте в исходный код комментарии.
6. **commit**, **push**.
```
$ git add .
$ git commit -m "add comments"
$ git push origin patch1
```
7. В удалённый репозитории выполните  слияние PR `patch1 -> master` и удалите ветку `patch1` в удаленном репозитории.
8. Локально выполните **pull**.
```
$ git checkout main
$ git pull origin main
```
9. С помощью команды **git log** просмотрите историю в локальной версии ветки `master`.
```
$ git log
```
10. Удалите локальную ветку `patch1`.
```
$ git branch -d patch1
Ветка patch1 удалена (была c59e9bc)
```

### Part III

**Note:** *Работать продолжайте с теми же репоззиториями, что и в первой части задания.*
1. Создайте новую локальную ветку `patch2`.
```
$ git branch patch2
$ git checkout patch2
```
2. Добавление изменений в ветке patch1 по исправлению кода и избавления от using namespace std;.
```
$ clang-format -style=Mozilla hello_world.cpp
```
3. **commit**, **push**, создайте pull-request `patch2 -> master`.
```
$ git add .
$ git commit -m "use clang-format"
$ git push origin patch2
```
4. В ветке **master** в удаленном репозитории измените комментарии, например, расставьте знаки препинания, переведите комментарии на другой язык.
```
$ git checkout main
```
5. Убедитесь, что в pull-request появились *конфликтны*.
6. Для этого локально выполните **pull** + **rebase** (точную последовательность команд, следует узнать самостоятельно). **Исправьте конфликты**.
```
$ git pull
$ git checkout patch2
$ git rebase main
Автослияние hello_world.cpp
КОНФЛИКТ (содержимое): Конфликт слияния в hello_world.cpp
error: не удалось применить коммит d50808c... use clang-format
Не удалось применить коммит d50808c... use clang-format

$ git add .
$ git status
интерактивное перемещение в процессе; над 15c337a
Last command done (1 command done):
   pick d50808c use clang-format
Команд больше не осталось.
Вы сейчас редактируете коммит при перемещении ветки  «patch2» над «15c337a».
  (используйте «git commit --amend», чтобы исправить текущий коммит)
  (используйте «git rebase --continue», когда будете довольны изменениями)

$ git commit -m "final commit"
$ git rebase --continue
Успешно перемещён и обновлён refs/heads/patch2.
```
7. Сделайте *force push* в ветку `patch2`
```
$ git push -f origin patch2
```

## Links

- [hub](https://hub.github.com/)
- [GitHub](https://github.com)
- [Bitbucket](https://bitbucket.org)
- [Gitlab](https://about.gitlab.com)
- [LearnGitBranching](http://learngitbranching.js.org/)

```
Copyright (c) 2015-2021 The ISC Authors
```
