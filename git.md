**1. Undo a commit & redo**

**2. Добавить файл в последний коммит. Для этого используется опция --amend.**

**3. Изменить любой незапушенный коммит**

**4. Отменить изменения в конкрентном файле последнего коммита**

**5. Внести изменения в любой коммит в середине**

**6. Компактный вывод истории коммитов**

**7. Ошибка Filename too long при добавлении файлов в индекс**

**8. Смена ссылки на удаленный репозиторий при изменении адреса репозитория или метода доступа к нему(например, с https на ssh)**

**1. Undo a commit & redo**
```bash
$ git commit -m "Something terribly misguided" # (0: Your Accident)
$ git reset HEAD~                              # (1)
[ edit files as necessary ]                    # (2)
$ git add .                                    # (3)
$ git commit -c ORIG_HEAD                      # (4)
```
1. git reset is the command responsible for the undo. It will undo your last commit while leaving your working tree (the state of your files on disk) untouched. You'll need to add them again before you can commit them again.

2. Make corrections to working tree files.

3. git add anything that you want to include in your new commit.

4. Commit the changes, reusing the old commit message. reset copied the old head to .git/ORIG_HEAD; commit with -c ORIG_HEAD will open an editor, which initially contains the log message from the old commit and allows you to edit it.
If you do not need to edit the message, you could use the -C option.

[link](https://stackoverflow.com/questions/927358/how-do-i-undo-the-most-recent-local-commits-in-git)


Чтобы сохранить файл и выйти из редактора Vim, используйте команду :wq.

Для этого:

Нажмите Esc, чтобы переключиться в обычный режим.

Введите :wq.


**2. Добавить файл в последний коммит. Для этого используется опция --amend.**

Пример использования

Просмотрим историю коммитов.
```bash
$ git log

commit 5c4a8e76f951eb7ee157f4136257f6666fddf1d1
Author: John Doe <johndoe@gmail.com>
Date:   Sun Aug 28 14:40:30 2016 +0300

    Changed 1.txt

commit 7f2ad8c26ad032800c049d0d6122c43410a5cbbc
Author: John Doe <johndoe@gmail.com>
Date:   Sun Aug 28 14:39:30 2016 +0300

    Initial commit
```
Допустим существует файл который нужно добавить в предыдущий коммит.
```bash
$ git status

On branch master
Untracked files:
   (use "git add <file>..." to include in what will be committed)    
        test.txt
```
Добавьте этот файл в индекс при помощи команды git add.
```bash
$ git add --all

$ git status

On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)
        new file:   test.txt
```
После этого вы можете добавить файл в последний коммит посредством использования --amend в команде git commit. Вы можете также изменить сообщение коммита добавив -m 'Commit message'. Чтобы оставить сообщение коммита тем же просто передайте пустую строку вместо сообщения -m ''.
```bash
$ git commit -m 'Added test' --amend

[master aad3e76] Added test
 Date: Sun Aug 28 14:40:30 2016 +0300
 2 files changed, 2 insertions(+), 1 deletion(-)
 create mode 100644 test.txt
```
Проверим историю коммитов.
```bash
$ git log --stat
commit aad3e7653cd76c4afa1a9272bd421493b4e3055c
Author: John Doe <johndoe@gmail.com>
Date:   Sun Aug 28 14:40:30 2016 +0300

     Added test

 1.txt    | 3 ++-
 test.txt | 0
 2 files changed, 2 insertions(+), 1 deletion(-)

commit 7f2ad8c26ad032800c049d0d6122c43410a5cbbc
Author: John Doe <johndoe@gmail.com>
Date:   Sun Aug 28 14:39:30 2016 +0300

     Initial commit

 1.txt | 1 +
 1 file changed, 1 insertion(+)
```
[link](https://ru.stackoverflow.com/questions/559711/%D0%9C%D0%BE%D0%B6%D0%BD%D0%BE-%D0%BB%D0%B8-%D0%B2-git-%D0%B4%D0%BE%D0%B1%D0%B0%D0%B2%D0%B8%D1%82%D1%8C-%D0%B5%D1%89%D0%B5-%D0%BE%D0%B4%D0%B8%D0%BD-%D1%84%D0%B0%D0%B9%D0%BB-%D0%B2-%D0%BF%D0%BE%D1%81%D0%BB%D0%B5%D0%B4%D0%BD%D0%B8%D0%B9-%D0%BB%D0%BE%D0%BA%D0%B0%D0%BB%D1%8C%D0%BD%D1%8B%D0%B9-%D0%BA%D0%BE%D0%BC%D0%B8%D1%82)

**3. Изменить любой незапушенный коммит**
[https://habr.com/ru/companies/flant/articles/536698/](https://habr.com/ru/companies/flant/articles/536698/)

**4. Отменить изменения в конкрентном файле последнего коммита**

Для этого надо вернуть состояние файла как в предпоследнем коммите и применить это состояние к последнему коммиту
Для того чтобы посмотреть какие файлы находятся в коммитах 
```bash
$ git log --name-status
```

Допустим, файл называется example.txt

```bash
$ git checkout HEAD~1 example.txt
$ git commit --amend
```
В итоге в последнем коммите изменений в этом файле не будет.

Если надо совсем удалить файл из последнего коммита
```bash
$ git rm --cached example.txt
$ git commit --amend
```
**5. Внести изменения в любой коммит в середине**

[https://confluence.atlassian.com/stashkb/how-do-you-make-changes-on-a-specific-commit-747831891.html](https://confluence.atlassian.com/stashkb/how-do-you-make-changes-on-a-specific-commit-747831891.html)

**6. Компактный вывод истории коммитов**
```bash
$ git log --oneline
```

```bash
$ git log --pretty=format:"%h %ad %s" --date=human
```
, где
```
# %h  - сокращенный хеш
# %ad - дата коммита (формат зависит от --date)
# %an - имя автора (в примере не используется)
# %s  - сообщение коммита
# --date=short - формат даты YYYY-MM-DD или --date=human - формат даты без вывода часового пояса
```
Результат:
```
33fa350 9 minutes ago Сообщение коммита
```
**7. Ошибка Filename too long при добавлении файлов в индекс**

Для локального репозитория

```bash
$ git config core.longpaths true
```

Либо в Win >=10 можно решить вопрос кардинально, включив по умолчанию опцию для поддержки длинных имен файлов
[https://gist.github.com/leodutra/a25bc1f51e8779943df0a95d5a4839d1](https://gist.github.com/leodutra/a25bc1f51e8779943df0a95d5a4839d1)


**8. Смена ссылки на удаленный репозиторий при изменении адреса репозитория или метода доступа к нему(например, с https на ssh)**

В Git remote — это просто именованная ссылка на URL удаленного репозитория. Обычно:

origin — основной удаленный репозиторий, созданный по умолчанию при клонировании;
могут быть и другие remote, например: upstream — оригинальный репозиторий, если вы сделали fork;backup — дополнительный репозиторий для резервного копирования.
Посмотреть список remote можно так:

```bash
git remote -v
# origin  git@github.com:user/project.git (fetch)   // URL для получения изменений
# origin  git@github.com:user/project.git (push)    // URL для отправки изменений
```

Каждый remote имеет свой URL. Именно его вы будете менять с помощью git remote set-url.

#### Команда git remote set-url — базовый синтаксис
Команда git remote set-url позволяет изменить URL, привязанный к конкретному remote.

Базовый синтаксис:

```bash
git remote set-url <имя-remote> <новый-URL>
```
Где:

<имя-remote> — обычно origin, но может быть любое другое имя;
<новый-URL> — новый путь до удаленного репозитория (SSH или HTTPS).

Пример:

```bash
git remote set-url origin git@github.com:user/new-project.git
// Меняем URL для remote origin на новый SSH-адрес
```

После этого команда git push origin main будет отправлять данные уже по новому адресу.

Просмотр текущих URL удаленных репозиториев
Прежде чем что-то менять, лучше убедиться, какие remote уже настроены.

Список всех remote с URL
```bash
git remote -v
// Показывает все удаленные репозитории и их URL
```

Пример вывода:

```bash
origin  https://github.com/user/old-project.git (fetch)
origin  https://github.com/user/old-project.git (push)
upstream  git@github.com:org/main-repo.git (fetch)
upstream  git@github.com:org/main-repo.git (push)
```

Здесь вы видите:

два remote: origin и upstream;
для каждого указаны URL для fetch и push.
Получение URL только одного remote
Если вам нужно посмотреть URL конкретного remote:

```bash
git remote get-url origin
// Показывает URL, привязанный к remote origin (обычно для fetch)
```

Можно вывести URL сразу для всех:

```bash
git remote get-url --all origin
// Покажет URL для fetch и push, если они отличаются
```

Типичные сценарии использования git remote set-url
Давайте разберем самые частые ситуации, когда вам нужно изменить URL удаленного репозитория.

1. Переезд репозитория на другой хостинг
Например, вы перенесли проект с GitHub на GitLab.

Старый URL:

https://github.com/user/project.git
Новый URL:

git@gitlab.com:user/project.git
Пошагово:

```bash
git remote -v
// Проверяем текущий URL

git remote set-url origin git@gitlab.com:user/project.git
// Меняем URL для origin на адрес GitLab

git remote -v
// Убеждаемся, что URL обновился
```

Теперь все git push и git pull будут работать с GitLab.

2. Переход с HTTPS на SSH (или наоборот)
Многие начинают работать с Git по HTTPS, а позже переходят на SSH для удобства (чтобы не вводить пароль каждый раз).

Переход HTTPS → SSH
Старый URL:

https://github.com/user/project.git
Новый URL:

git@github.com:user/project.git
Команда:

git remote set-url origin git@github.com:user/project.git
// Переключаем origin на SSH-URL
Переход SSH → HTTPS
Старый URL:

git@github.com:user/project.git
Новый URL:

https://github.com/user/project.git
Команда:

```bash
git remote set-url origin https://github.com/user/project.git
// Переключаем origin на HTTPS-URL
```

Обратите внимание
Формат SSH и HTTPS URL отличается, но Git одинаково хорошо понимает оба варианта, если вы корректно настроили доступ.

3. Переименование или перенос репозитория на том же сервере
Бывает, что репозиторий просто переименовали, не меняя хостинг:

было: https://git.company.com/team/old-name.git
стало: https://git.company.com/team/new-name.git
В этом случае:

```bash
git remote set-url origin https://git.company.com/team/new-name.git
// Меняем только путь, хост остается прежним
```

Изменение URL только для fetch или только для push
Иногда вам нужно, чтобы Git получал изменения (fetch) из одного места, а отправлял (push) — в другое. Это менее распространенный, но вполне рабочий сценарий.

Например:

вы читаете изменения из центрального репозитория компании;
пушите их в свой форк.
Разные URL для fetch и push
Смотрите, я покажу вам схему:

fetch: git@github.com:company/project.git
push: git@github.com:your-account/project.git
Настроить это можно так:

```bash
git remote set-url --fetch origin git@github.com:company/project.git
// Устанавливаем URL для получения изменений

git remote set-url --push origin git@github.com:your-account/project.git
// Устанавливаем URL для отправки изменений
Проверяем:

git remote -v
// origin  git@github.com:company/project.git (fetch)
// origin  git@github.com:your-account/project.git (push)
```

Теперь вы:

получаете обновления из репозитория компании;
отправляете свои изменения в собственный форк.
Восстановление одного URL и для fetch, и для push
Если вы хотите вернуть одинаковый URL для обоих направлений:

```bash
git remote set-url origin git@github.com:your-account/project.git
// Этот URL будет использоваться и для fetch и для push
```

После этого git remote -v покажет одинаковые строки для обеих операций.

Добавление и переименование remote против изменения URL
Иногда вместо git remote set-url лучше использовать другие команды. Давайте разберем, когда что применять.

Когда использовать git remote set-url
Используйте git remote set-url, если:

только URL изменился, а логика работы с remote осталась прежней;
вы просто переехали на другой сервер;
поменялся протокол (SSH ↔ HTTPS), но сам репозиторий тот же.
Тогда достаточно одной команды:

```bash
git remote set-url origin <новый-URL>
```

Когда лучше добавить новый remote
Если вы хотите работать с двумя разными удаленными репозиториями одновременно, правильнее не менять URL, а добавить новый remote:

```bash
git remote add backup git@gitlab.com:user/project-backup.git
// Добавляем дополнительный удаленный репозиторий backup
```

Теперь:

origin — основной;
backup — дополнительный, например, для резервного копирования.
Отправка в конкретный remote:

```bash
git push origin main
// Отправляем изменения в origin

git push backup main
// Отправляем те же изменения в резервный репозиторий backup
```

Когда переименовать remote (git remote rename)
Если вам нужно просто поменять имя remote (например, из origin в github), используйте:

```bash
git remote rename origin github
// Меняем имя remote origin на github, URL при этом не меняется
```

А затем при необходимости меняйте его URL:

```bash
git remote set-url github git@github.com:user/project.git
// Обновляем адрес для нового имени remote
```

[https://purpleschool.ru/knowledge-base/git/remote/set_url](https://purpleschool.ru/knowledge-base/git/remote/set_url)
