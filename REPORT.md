md
# Лабораторная работа №2

## Тема
Системы контроля версий на примере Git

## Цель работы
Освоить базовые операции с Git: создание репозитория, ветки, pull request, разрешение конфликтов.

## Ход выполнения

### Настройка окружения
```bash
export GITHUB_USERNAME=psychoxdune-dot
export GITHUB_EMAIL=<твоя_почта>
export GITHUB_TOKEN=<токен>
alias edit=nano
Создание репозитория lab02
bash
mkdir -p projects/lab02 && cd projects/lab02
git init
git config --global user.name ${GITHUB_USERNAME}
git config --global user.email ${GITHUB_EMAIL}
git remote add origin https://github.com/${GITHUB_USERNAME}/lab02.git
Добавление файлов
bash
touch README.md
git add README.md
git commit -m "added README.md"
git push origin master
Создание .gitignore
На сервисе GitHub добавлен файл .gitignore:

text
*build*/
*install*/
*.swp
.idea/
Добавление исходного кода
Создана структура проекта:

sources/print.cpp — реализация функции print

include/print.hpp — заголовочный файл

examples/example1.cpp и example2.cpp — примеры использования

bash
git add .
git commit -m "added sources"
git push origin master
Домашнее задание
Часть I. Работа с коммитами
Создан файл hello_world.cpp (плохой стиль):

cpp
#include <iostream>
using namespace std;

int main() {
    cout << "Hello, World!" << endl;
    return 0;
}
Добавлен и закоммичен:

bash
git add hello_world.cpp
git commit -m "added hello_world with bad style"
git push origin master
Изменена программа — добавлен ввод имени:

cpp
#include <iostream>
#include <string>
using namespace std;

int main() {
    string name;
    cout << "Enter your name: ";
    cin >> name;
    cout << "Hello world from " << name << endl;
    return 0;
}
Коммит с флагом -a (автоматически добавляет изменения в отслеживаемых файлах):

bash
git commit -a -m "added name input"
git push origin master
История коммитов:

bash
git log --oneline
text
b632996 added name input
f5aa352 added hello_world with bad style
acfa469 added sources
b8cd9f5 added .gitignore
5c513fa added README.md
5281290 Initial commit
Часть II. Ветки и pull request
Создана ветка patch1:

bash
git checkout -b patch1
Исправлен код — удалён using namespace std:

cpp
#include <iostream>
#include <string>

int main() {
    std::string name;
    std::cout << "Enter your name: ";
    std::cin >> name;
    std::cout << "Hello world from " << name << std::endl;
    return 0;
}
Коммит и пуш ветки:

bash
git commit -a -m "removed using namespace std"
git push origin patch1
Создан pull request через GitHub из patch1 в master.

Добавлены комментарии в код:

cpp
#include <iostream>
#include <string>

int main() {
    // Запрашиваем имя пользователя
    std::string name;
    std::cout << "Enter your name: ";
    std::cin >> name;
    // Выводим приветствие
    std::cout << "Hello world from " << name << std::endl;
    return 0;
}
Дополнительный коммит и пуш:

bash
git commit -a -m "added comments"
git push origin patch1
Выполнено слияние pull request на GitHub. Ветка patch1 удалена.

Обновление локального master:

bash
git checkout master
git pull origin master
git branch -d patch1
Итоговая история после слияния:

bash
git log --oneline
text
89f4088 Merge pull request #1 from psychoxdune-dot/patch1
8a1994a added comments
7a83d57 removed using namespace std
b632996 added name input
f5aa352 added hello_world with bad style
acfa469 added sources
b8cd9f5 added .gitignore
5c513fa added README.md
5281290 Initial commit
Часть III. Конфликты и clang-format
Создана ветка patch2:

bash
git checkout -b patch2
Применён clang-format в стиле Mozilla:

bash
clang-format -style=Mozilla -i hello_world.cpp
Коммит и пуш:

bash
git commit -a -m "apply clang-format Mozilla style"
git push origin patch2
Создан pull request. В ветке master через веб-интерфейс изменены комментарии — создан конфликт.

Разрешение конфликта через rebase:

bash
git checkout master
git pull origin master
git checkout patch2
git rebase master
Конфликт разрешён вручную, затем:

bash
git add hello_world.cpp
git rebase --continue
git push --force-with-lease origin patch2
После успешного разрешения pull request был слит, ветка patch2 удалена.

Итоговая история:

bash
git log --oneline
text
a58890e Merge pull request #2 from psychoxdune-dot/patch2
a6b89d0 apply clang-format Mozilla style
958dd12 Update comments in master
89f4088 Merge pull request #1 from psychoxdune-dot/patch1
8a1994a added comments
7a83d57 removed using namespace std
b632996 added name input
f5aa352 added hello_world with bad style
acfa469 added sources
b8cd9f5 added .gitignore
5c513fa added README.md
5281290 Initial commit
Вывод
В ходе лабораторной работы были освоены:

базовые операции Git (init, add, commit, push, pull)

работа с ветками (checkout -b, push origin branch)

создание pull request на GitHub

разрешение конфликтов через rebase

применение clang-format

force push с флагом --force-with-lease
